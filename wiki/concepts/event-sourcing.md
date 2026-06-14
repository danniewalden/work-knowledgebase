---
title: Event Sourcing
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [semaphore-dymitruk-event-modeling, eventmodeling-what-is-event-modeling, akka-event-sourcing-backbone-agentic-ai, akka-agentic-systems-are-distributed-systems]
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
[[business-capabilities]] · [[agentic-ai]] · [[event-sourced-agentic-patterns]] ·
[[event-driven-architecture]] · [[agentic-event-driven-systems]] ·
[[open-closed-principle]] · [[domain-driven-design]]

**Substrate note (2026-06-14):** the focus now explicitly includes the event-sourcing design
substrate around Event Modeling — see [[dynamic-consistency-boundaries]] (per-decision consistency
scopes replacing the fixed aggregate) and [[vertical-slice-architecture]] (feature-slice organization
that yields [[cqrs]] and maps to Event Modeling slices).

**Note (2026-06-12):** event sourcing is a pattern *within* the broader
[[event-driven-architecture]] family. Three external 2026 sources now apply it to agents directly:
[[confluent-agentic-event-driven-systems-architecture]] lists immutability, exactly-once, and
**deterministic replay** as production design principles for agent decisions, and
[[atlan-event-driven-architecture-for-ai-agents]] names event sourcing as a core agent-coordination
pattern — externally corroborating the Akka "backbone" thesis above. See [[agentic-event-driven-systems]].

_Source pages: [[eventmodeling-what-is-event-modeling]] · [[semaphore-dymitruk-event-modeling]] · [[akka-event-sourcing-backbone-agentic-ai]] · [[akka-agentic-systems-are-distributed-systems]]._
