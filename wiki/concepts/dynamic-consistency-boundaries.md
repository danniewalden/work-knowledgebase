---
title: Dynamic Consistency Boundaries (DCB)
type: concept
created: 2026-06-14
updated: 2026-08-03
sources: [pellegrini-dynamic-consistency-boundary, dilger-dcb-is-what-event-sourcing-should-have-been, atomicobject-cqrs-event-sourcing-production-walkthrough, event-modeling-event-sourcing-podcast, rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb, fritzsche-ccc-atomic-append-serialized-write-order, dilger-first-event-modeling-conference-munich-recap, enzler-event-sourcing-aggregates-dcb-or-what, dilger-how-does-dcb-affect-event-modeling, fritzsche-command-context-consistency-principle]
tags: [event-sourcing, dcb, ddd, consistency, focus]
---

# Dynamic Consistency Boundaries (DCB)

*(Opened 2026-06-14 as a stub when Dannie broadened the focus to the Event Modeling design substrate;
the stub marker was removed 2026-08-30 — the page now runs to ten sources and covers origin, mechanism,
the CCC comparison and the tooling landscape.)*

A **Dynamic Consistency Boundary** defines a transactional consistency scope *at runtime,
per decision*, rather than fixing it up front in an aggregate. Origin: **[[sara-pellegrini]]**'s "Kill
Aggregate" series and her naming post ([[pellegrini-dynamic-consistency-boundary]], 2023); the idea is
also associated with **[[adam-dymitruk]]**.

## The idea

A decision in an event-sourced system is a function: **input** = the ordered stream of *relevant* past
events (the "given"); **output** = new events (the consequence). DCB is an **optimistic lock** for
that: append the output **iff** the relevant input stream is unchanged between load and append. The
event store needs two capabilities — **dynamic query** (select events by criteria, e.g. tags) and
**conditional append** (write only if the query result still matches). Immutability makes the check
cheap (compare the last event).

The payoff is escaping the **aggregate** as the mandatory consistency unit: consistency boundaries
become per-operation "temporary bubbles" that include just the events a decision needs, so the model
can evolve without re-architecting around early aggregate choices ("Aggregates introduce rigidity").

## Where it sits / why it's in the focus

DCB is part of the [[event-sourcing]] / [[cqrs]] design substrate around [[event-modeling]] (the
focus broadened to include it). It connects to several existing threads:

- **Event Modeling fit.** EM models decisions as command→event on a timeline; DCB is a principled
  answer to "which events must I read, and how do I append safely" for those decisions — boundaries
  drawn from the timeline rather than from aggregates.
- **Tooling adoption (out-of-window, foundational — not filed as new):** Axon Framework 5 shipped
  experimental DCB support (AxonIQ, Steven van Beelen, Jun 2025) using tag-based multi-stream
  queries; the Critter Stack's **Marten 9.0** added a higher-performance DCB option via PostgreSQL
  HSTORE ([[martin-dilger|—]] reported by [[jeremy-miller]] via *The Shade Tree Developer*, May 2026).
  *These are the canonical current implementations to capture if/when an in-window development lands.*
- **Agent angle (claimed).** Vendor framing argues DCB "reduces AI hallucinations" and lets the
  architecture evolve safely under agent-driven change — a possible bridge to
  [[event-modeled-agent-design]] worth watching, currently assertion-level.
- **Capability-ownership parallel.** [[rico-fritzsche]]'s [[autonomous-domain-capabilities|CCC/RPU]]
  pattern — build a decision's context from the *relevant recorded events*, not from a shared
  aggregate — is essentially DCB framed as a [[business-capabilities|capability]]-ownership pattern
  rather than a consistency mechanism. Same instinct, different lens.

## CCC vs DCB — same principle, different layer (Fritzsche, 2026-06-19)

The KB had left open *how (if at all) CCC differs operationally from DCB.* Fritzsche answers it directly
([[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]]): **same rejection principle, different
abstraction level.** Both reject an append if the command's relevant event context changed between read
and write. **CCC** ([[autonomous-domain-capabilities|Command Context Consistency]]) states that principle
*representation-agnostically* — tags, indexes, or other access structures are optional implementation
optimizations. **DCB** pins it to a specific **event-store contract**: event types + tags form the query
contract while the payload stays opaque to the store, so tags determine an event's discoverability *at
write time*. In his framing CCC is the conceptual guarantee and DCB is one tag-based store contract that
implements it — and crucially **neither is a synonym for Event Sourcing**, which is just the persistence
concept underneath. (His framing; a DCB proponent need not accept CCC as the more general layer.) Same
post argues **Event Sourcing does not require aggregates** at all — the "rebuild aggregate → call method →
append at expected version" recipe is one implementation, not the definition.

## Implementation: optimistic check isn't enough — you need a serialized write order (Fritzsche, 2026-06-23)

The "append iff the relevant input stream is unchanged" check above is necessary but, on its own,
**unsafe under real concurrency**. [[fritzsche-ccc-atomic-append-serialized-write-order|Fritzsche]] shows
that an *atomic* conditional append (a PostgreSQL CTE combining the Event-Query check with the insert)
still lets two incompatible decisions through: under **READ COMMITTED**, two commands can evaluate the
same Event Query, observe the same context version, both pass, and both write — atomicity orders nothing
*between* the two transactions. Achieving the boundary's guarantee therefore needs a **protected write
order (serialization)**, e.g. locking a single metadata row per append transaction: physical writes are
serialized globally while the conflict decision stays *local* to the command context (registrations for
*alice* and *bob* both succeed; two concurrent *alice*s cannot). The takeaway is a **store contract**,
not a lock — "atomicity safeguards one append; serialization prevents two decisions from the same
observed context from being accepted." This explains the *advisory-lock serialization* the
[[atomicobject-cqrs-event-sourcing-production-walkthrough|Atomic Object]] walkthrough mentions in passing.

## Third way — design the concurrency away (Enzler, 2026-06-23)

[[urs-enzler]] ([[enzler-event-sourcing-aggregates-dcb-or-what]]) sidesteps the whole choice: rather
than pick a consistency *mechanism*, **eliminate the concurrency that creates the consistency problem.**
He grants DCBs are "powerful, but quite complicated" and that DDD aggregates tend to grow "overly
large," then argues his team needed neither because (1) **"small data" + task-based UI** — a command
per task carrying only that task's data, **no unit-of-work** — makes conflicting commands vanishingly
unlikely; (2) you can often **replace a concurrent design with a non-concurrent one** (his course-
registration example: submit a *draft* intent, then a **single-threaded batch algorithm** resolves all
drafts — which also enables prioritisation and better global solutions); and (3) where serialisation
*is* genuinely needed, get it from **infrastructure** — Azure Service Bus **sessions** keyed on
tenant+employee+workday serialise validation *within* the boundary (plus scheduled grace-period
messages, dead-lettering, queue suspension). This is the concrete, production-grounded "**you might not
need it**" position, and it's a **third axis** on the debate below: DCB removes the boundary as a
modeling commitment; the conventional view keeps it but shrinks it; **Enzler removes the *concurrency*
so the boundary rarely binds.** Note his serialised-write step is the message-infrastructure analogue of
[[fritzsche-ccc-atomic-append-serialized-write-order|Fritzsche's]] "serialised write order" argument.
Caveat: an HR/time-tracking domain where concurrency is genuinely rare (his own caveat — "always
possible? Probably not").

## Counterpoint — the conventional "keep the aggregate small" view

Not everyone is killing the aggregate. [[atomicobject-cqrs-event-sourcing-production-walkthrough|Atomic
Object's production walkthrough]] states the mainstream discipline: *"an aggregate is a consistency
boundary — if a command handler is reaching across to other aggregates, you've drawn the boundary in
the wrong place; solve it with async projections, not bigger aggregates."* That is the same problem DCB
addresses (cross-entity decisions) handled the other way — keep the fixed boundary *small* and push
coordination into projections/sagas, rather than making the boundary *dynamic per decision*. Worth
holding both: DCB removes the boundary as a modeling commitment; the conventional view keeps it but
shrinks it. The KB surfaces the disagreement rather than picking a winner.

## Naming debate (Dilger, 2026-06-15)

[[martin-dilger]] ([[dilger-dcb-is-what-event-sourcing-should-have-been]]) makes a pointed naming
argument: "Dynamic Consistency Boundaries" is a poor, un-marketable term — we already had a good name
for what it describes, **"Event Sourcing."** The thing that actually deserved a qualifier is the
**aggregate-based** approach people struggle with: call *that* "**Static Consistency Boundaries**." So
DCB is event sourcing "what it always should have been," and the aggregate is the special case. (DCB
gets a prominent place in the 2nd edition of his book *Understanding Eventsourcing*.) Rhetorical, but
captures why the [[sara-pellegrini|"Kill Aggregate"]] line is gaining traction.

## Live in the room — DCB vs Aggregates at the first EM Conference (Oct 2025)

The DCB-vs-aggregates debate is no longer just online: it was the **top community-voted topic** at the
first Event Modeling Conference ([[dilger-first-event-modeling-conference-munich-recap]]), with
[[allard-buijze]] ([[axoniq]]) and [[adam-dymitruk]] in the room and practitioners on both sides
trading war stories — systems that scaled well on aggregates, systems that collapsed under them, teams
that adopted DCB and never looked back, teams that couldn't tell if it mattered. [[martin-dilger]]'s
read after "hundreds of systems": **"it depends"** — keep aggregates and risk later scaling pain, or
invest in DCB upfront. A useful corrective to the KB's more partisan captures (Dilger's own
"static-consistency-boundary" jab below; Fritzsche's CCC framing): the practitioner consensus is
situational, not settled.

## How DCB affects Event Modeling — "not at all; it gets simpler" (Dilger, 2026-07-06)

[[dilger-how-does-dcb-affect-event-modeling|Dilger]] answers the question the
[[dilger-first-event-modeling-conference-munich-recap|Munich conference]] kept raising ("where does the
Decision Model / the logic go?") from the **modeling** side, and the answer is *deflationary*: modeling
a few systems with DCB, he finds **the event model is unaffected — if anything it simplifies.** Three
consequences worth holding:

- **Swimlanes revert to integration, not stream design.** With aggregates gone as the unit, you model
  **one swimlane per system / bounded context**; lanes go back to showing **integration between systems
  and teams** (Payments = another team's system) rather than encoding stream boundaries. "Whenever
  information crosses a lane, pay attention." So DCB *removes* modeling ceremony rather than adding a
  new construct — a modeling-side complement to the storage-side "kill the aggregate" argument.
- **No separate "Decision Model."** The events a command handler must read are exactly the **GIVEN**
  clause of that slice's [[given-when-then|GWT]] scenarios — so you never model the decision context
  separately; "we don't." This is the KB's crispest statement of *why* GWT is load-bearing under DCB
  (see [[given-when-then]]).
- **Model → generated Criteria + tests.** DCB pushes the decision to per-command granularity; in Axon
  each handler declares a **Criteria** (an SQL-like query over event types for an id). Writing these by
  hand is cumbersome, so the **Axon Build Kit** for [[eventmodelers-ai]] generates them (and the tests)
  from the model — extending the [[dilger-build-kits-model-to-generated-code|build-kit]] /
  [[dilger-event-modeling-agent-harness|Agent Harness]] codegen thread. **Tags** are treated as
  **indices, not domain concepts** — absent from Discovery models, added in Detailed-Modeling (via a
  public schema; he reuses the `id`-attribute for now) "before handing the slice to an Agent."

This is a **fourth position** alongside the three below: where Enzler removes the *concurrency*, the
conventional view shrinks the boundary, and Pellegrini/DCB makes it dynamic, **Dilger's contribution is
that adopting DCB changes the *event model* barely at all — it just lets swimlanes mean integration
again.** Caveat: DCB-favorable, vendor-adjacent (Eventmodelers/Axon Build Kit), one worked example.

## DCB as a first-class modeling kind (ESDM, 2026-07)

[[thenativeweb|thenativeweb]]'s [[esdm-event-sourced-domain-modeling|ESDM]] language makes **Dynamic
Consistency Boundary a first-class kind** in its core schema, standing beside **Aggregate** as a
"consistency unit" — both in the schema and in ESDM's "documenting an existing system" guidance ("start
with the consistency units: every Aggregate, DCB, Process Manager, and Read Model"). A vendor treating
DCB as a peer of the aggregate at the *format* level (rather than a replacement or an implementation
detail) is a small but real signal that DCB is settling into the mainstream ES/DDD vocabulary — and a
data point on the [[dilger-dcb-is-what-event-sourcing-should-have-been|"DCB is just event sourcing done
right"]] side of the debate.

## What's open / to capture next

A primary write-up tying DCB to *agent* design (vs. plain event sourcing); the Pellegrini/Savić
conference talk; and the Axon AF5 / **Marten 9.0** ([[critter-stack]]) implementation docs as proper
sources if they re-surface in-window.

## On the podcast (2024–2026)

DCB is a running thread on the [[event-modeling-event-sourcing-podcast]]: first developed in **Ep 18
"The Future of Event Sourcing"** (2025-03) and recurring through Eps 38, 39, 41, 43 alongside the
aggregate-coupling argument — the conversational origin of Dilger's "DCB is event sourcing done right"
position. **Caveat:** the AI-generated show notes for Eps 38/43 expand "DCB" as *"Domain Command Bus,"*
which is a transcription/summarization error — the hosts mean **Dynamic Consistency Boundaries**. A
reminder to treat the podcast's auto-summaries as lossy.

## DCB is the tag-based form of a store-agnostic principle (CCC)

[[rico-fritzsche|Fritzsche's]] canonical [[command-context-consistency|CCC]] primary
([[fritzsche-command-context-consistency-principle]], 2026-07-26) reframes DCB's relationship to the
whole debate: the **principle** is *"record a command's outcome only while the facts its decision read
still hold"* — which **names no store**. DCB is that principle in **tag-based event-store** form (a
conditional append over a query); a relational database enforces the *same* principle with a conditional
`UPDATE`, `FOR SHARE`, and a `UNIQUE` constraint. So DCB is not a synonym for event sourcing, and not the
only way to get past the aggregate — it is one physical **guard** for a logical context. The design rule
that carries over: the guard must **cover the context and never less** (an aggregate version is a guard
far wider than most command contexts). See [[command-context-consistency]].

_Sources: [[pellegrini-dynamic-consistency-boundary]] · [[dilger-dcb-is-what-event-sourcing-should-have-been]] · [[atomicobject-cqrs-event-sourcing-production-walkthrough]] · [[event-modeling-event-sourcing-podcast]] · [[fritzsche-command-context-consistency-principle]]._
