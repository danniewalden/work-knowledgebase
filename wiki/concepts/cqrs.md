---
title: CQRS (Command Query Responsibility Segregation)
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [eventmodeling-what-is-event-modeling, akka-event-sourcing-backbone-agentic-ai]
tags: [cqrs, pattern, event-sourcing, architecture]
---

# CQRS (Command Query Responsibility Segregation)

An architectural pattern that **separates the write model (commands) from the read model
(queries/views)** instead of using one model for both. Closely associated with
[[greg-young]] and frequently paired with [[event-sourcing]] (the "CQRS/ES" lineage).

## Relevance to this KB

- [[event-modeling]]'s two core building blocks — **commands** (write/intent) and **views /
  read models** (read) — are CQRS made visual on the blueprint. Dymitruk built event
  modeling partly on Greg Young's CQRS/ES long-running process specifications.
- The read/write separation is also why [[kevin-hoffman]] calls agentic systems a "perfect
  match" for event sourcing — their distributed architecture already separates these models
  ([[akka-event-sourcing-backbone-agentic-ai]]).

## Related

[[event-sourcing]] · [[event-modeling]] · [[vertical-slice-architecture]] (organizing by feature
slice "gives CQRS out of the gate" — [[jimmy-bogard]]) · [[dynamic-consistency-boundaries]] ·
[[greg-young]] · [[domain-driven-design]]

_Source pages: [[eventmodeling-what-is-event-modeling]] · [[akka-event-sourcing-backbone-agentic-ai]]._
