---
title: Rico Fritzsche
type: entity
created: 2026-06-15
updated: 2026-08-03
sources: [rico-fritzsche-autonomous-domain-capabilities-ccc, fritzsche-functional-core-imperative-shell-agentic-coding, rico-fritzsche-rpu-reactor-vocabulary, rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb, fritzsche-ccc-atomic-append-serialized-write-order, fritzsche-clean-architecture-capability-over-layers, fritzsche-microservices-not-a-maturity-level, fritzsche-command-context-consistency-principle, fritzsche-who-owns-a-rule-shared-across-domain-capabilities, fritzsche-why-solid-is-outdated, fritzsche-choosing-storage-is-choosing-what-your-system-forgets, fritzsche-why-your-software-cannot-explain-business-decisions]
tags: [person, business-capabilities, vertical-slice-architecture, event-sourcing, ddd, focus]
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

> **Blog-visibility note:** ricofritzsche.me is a client-rendered Ghost site, so headless watches saw only
> a shell and reported it "evergreen"; these five in-window articles surfaced only via a live-Chrome sweep
> (2026-08-03). Worth checking his blog live in future sweeps.

_Source pages: [[rico-fritzsche-autonomous-domain-capabilities-ccc]] · [[fritzsche-functional-core-imperative-shell-agentic-coding]] · [[rico-fritzsche-rpu-reactor-vocabulary]] · [[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]] · [[fritzsche-ccc-atomic-append-serialized-write-order]] · [[fritzsche-clean-architecture-capability-over-layers]] · [[fritzsche-microservices-not-a-maturity-level]] · [[fritzsche-command-context-consistency-principle]] · [[fritzsche-who-owns-a-rule-shared-across-domain-capabilities]] · [[fritzsche-choosing-storage-is-choosing-what-your-system-forgets]] · [[fritzsche-why-your-software-cannot-explain-business-decisions]] · [[fritzsche-why-solid-is-outdated]]._
