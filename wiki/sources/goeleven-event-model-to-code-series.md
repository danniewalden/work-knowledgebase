---
title: "Goeleven — Translating an Event Model into code (series)"
type: source
created: 2026-06-14
updated: 2026-06-14
sources: [goeleven-event-modeling-visualize-business-processes, goeleven-interaction-design-aggregate-outbox-projection, goeleven-event-model-to-code-projection]
tags: [event-modeling, event-sourcing, cqrs, business-capabilities, coupling-cohesion, focus]
---

# Goeleven — Translating an Event Model into code (series)

A 2023 LinkedIn mini-series by **[[yves-goeleven]]** on how he turns an [[event-modeling|Event Model]]
into working [[event-sourcing|event-sourced]] code, organized around **business capabilities**.
Captured 2026-06-14 (three posts) as the richer-than-LinkedIn-feed deep backfill Dannie asked for.
Raw: `goeleven-event-modeling-visualize-business-processes`,
`goeleven-interaction-design-aggregate-outbox-projection`, `goeleven-event-model-to-code-projection`.

## The model (what an Event Model *is*, to Goeleven)

Event Modeling visualizes **business processes — even manual ones** — not "how event-sourced software
works." Top swimlanes = **roles** and their interaction points (screens, but also paper, PDFs, cash,
Excel). Bottom swimlanes = **business capabilities**, the long-term-stable boundaries within which part
of the process runs. **Decisions become events** recorded in the capability swimlane — even decisions
taken "in the mind of an authorized person"; ownership belongs to the capability, not the individual.
Between lanes: humans send **intent = commands** (a paper PO and an HTTP POST are equivalent), and the
org reports back **state = read models** derived from those same decisions. (The "big black dot"
notation = state that must be **rebuilt from the complete history**, not just the last event.)

## The code (the translation patterns)

- **Write side — Event Sourced Aggregate Root:** decides how to respond to a command, captures
  decisions as events, written atomically (entity-group transaction). Fronted by an HTTP API consumed
  by the capability's UI.
- **Outbox:** a pump that forwards stored events (batched) to a broker (Azure Service Bus topic),
  tracking its read position; retries guarantee **at-least-once** delivery.
- **Atomic message processing (MessageHandler):** a handler does receive+send atomically with room for
  exactly one more write; failures abandon-and-retry.
- **Read side — Event Sourced Projection:** rolls a stream of events up into one or more **state
  objects** for people. Often run *in-process in the query handler* when the reader is the same person
  who just issued the command. The same event stream can be shaped into a PO, receipt, sales order,
  list, notification — "whatever shapes the users have in mind, now and in the future." Attach many
  projections in parallel for **polyglot persistence**.

## Why it matters

This is a concrete **Event-Model → code** mapping from a practitioner: command→aggregate(decision)→
events→outbox→projection→read model — i.e. the [[event-modeling]] building blocks rendered as
[[cqrs]]/[[event-sourcing]] code. It directly supports [[event-modeled-agent-design]]: it shows what
"implement a slice" actually *is* (the unit an agent would generate — cf.
[[jwilger-agent-skills-event-modeling]], [[dilger-model-is-a-living-spec-always-on-agent]]). It also
carries a sharp **coupling/cohesion** lesson (via a Dragan Stepanović exchange): a bounded context's
internal events should not double as integration events, or you couple contexts as tightly as a shared
database — **a contract between capabilities is required** (relates to [[domain-driven-design]],
[[conways-law]], [[open-closed-principle]]).

## Caveats

LinkedIn posts (2023), .NET/Azure-specific tooling (his MessageHandler); the series has more parts than
the three captured here. Practitioner assertion, not a controlled study.

## Links

Entities: [[yves-goeleven]], [[adam-dymitruk]]. Concepts: [[event-modeling]], [[event-sourcing]],
[[cqrs]], [[event-modeled-agent-design]], [[domain-driven-design]], [[vertical-slice-architecture]]
(a slice ≈ command→events→projection path). Related: [[goeleven-event-sourcing-not-auditing-for-free]],
[[qlerify-event-modeling-tool-ai]], [[eventmodeling-what-is-event-modeling]].
