---
title: Event Sourcing
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [semaphore-dymitruk-event-modeling, eventmodeling-what-is-event-modeling, akka-event-sourcing-backbone-agentic-ai, akka-agentic-systems-are-distributed-systems, atomicobject-cqrs-event-sourcing-production-walkthrough, event-modeling-event-sourcing-podcast, rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb, axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember, roden-event-sourcing-meets-mcp-whole-story-for-llms, enzler-event-sourcing-aggregates-dcb-or-what, adaptech-workflow-not-inside-giant-process-manager, fritzsche-choosing-storage-is-choosing-what-your-system-forgets, dudycz-fixing-bugs-in-event-sourcing, fritzsche-how-event-sourcing-grows-with-the-business, fritzsche-thinking-in-events, fritzsche-event-sourcing-is-not-an-audit-feature, dudycz-archiving-events-stream-lifetime-slicing, dudycz-checklist-first-event-sourcing-feature, axoniq-government-ai-explainability-requirements]
tags: [event-sourcing, pattern, cqrs, agentic-ai, architecture]
---

# Event Sourcing

A design pattern that stores state as an **append-only log of immutable events** rather
than overwriting rows in a database. [[adam-dymitruk]]'s analogy: like accounting,
**"no erasers are allowed"** — you only ever add events; current state is derived by
replaying them. The store is an **event store**: a database built to recall events in a
guaranteed order.

## Properties

- **Full history / audit** — every change is retained, so you can see how information
  evolved and who/what caused it.
- **No "downhill effect"** — changing state means appending one event, not carefully
  updating many interdependent queries.
- **Multiple projections** — the same events feed many read models / views, each isolated
  from the others.
- Per Dymitruk, adopting it is a modest change: ~80% of the work is the same UI-on-a-model
  app; the addition is the ordered, replayable ledger.

## Two domains this KB connects

1. **Information systems** — the partner pattern to [[event-modeling]]: the blueprint
   defines the contract for what each workflow step leaves on the ledger vs. projects to a
   screen. Lineage runs through [[cqrs]] and [[greg-young]].
2. **Agentic AI** — [[kevin-hoffman]] / [[akka]] argue event sourcing is the **"backbone"**
   of [[agentic-ai]]: because LLMs are nondeterministic, an immutable event log gives
   **perfect recall** (reproduce any agent's state and know *why*), **auditability**,
   durable inter-agent communication, and **agent/event versioning via replay**. Storing
   agent memory as replicated events also yields a distributed backbone
   ([[akka-agentic-systems-are-distributed-systems]]). For how this substrate maps onto
   [[anthropic]]'s concrete [[agentic-workflow-patterns]], see [[event-sourced-agentic-patterns]].

## Related

[[event-modeling]] · [[cqrs]] · [[dynamic-consistency-boundaries]] · [[vertical-slice-architecture]] ·
[[business-capabilities]] · [[autonomous-domain-capabilities]] · [[agentic-ai]] ·
[[event-sourced-agentic-patterns]] · [[event-driven-architecture]] · [[agentic-event-driven-systems]] ·
[[open-closed-principle]] · [[domain-driven-design]] · [[entity-centric-thinking]] ·
[[internal-vs-external-events]] · [[event-versioning-and-upcasting]] · [[decision-trace]]

**Substrate note (2026-06-14):** the focus now explicitly includes the event-sourcing design
substrate around Event Modeling — see [[dynamic-consistency-boundaries]] (per-decision consistency
scopes replacing the fixed aggregate) and [[vertical-slice-architecture]] (feature-slice organization
that yields [[cqrs]] and maps to Event Modeling slices).

**Update (2026-06-15):** [[martin-dilger]] argues DCB *is* event sourcing "what it always should have
been," recasting the aggregate as a *static* consistency boundary
([[dilger-dcb-is-what-event-sourcing-should-have-been]]). [[rico-fritzsche]] treats recorded events as
the **Application State** that capabilities (RPUs) interpret to form the domain
([[autonomous-domain-capabilities]]).

**Update (2026-06-19):** Fritzsche makes the "no aggregates" claim explicit —
**Event Sourcing does not require aggregates** ([[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]]):
ES is *defined* by the event history as source of truth, and the "rebuild aggregate → call method →
append at expected version" pattern is one implementation the DDD community conflated with the
definition. The same post separates the consistency layer from ES itself — [[autonomous-domain-capabilities|CCC]]
is the representation-agnostic principle, [[dynamic-consistency-boundaries|DCB]] a tag-based store
contract, **neither a synonym for Event Sourcing.**

**Production reference (2026-06-17):**
[[atomicobject-cqrs-event-sourcing-production-walkthrough|Atomic Object's production walkthrough]]
grounds the pattern in a real stack (NestJS + KurrentDB + PostgreSQL/Drizzle): commands-as-intent,
aggregate-as-state-machine with type-level exhaustiveness, **snapshots as a non-authoritative
optimization**, **upcasters/event-versioning from day one**, at-least-once **idempotent projections**,
and a split between transactional read-model projections and async side-effect projections. Its advice
to **keep aggregates small** (solve cross-aggregate work with async projections, not bigger aggregates)
is the conventional counterpoint to the [[dynamic-consistency-boundaries|DCB]] "kill the aggregate" line.

**Event store as agent memory — two payoffs (2026-06-21):** two new ES-vendor sources sharpen *why*
the immutable log matters for agents. [[axoniq]] ([[allard-buijze]]) argues **agent
[[agent-explainability|explainability]] is an infrastructure problem, not a model problem**:
state-based stores overwrite the causal history regulators now require (EU AI Act, SR 11-7, GDPR
Art. 22), and only an event store captures *why* a decision was made
([[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]]). It also draws a crisp
**event store vs. event stream** line — a store records *why* (full causal context, replayable); a
stream (Kafka) only moves *what*. [[golo-roden]] takes the *context-quality* angle: CRUD is "only the
last chapter," an event store gives an LLM "the whole story," and **events are the natural language for
LLMs**, reachable via [[model-context-protocol|MCP]]
([[roden-event-sourcing-meets-mcp-whole-story-for-llms]], [[context-engineering]]). Same backbone, two
payoffs: *explainability* (why it decided) and *context* (what it needs to decide well). See
[[agent-explainability]]. **Note that AxonIQ's framing is contested, and this page holds the dispute
open rather than settling it — see "Is history the point?" below.** AxonIQ is an event-store vendor, so
its explainability framing is an **interested claim** and carries that marker wherever it travels.

**Third-way substrate note (2026-06-23):** [[urs-enzler]]
([[enzler-event-sourcing-aggregates-dcb-or-what]], part 11 of his ES series) argues the cheapest
consistency boundary is often **no concurrency at all** — "small data" + a task-based UI
(command-per-task, no unit-of-work) and, where possible, replacing a concurrent design with a
non-concurrent one (draft-intent + single-threaded batch), serialising only where genuinely needed via
infrastructure (Azure Service Bus sessions). A pragmatic "you might not need aggregates *or* DCBs"
counterweight; see [[dynamic-consistency-boundaries]].

**Long-running workflows note (2026-07-29):** [[adaptech-group]]
([[adaptech-workflow-not-inside-giant-process-manager]]) argues the event log is the **durable
evidence** that makes long-running processes recoverable: rather than a large saga/process manager
holding hidden in-memory state, model progress as a **projected to-do list** read by focused
processors, so after a restart a processor can **verify rather than repeat** a possibly-completed
action. See [[process-managers-and-todo-lists]].

**Note (2026-06-12):** event sourcing is a pattern *within* the broader
[[event-driven-architecture]] family. Three external 2026 sources now apply it to agents directly:
[[confluent-agentic-event-driven-systems-architecture]] lists immutability, exactly-once, and
**deterministic replay** as production design principles for agent decisions, and
[[atlan-event-driven-architecture-for-ai-agents]] names event sourcing as a core agent-coordination
pattern — externally corroborating the Akka "backbone" thesis above. See [[agentic-event-driven-systems]].

**Practitioner commentary (2026-06-17):** the [[event-modeling-event-sourcing-podcast]] (Dymitruk &
[[martin-dilger]], 46 eps) is the running conversational source for this pattern — recurring hard parts
captured there include [[event-versioning-and-upcasting|schema migration / upcasting]] (Eps 5, 37, 46),
replay times and metrics (Ep 17), Git-as-event-store (Eps 26, 40), "SQL is an anti-pattern" (Ep 22),
and the historical framing "event sourcing predates anything in computing" + the accounting analogy
(Ep 39). Show-notes-level only (transcripts were blocked).

## Event Sourcing is a *storage decision*, not "thinking in events" (Fritzsche, 2026-07)

[[fritzsche-choosing-storage-is-choosing-what-your-system-forgets]] gives the concept its clearest
conceptual grounding by holding four words apart — **state** (what holds), **event** (a change at one
moment, whose *type* carries what the before/after pair loses), **fact** (a true statement bound to its
moment — "you cannot update a fact"), and **record** (a fact written to a store). The dividing line is
**the discipline of the record, nothing else**: an append-only relational table *keeps facts*; an event
log edited in place *keeps state under a misleading name*. "Overwritten records keep state; appended
records keep facts." So current state is **derived** (Greg Young: "a Left Fold of previous behaviours"),
and **Event Sourcing is the decision to make event records authoritative — one storage choice; "thinking
in events" does not depend on it.** This separates the *method* from the *store* (the same split Fritzsche
draws for [[agent-explainability]] and [[command-context-consistency]]).

## Fixing bad data: fix forward, and the `buildSha` trick (Dudycz, 2026-07)

The standard objection — "you can't fix bad data in an immutable log" — gets its first proper answer in
the KB ([[dudycz-fixing-bugs-in-event-sourcing]]), by running one incident twice. **All figures in it are
an invented hotel-pricing scenario, not data.**

- **Why the state-based recovery compounds.** The row holds a total with no record of the inputs, so the
  migration must **recompute** — against a rate plan revised since the booking, repricing rows that were
  never wrong; and its `WHERE` clause cannot distinguish "changed" from "changed because of the bug."
  Migration two is then written against migration one's output: "If we get that wrong, the input to
  migration three is the output of migration two." Preparing a state-based system is possible (JSON
  breakdown, version column, `price_history` table, `corrected_by` marker) but each is added after the
  incident that taught you to — "what we're building at that point is a **partial event log, decided per
  column, under time pressure.**"
- **Why the event-sourced recovery doesn't.** `RatePlanApplied` still says v4 at 180.00; the per-night
  breakdown is still beside the wrong tax. The fix is a calculation, not a reconstruction — and if the
  *correction* is wrong, attempt three is still computed from the booking, not from attempt two.
- **`buildSha` in event metadata** — the commit the service was running when it appended the event, "an
  environment variable and a few lines in whatever builds our metadata." It makes blast radius exact
  (`WHERE metadata->>'buildSha' = 'a4f9c2e'` returns the events the broken binary produced and nothing
  else); `correlationId` groups one user action and `causationId` chains back to the command. A
  [[decision-trace]] primitive, directly reusable for agent-written events.
- **Fix forward, never rewrite** — append a corrective event (`previousTotal`, `correctedTotal`,
  `reason`), rebuild read models, fix the bug. "Having precise history, bugs included, is a valid
  scenario. It's often the only way to see later what really went wrong." If a clean stream is later
  needed for a regulator, **copy and transform into a new stream and keep the original.**
- **The argument that decides it** is not about arithmetic: a front-office agent had already corrected
  one reservation by hand with a goodwill discount. A blind bulk recalculation is *correct* and **undoes a
  deliberate human decision**. With a stream you can branch on it ("skip if any price-affecting event
  follows the bad one"); **"in the mutable model, a bug and a deliberate correction look identical: a
  number in a column. There's nothing to branch on."**
- **Make correction a feature.** Ask the business "how do you fix this today?", then model it —
  `CorrectReservationPrice` with permissions, validation and a **mandatory reason** — so the bulk fix runs
  through the same command as the front desk and "nobody connects to the production database at 23:00."
  His follow-up when told something can never happen: "fine, how often?"

Keep this distinct from [[event-versioning-and-upcasting]]: that is an event's *shape* changing; this is
an event's *value* being wrong.

## Additive evolution, and the schema you cannot design up front (Fritzsche, 2026-08)

[[fritzsche-how-event-sourcing-grows-with-the-business]] inserts a fifth step (`Inspect`) into a running
four-step flow and counts the change. "For events, the schema consists of a set of event types, and that
set **only grows**": a new event type, a new function, and a change to existing capabilities **only where
the new fact is relevant to their context** — `AcquireVehicle` and `ReceiveVehicle` untouched,
`InfleetVehicle` plus one fold case and one rule, **no data migration** ("vehicles already in the fleet
simply do not have a `VehicleInspected` event"). The mechanism is the **fold** (Greg Young, 2012:
"Current State is a Left Fold of previous behaviours"): each capability derives its own state from the
events its rules read, and "events that the rules do not read are not taken into account."

His statement of why this works is the most useful sentence: "**events are additive, since no reader needs
to know the big picture. Functions remain small because they derive their specific perspective precisely
from the events.**" Contrast the entity-centred path, where "every new step is a change to a shared
structure, because the database represents a global, shared, mutable state" (Kleppmann, 2014) and
normalization "must be complete before the first record is written" (Pat Helland, 2015). He is explicit
about where cost *does* land: a new projection "is new code with its own rebuild." One authored example,
no measurement, and the favourable case is chosen.

He also draws the method/store line the page should keep: **[[event-modeling]] is a modelling discipline,
event sourcing is a storage decision** ([[fritzsche-thinking-in-events]]), and the authority test decides
which you have — "if the current tables are authoritative and events only appear in the model, logs,
messages, audit trails, or integration notifications, the system may be event-aware or event-driven, but
it is not Event Sourcing." With the symmetric warning: "an event store does not guarantee a good model…
**storing vague events only preserves the vagueness permanently.**"

## Is history the point? — three positions, unresolved

**A live disagreement about what event sourcing is *for*. The KB carries all of it; nothing below is the
wiki's settled view.**

- **[[axoniq]]** sells event sourcing *as* an audit and explainability capability in both captures, most
  fully in [[axoniq-government-ai-explainability-requirements]] (an interested party; its one number, an
  80% audit-prep reduction, is a **VENDOR SELF-REPORT** with the customer unnamed). This is the framing
  the "event store as agent memory" section above rests on, so that section and this one are in tension
  by construction.
- **[[rico-fritzsche]]** rejects that motivation outright: "anyone who thinks Event Sourcing is an audit
  feature has misunderstood its purpose… the fact that the history is preserved is a **consequence** of
  that very property, but it is not the reason for it." His stated motivation is **independent domain
  capabilities not tied to a central shared data structure**
  ([[fritzsche-event-sourcing-is-not-an-audit-feature]],
  [[fritzsche-how-event-sourcing-grows-with-the-business]]).
- **And Fritzsche is in tension with himself over time — record the hardening, do not average it.** In
  July ([[fritzsche-thinking-in-events]]) he lists **"strong auditability"** among the conditions that
  make ES compelling; by late August ([[fritzsche-event-sourcing-is-not-an-audit-feature]],
  2026-08-31) audit-motivated ES is "fundamentally wrong." He never reconciles the two, so his position
  **hardened over July–August 2026** and **no page should quote one month's framing as his settled
  view**. The July position is not superseded; it is unretracted.
- **[[yves-goeleven]]** ([[goeleven-event-sourcing-not-auditing-for-free]]) attacks from a third side:
  auditing is not something the log hands you free. So the three voices do not line up on one axis —
  AxonIQ says audit is the payoff, Fritzsche says audit is the wrong reason to want the payoff, and
  Goeleven says the payoff is not free even if you want it.
- **[[oskar-dudycz]]** adds an oblique data point: his 14-question checklist for choosing a first
  event-sourced feature ([[dudycz-checklist-first-event-sourcing-feature]]) **never asks whether you need
  a history** — it selects on decision-shape (can a command be rejected for a business reason?),
  ownership, stream lifetime, and reversibility.

**A second, separable disagreement: where do you adopt it first?** Dudycz's checklist selects for
**off the critical path**, "wrong for a day" survivable, reversible in a week, "small enough to do
slightly rogue" — i.e. **adopt where it is cheap to be wrong, and learn**. AxonIQ advises the
**opposite**: brownfield, incremental, and **start where auditability matters most**
([[axoniq-government-ai-explainability-requirements]]) — i.e. **adopt where it hurts**. AxonIQ is an
interested party (**VENDOR SELF-REPORT**) and Dudycz sells consulting on these patterns and disclaims
his own list ("that's why I don't like checklists!"), and the fuller article behind it is uncaptured.
Neither position is evidenced; the KB holds both.

## Storage does not grow forever — slice streams by lifetime (Dudycz)

[[dudycz-archiving-events-stream-lifetime-slicing]] answers the infinite-growth worry. First, often do
nothing: "event stores usually scale well with the number of streams. If they're not actively accessed
and are not long, then it's okay to keep them." Second, archiving need not be uniform — "you don't need
to have a uniform archiving strategy for all." Third, **slice streams per lifetime** ("bank account to
accounting period, point of sales to cashier shifts") and "keep just the **last summary event**, archive
the rest," so a reopening starts from the summary rather than the full history. The objection he takes
seriously is not storage but the **long legal tail** (invoice corrections, cashier-shift recalculations,
late-arriving data).

Two things to hold. **Stream lifetime is a modelling decision, not an ops setting** — the grain decides
whether archiving is ever possible. And **it directly contradicts the retain-forever framing of the audit
sources, which the KB does not resolve**: [[axoniq-government-ai-explainability-requirements]] treats
**indefinite retention as the selling point** — "institutional memory on government timescales," a
decision questioned "in a decade, by an oversight body that does not yet exist" (**VENDOR
SELF-REPORT**) — while Dudycz treats **retention as a cost to manage**, to be bounded by stream
lifetime. **So indefinite retention is not a settled property of event sourcing**, and a page or reader
that needs one has to choose on grounds neither source supplies. It also bounds
[[dudycz-fixing-bugs-in-event-sourcing]], which depends on old events still being there; he does not
draw that connection himself. (Distinct from a **snapshot**, which is a performance device leaving
history in place.) Caveats: ~300-word post, no mechanics, no cost figures, and its date is a **repost**
date at best.

_Source pages: [[eventmodeling-what-is-event-modeling]] · [[semaphore-dymitruk-event-modeling]] · [[akka-event-sourcing-backbone-agentic-ai]] · [[akka-agentic-systems-are-distributed-systems]] · [[atomicobject-cqrs-event-sourcing-production-walkthrough]] · [[event-modeling-event-sourcing-podcast]] · [[fritzsche-choosing-storage-is-choosing-what-your-system-forgets]] · [[dudycz-fixing-bugs-in-event-sourcing]] · [[fritzsche-how-event-sourcing-grows-with-the-business]] · [[fritzsche-thinking-in-events]] · [[fritzsche-event-sourcing-is-not-an-audit-feature]] · [[dudycz-archiving-events-stream-lifetime-slicing]] · [[dudycz-checklist-first-event-sourcing-feature]] · [[axoniq-government-ai-explainability-requirements]]._
