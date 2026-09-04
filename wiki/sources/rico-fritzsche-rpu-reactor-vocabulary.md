---
title: "Rico Fritzsche — Request Processing Units & Reactors (the RPU vocabulary)"
type: source
created: 2026-06-19
updated: 2026-06-19
sources: [rico-fritzsche-rpu-reactor-vocabulary]
raw_file: [raw/articles/rico-fritzsche-request-processing-units-and-reactors.md, raw/articles/rico-fritzsche-domain-defined-by-capabilities-not-object-models.md]
tags: [business-capabilities, vertical-slice-architecture, event-sourcing, agentic-coding, ddd, focus]
---

# Rico Fritzsche — Request Processing Units & Reactors (the RPU vocabulary)

Two companion blog posts by **[[rico-fritzsche]]**, both published 2026-06-17 on ricofritzsche.me
(cross-posted to Level Up Coding / gitconnected), captured verbatim. Together they **rename and
sharpen** the Autonomous Domain Capabilities / CCC idea from
[[rico-fritzsche-autonomous-domain-capabilities-ccc]] (2026-06-08) — this is the "worked detail" that
page flagged as still-uncaptured.

- Source file 1: `raw/articles/rico-fritzsche-request-processing-units-and-reactors.md`
- Source file 2: `raw/articles/rico-fritzsche-domain-defined-by-capabilities-not-object-models.md`

## Part 1 — "Request Processing Units and Reactors" (terminology overhaul)

Fritzsche **retires the term "Feature Slice."** A "feature" can mean anything and a "slice" describes
*shape, not responsibility*; the word never named the actual architectural unit. The architecture is now
built around a precise vocabulary that names **responsibilities**:

- **RPU (Request Processing Unit)** — atomic, self-contained unit implementing exactly **one** internal
  domain capability = one domain request (a Command **or** a Query). It owns the full processing:
  load relevant facts, build context, evaluate rules, generate result/consequences, run the imperative
  shell around the pure decision core. **Reversal of his earlier stance:** an RPU is *not* an external
  interface and should **not** contain transport (HTTP) — "an RPU is not an external interface, it is an
  internal processing unit of the domain." Duplication between RPUs is accepted on purpose (independence
  > DRY); RPUs don't depend on or reuse each other.
- **Reactor** — *optional, lightweight* coordinator introduced only when one Interaction needs several
  RPUs/Providers together. It coordinates the system's response; it **does not own** the participating
  RPUs' domain decisions. Explicitly **not** an event handler, subscriber, projection, saga, or process
  manager — it does not react to recorded facts after the fact.
- **Interaction** — the user-facing process from external trigger to returned output; fulfilled by one
  RPU or by several coordinated by a Reactor.
- **Use Case** — higher-level stakeholder description; contains one or more Interactions.
- **Delivery Mechanism** — thin translation layer (HTTP, CLI) converting external requests into
  RPU/Reactor commands and back. A `RegisterToolHttpHandler` belongs only to the `register_tool`
  capability, not to a shared `ToolController`.
- **Providers** — infrastructure (DB, ID generators, blob storage, external APIs), always **injected**
  from outside, never living inside an RPU.
- **Application State (Event Store)** — the single source of truth; the immutable event/fact sequence
  all RPUs read context from and Command RPUs append to.

The recommended repo layout makes this visible: `rpunits/<capability>/` (with `load_context`,
`build_context`, `generate_consequences` = pure functional core, `append_consequences`, `process_request`
= imperative shell), `reactors/` (only when needed), `http/` (one delivery mechanism), `events/`,
`store.rs`, `providers/`. Worked example: a `prepare_tool_rental` **Reactor** sequencing `register_tool`
then `check_out_tool` RPUs — each RPU still owns its own decision.

## Part 2 — "Why the Domain Is Defined by Domain Capabilities, Not Object Models"

The deeper argument behind the rename:

- **Layered architecture = "distributed technical ownership."** Controllers/services/repositories/
  entities/mappers each own *part* of a capability, so one capability is physically fragmented across the
  system and must be reconstructed by traversing technical boundaries. The real cost isn't indirection —
  it's **coordination pressure**: every new capability integrates into shared abstractions/repos/entity
  models, which become bottlenecks because independent capabilities are forced to evolve together.
- **VSA only moves partway.** [[vertical-slice-architecture]] packages by feature, but the architectural
  center is often *still* shared internal ownership structures under the slice — so the capability
  remains structurally distributed even when the packaging looks vertical.
- **The capability itself should be the ownership boundary.** An RPU applies a **localized Functional
  Core / Imperative Shell** internally, so technical separation lives *inside* the capability rather than
  *globally* across layers. Delivery Mechanisms, Reactors, and Providers **connect/coordinate/translate
  but never absorb the domain decision** — they're peripheral to an already-complete capability, which is
  why they are *not* layers.
- **User interaction ≠ domain capability.** A pointed distinction: a user interaction is external
  (transport, UX, workflow); a domain capability is one autonomous business-decision boundary. Conflating
  them is what spawns oversized handlers / application services / aggregate-orchestration layers. They
  also **evolve for different reasons** (a frontend can change completely while the capability is stable),
  so separating them stops external structures from becoming the domain's ownership model.
- **The DDD jab:** "all business rules are encapsulated within the domain as a whole — **not in
  aggregates, but in the domain. That is precisely where the problem with Domain-Driven Design lies.**"
  The domain behaves as a deterministic **functional core** over immutable facts; systems then grow
  **additively** (new capabilities as independent units) instead of by extending shared behavioral
  centers.

## Why it matters here

This supersedes the LinkedIn-length sketch in
[[rico-fritzsche-autonomous-domain-capabilities-ccc]] with a named, structured vocabulary and a clear
project layout — the strongest statement in the KB of *capability-as-the-ownership-boundary* for the
agent era. Notable shifts vs. the earlier capture: (1) **"Feature Slice" is explicitly abandoned**, which
matters for [[vertical-slice-architecture]] framing; (2) the RPU is now **transport-free** (HTTP pushed
out to the Delivery Mechanism), a reversal of his earlier "a slice contains everything incl. HTTP" view;
(3) the **interaction vs capability** split and **Reactor-is-not-a-saga** clarification are new precision.
The RPU remains a capability-scoped, [[event-sourcing|event-sourced]] unit with no shared object model —
a natural [[event-modeled-agent-design|agent-ownership]] boundary, parallel to
[[dynamic-consistency-boundaries|DCB]] and a sharper sibling of [[yves-goeleven]]'s capability swimlanes.
The internal FC/IS shape connects to [[fritzsche-functional-core-imperative-shell-agentic-coding]] and
[[locality-of-reference]].

## Caveats

Still one author's coinage (RPU/Reactor/CCC) without independent adoption yet — assertion-level, but now
fully worked rather than a teaser. Examples are in Rust; the pattern is language-agnostic. The DDD
critique ("the problem with DDD") is a deliberately provocative framing of an aggregate-vs-capability
debate, not a settled consensus.

## Touches

[[rico-fritzsche]] · [[autonomous-domain-capabilities]] · [[business-capabilities]] ·
[[vertical-slice-architecture]] · [[event-sourcing]] · [[dynamic-consistency-boundaries]] ·
[[locality-of-reference]] · [[agentic-coding]] · [[event-modeled-agent-design]] · [[domain-driven-design]] · [[cqrs]]

_Sources: `raw/articles/rico-fritzsche-request-processing-units-and-reactors.md` ·
`raw/articles/rico-fritzsche-domain-defined-by-capabilities-not-object-models.md`._
