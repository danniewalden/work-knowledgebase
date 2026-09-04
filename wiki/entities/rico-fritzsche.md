---
title: Rico Fritzsche
type: entity
created: 2026-06-15
updated: 2026-09-04
sources: [rico-fritzsche-autonomous-domain-capabilities-ccc, fritzsche-functional-core-imperative-shell-agentic-coding, rico-fritzsche-rpu-reactor-vocabulary, rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb, fritzsche-ccc-atomic-append-serialized-write-order, fritzsche-clean-architecture-capability-over-layers, fritzsche-microservices-not-a-maturity-level, fritzsche-command-context-consistency-principle, fritzsche-who-owns-a-rule-shared-across-domain-capabilities, fritzsche-why-solid-is-outdated, fritzsche-choosing-storage-is-choosing-what-your-system-forgets, fritzsche-why-your-software-cannot-explain-business-decisions, fritzsche-thinking-in-events, fritzsche-why-the-entity-model-is-an-illusion, fritzsche-how-event-sourcing-grows-with-the-business, fritzsche-the-entity-is-a-projection-not-a-row, fritzsche-event-sourcing-is-not-an-audit-feature, fritzsche-vsa-does-not-fix-entity-centered-thinking, fritzsche-what-ai-changes-is-which-work-stays-hard, fritzsche-dotnet-scene-stuck-in-mid-2000s]
tags: [person, business-capabilities, vertical-slice-architecture, event-sourcing, ddd, entity-centric-thinking, focus]
---

# Rico Fritzsche

Software architect and writer on domain-centric design; an active LinkedIn/Medium voice on
organizing code around **[[business-capabilities]]** in the age of AI coding agents. Added to the
`watch-config.json` people list on 2026-06-15.

## Position — Autonomous Domain Capabilities & CCC

Fritzsche argues that most architectures (layered/Clean/Hexagonal, and even
[[vertical-slice-architecture]] when it still leans on shared models/repositories/aggregates) give a
domain capability **no clear home** — and that AI agents' speed makes this weakness expensive. His
proposal ([[rico-fritzsche-autonomous-domain-capabilities-ccc]]): stop routing Commands/Queries through
a centralized object model; let each capability be a **Request Processing Unit (RPU)** that builds a
**local context from recorded events** (Command Context Consistency, CCC), decides, and emits
consequences. *Domain = recorded state + the capabilities that interpret it.* See
[[business-capabilities]] and the close kinship with [[dynamic-consistency-boundaries]].

**Update (2026-06-17, captured 06-19):** in [[rico-fritzsche-rpu-reactor-vocabulary]] he **retires
"Feature Slice"** and names the full vocabulary — **RPU** (transport-free capability unit), **Reactor**
(lightweight coordinator, *not* a saga), **Interaction / Use Case / Delivery Mechanism / Providers /
Event Store**. The companion post reframes layered architecture as **"distributed technical ownership"**
and argues the domain capability — not an object model or aggregate — must be the ownership boundary
("the problem with DDD" is putting rules in aggregates). This is the worked-out form of his CCC sketch.

**Update (2026-06-19, captured 06-21):** in
[[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]] he argues **Event Sourcing does not require
aggregates** (the aggregate-rebuild recipe is one implementation, not the definition) and locates **CCC
vs [[dynamic-consistency-boundaries|DCB]]** precisely — same rejection principle, but CCC is the
representation-agnostic *principle* and DCB a specific tag-based event-store *contract*; neither is a
synonym for Event Sourcing. Resolves the KB's standing CCC-vs-DCB open question.

**Update (2026-06-29 sweep).** Three more in-window posts captured via live Chrome:
- **CCC needs a protected write order** ([[fritzsche-ccc-atomic-append-serialized-write-order]], ~Jun-23)
  — the *implementation* layer under CCC/DCB: an atomic conditional append (PostgreSQL CTE) is **not**
  enough, because under READ COMMITTED two concurrent commands can observe the same context version and
  both append. CCC requires **serialization** (e.g. locking a single metadata row per append txn) — the
  lock is an implementation detail, the **contract** is what matters: "atomicity safeguards one append;
  serialization prevents two decisions from the same observed context being accepted."
- **Clean Architecture critique** ([[fritzsche-clean-architecture-capability-over-layers]], Jun-28) —
  Dependency Inversion changes dependency *direction* but doesn't remove *functional* dependencies; SoC
  belongs to the **domain capability**, not horizontal layers; CRUD isn't domain language; FC/IS is the
  stronger foundation. The capability-over-layers thesis aimed squarely at Clean/Hexagonal.
- **Microservices are not a maturity level** ([[fritzsche-microservices-not-a-maturity-level]], Jun-24) —
  rebuts the "modular monolith first" line (names Anton Martyniuk); microservices are a cost/purpose
  decision justified only by real **end-to-end ownership**, not team seniority. (Off the agents thread;
  captured under people *anything-substantive*.)

## Position — the entity itself is the problem (Jul–Aug 2026, six captures)

Through July–August 2026 his argument moves one level below capability ownership: not "the capability has
no home" but **"the entity was never the right unit."** Four captures argue one connected thesis, now
carried on [[entity-centric-thinking]]:

- **[[fritzsche-thinking-in-events]]** (2026-07-03) — the *mildest* of the set, and the KB's cleanest
  statement of **[[event-modeling]] ≠ [[event-sourcing]]**: one is a modelling discipline, the other a
  storage decision, and "confusing both turns a useful way of thinking into another technical
  prescription." Quotes [[adam-dymitruk]]'s "Events happen — whether we store them or not is our
  choice," insists on rigorous ubiquitous language (`ReservationUpdated` "preserves the mutation and
  loses the reason"), and warns symmetrically that "an event store does not guarantee a good model…
  **storing vague events only preserves the vagueness permanently.**" Note: here relational tables are a
  legitimate implementation of a good event model, and **auditability is listed as a reason to choose
  ES**.
- **[[fritzsche-why-the-entity-model-is-an-illusion]]** (2026-08-26) — the root article. The row "is
  actually only the result of the last write"; audit/history/status columns are workarounds for what it
  destroys; a physical thing has a **reference** in software, not an entity; the "Vehicle" is a
  **projection**, and different interests get different projections. Mutation costs two things: it
  destroys what happened, and it turns every concurrent request into a conflict.
  Companion LinkedIn post: **[[fritzsche-the-entity-is-a-projection-not-a-row]]** (the article is the
  fuller primary).
- **[[fritzsche-how-event-sourcing-grows-with-the-business]]** (2026-08-30) — the sequel and the most
  concrete piece he has published: inserts a fifth process step into a running system and counts the
  change. The **fold** per command context, "events that the rules do not read are not taken into
  account," the event-type set that only grows, and **no data migration**. Also his clearest formulation
  of why: "events are additive, since no reader needs to know the big picture."
- **[[fritzsche-vsa-does-not-fix-entity-centered-thinking]]** (2026-08-28) — the architectural corollary
  and the sharpest line: **"VSA improves locality after a team chooses a request boundary. It does not
  discover that boundary."** Noun folders + CRUD verbs are vertical *and* entity-centred; "that is an
  ownership problem"; and Clean Architecture has the same defect. **The fuller article is uncaptured**
  (linked in a LinkedIn first comment, unresolved at capture) — a named gap.
- **[[fritzsche-event-sourcing-is-not-an-audit-feature]]** (2026-08-31) — "anyone who thinks Event
  Sourcing is an audit feature has misunderstood its purpose"; history is a **consequence**, not a
  reason; the motivation is independent capabilities free of a central shared structure. "The problem
  with entity-centric thinking is **less of a technical nature.**"

### He changed his mind. Do not average the two positions into one

This page must read as a **trajectory with dates**, not as a single settled view, because within nine
weeks he argued both sides of the same question:

| Date | Capture | On audit | On the entity / relational tables |
| --- | --- | --- | --- |
| **2026-07-03** | [[fritzsche-thinking-in-events]] | **strong auditability is listed among the reasons event sourcing is compelling** | relational tables are a legitimate implementation of a good event model |
| **2026-08-26 → 08-31** | [[fritzsche-why-the-entity-model-is-an-illusion]], [[fritzsche-event-sourcing-is-not-an-audit-feature]] | **"anyone who thinks Event Sourcing is an audit feature has misunderstood its purpose"** — history is a consequence, not a reason | the row is "only the result of the last write"; the entity model is an **illusion** |

**His position hardened over July–August 2026, and he nowhere reconciles the two.** Neither month is his
settled view, so **no page may quote one month's framing as "Fritzsche's position"** — cite the date. The
July piece remains the better citation for *event modeling ≠ event sourcing*; the late-August pieces are
the better citation for the anti-entity thesis; and the audit question is one he answers differently in
each. Filed under the same hold as the KB's other same-author reversals (cf.
[[rachel-laycock|Laycock's]] two 2026 essays).

**Where he now disagrees with a KB peer.** [[oskar-dudycz]], in the same fortnight
([[dudycz-vertical-slices-ownership-and-external-dependencies]]), keeps "business logic per entity or
aggregate" as a deliberate rule while agreeing entirely on the naming half (CRUD verbs give you nothing
to slice along). Same diagnosis, opposite conclusion about where rules live.

**Evidence standing, unchanged:** position papers, LinkedIn posts and one authored vehicle-rental
example. No measurement, no case study, no counter-case. The blog-visibility note below still applies —
and all three LinkedIn captures in this batch were retrieved via **live logged-in Chrome**, with dates
accurate to the day only.

## In the KB

A fresh, independent practitioner voice on the **flagged-important** business-capabilities focus,
complementing [[yves-goeleven]] (capability swimlanes in Event Modeling) and [[ulrich-homann]] (the
seminal capability-mapping primary). Ties capability boundaries to [[event-sourcing]] and to
[[event-modeled-agent-design|agent ownership]]. Caveat: the captured source is a LinkedIn post; the
worked detail lives in an uncaptured Medium article.

## Position — repo shape over prompting (FC/IS for agents)

In [[fritzsche-functional-core-imperative-shell-agentic-coding]] (2026-04-14) he turns the capability
argument into a concrete repo recipe for coding agents: the **repository teaches the agent its
structure before the prompt does**, so reliable agent output comes from a codebase + project-level
**skill files** + review rules that make self-contained slices the default. Inside a slice he applies
**Functional Core / Imperative Shell** (pure decision core, IO-only shell), insists on
behavior-describing file names over `service/manager/repository`, and treats **cross-feature
dependencies as a structural exception**. This operationalizes [[locality-of-reference]] and sits in
the [[agent-legibility]] / [[harness-engineering]] thread.

## Position — which part of the work stays hard (2026-09)

Two LinkedIn posts on consecutive days move his argument one level up again, from code structure to
skill value — the **third** dated station on the trajectory above. The formulation worth keeping is from
the second:

> "Nothing has changed in that regard. **What AI changes is which part of that work remains difficult.**"

Around it ([[fritzsche-what-ai-changes-is-which-work-stays-hard]], 2026-09-04): implementation detail is
getting cheap, so *"people who are able to figure out what actually needs to be built will become more
important"*; the fundamentals are *"system design, reliability, data, consistency, system structure and
boundaries"*; and **"a framework isn't a foundation"** — *"if you're proficient in ASP.NET Core, Spring,
React… you're proficient in tools… and if you focus on them, then you yourself become interchangeable."*
The most checkable claim is an aside: *"thanks to AI agents, it's becoming increasingly clear that
developers often created and solved problems that had absolutely nothing to do with the domain or the
business problem"* — i.e. accidental complexity becomes visible when its production cost falls to zero. See
[[domain-discovery]].

The blunter first post ([[fritzsche-dotnet-scene-stuck-in-mid-2000s]], 2026-09-03) wraps the same point in
a complaint about .NET LinkedIn discourse, and supplies the **"bottleneck"** phrasing: *"writing code isn't
crucial for creating a usable application with business value… I think it's great that this bottleneck is
disappearing."*

**Markers: PRACTITIONER OPINION, unmeasured, and his own standing thesis winning.** Note also that
[[miller-pondering-continuous-integration-ai-world-order]] describes *verification* capacity becoming the
new bottleneck under precisely the conditions Fritzsche celebrates — he does not ask what becomes the
constraint next.

## Where he appears

- [[rico-fritzsche-autonomous-domain-capabilities-ccc]] — Autonomous Domain Capabilities & CCC (LinkedIn, 2026-06-08).
- [[fritzsche-functional-core-imperative-shell-agentic-coding]] — Functional Core / Imperative Shell for Agentic Coding (blog/Medium, 2026-04-14).
- [[rico-fritzsche-rpu-reactor-vocabulary]] — Request Processing Units & Reactors / "the domain is capabilities, not object models" (blog, 2026-06-17).
- [[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]] — "Event Sourcing does not require aggregates"; CCC vs DCB (LinkedIn, 2026-06-19; restated 06-22).
- [[fritzsche-ccc-atomic-append-serialized-write-order]] — atomic append isn't enough; CCC needs a serialized write order (LinkedIn, 2026-06-23).
- [[fritzsche-clean-architecture-capability-over-layers]] — Clean Architecture critique; capability over layers (LinkedIn, 2026-06-28).
- [[fritzsche-microservices-not-a-maturity-level]] — microservices are a decision, not a maturity level (LinkedIn, 2026-06-24).
- [[fritzsche-why-your-software-cannot-explain-business-decisions]] — make the command→context→decide→outcome path explicit via the RPU; storage is a separate decision (blog/Medium, 2026-07-23).
- [[fritzsche-command-context-consistency-principle]] — the **canonical CCC primary**: record only while the decision's facts still hold; store-agnostic (blog, 2026-07-26).
- [[fritzsche-choosing-storage-is-choosing-what-your-system-forgets]] — state/fact/event/record held apart; ES is a storage decision, "thinking in events" isn't (blog, 2026-07-29).
- [[fritzsche-who-owns-a-rule-shared-across-domain-capabilities]] — shared invariants across capabilities: one authority, many local evaluators (blog, 2026-07-30).
- [[fritzsche-why-solid-is-outdated]] — SOLID is wrong as a default checklist; agents default to it unless the repo says otherwise; CUPID (blog, 2026-08-01).
- [[fritzsche-thinking-in-events]] — event modeling ≠ event sourcing; **auditability listed as a reason to choose ES** (blog, 2026-07-03).
- [[fritzsche-why-the-entity-model-is-an-illusion]] — the row is only the last write; the entity is a projection (article, 2026-08-26).
- [[fritzsche-the-entity-is-a-projection-not-a-row]] — companion LinkedIn post to the above (2026-08-26).
- [[fritzsche-vsa-does-not-fix-entity-centered-thinking]] — VSA improves locality, it does not discover the boundary (LinkedIn, 2026-08-28); fuller article uncaptured.
- [[fritzsche-how-event-sourcing-grows-with-the-business]] — a fifth process step added to a running system, counted; no data migration (blog, 2026-08-30).
- [[fritzsche-event-sourcing-is-not-an-audit-feature]] — audit-motivated ES "has misunderstood its purpose" (LinkedIn, 2026-08-31); **reverses the July framing**.
- [[fritzsche-dotnet-scene-stuck-in-mid-2000s]] — the "bottleneck is disappearing" phrasing (LinkedIn, 2026-09-03).
- [[fritzsche-what-ai-changes-is-which-work-stays-hard]] — what AI changes is which part of the work remains difficult (LinkedIn, 2026-09-04).

> **Blog-visibility note:** ricofritzsche.me is a client-rendered Ghost site, so headless watches saw only
> a shell and reported it "evergreen"; these five in-window articles surfaced only via a live-Chrome sweep
> (2026-08-03). Worth checking his blog live in future sweeps.

_Source pages: [[rico-fritzsche-autonomous-domain-capabilities-ccc]] · [[fritzsche-functional-core-imperative-shell-agentic-coding]] · [[rico-fritzsche-rpu-reactor-vocabulary]] · [[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]] · [[fritzsche-ccc-atomic-append-serialized-write-order]] · [[fritzsche-clean-architecture-capability-over-layers]] · [[fritzsche-microservices-not-a-maturity-level]] · [[fritzsche-command-context-consistency-principle]] · [[fritzsche-who-owns-a-rule-shared-across-domain-capabilities]] · [[fritzsche-choosing-storage-is-choosing-what-your-system-forgets]] · [[fritzsche-why-your-software-cannot-explain-business-decisions]] · [[fritzsche-why-solid-is-outdated]] · [[fritzsche-thinking-in-events]] · [[fritzsche-why-the-entity-model-is-an-illusion]] · [[fritzsche-the-entity-is-a-projection-not-a-row]] · [[fritzsche-how-event-sourcing-grows-with-the-business]] · [[fritzsche-vsa-does-not-fix-entity-centered-thinking]] · [[fritzsche-event-sourcing-is-not-an-audit-feature]] · [[fritzsche-dotnet-scene-stuck-in-mid-2000s]] · [[fritzsche-what-ai-changes-is-which-work-stays-hard]]._
