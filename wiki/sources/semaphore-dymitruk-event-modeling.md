---
title: "Source: Semaphore — Dymitruk on Event Modeling"
type: source
created: 2026-06-11
updated: 2026-06-11
sources: [semaphore-dymitruk-event-modeling]
raw_file: [raw/articles/semaphore-dymitruk-event-modeling.md]
tags: [event-modeling, event-sourcing, ddd, open-closed-principle, interview]
---

# Source: Semaphore — Dymitruk on Event Modeling

**Raw file:** `raw/articles/semaphore-dymitruk-event-modeling.md`
**Origin:** [semaphore.io/blog/adam-dymitruk-event-modeling](https://semaphore.io/blog/adam-dymitruk-event-modeling)
**Author:** Darko Fabijan (Semaphore), interviewing [[adam-dymitruk]] · **Published:** 2022-08 (updated 2024-09)

## Summary

An interview that situates [[event-modeling]] relative to neighbouring practices:
[[event-storming]] (its origin), [[domain-driven-design]], the [[open-closed-principle]],
and [[event-sourcing]]. The throughline is that modelling a system as a timeline of events
gives the **visibility** needed to scope, price (even fixed-price), and onboard against,
without anyone getting "distracted by the technicals."

## Key points

- Event modeling = a **storyboard / "captured screencast" of someone using the system you
  intend to build**; describes systems by their event timeline, not their current state.
- Enables **fixed-price delivery**: counting state changes and projections exposes why a
  feature costs what it does. Reinforces the flat-cost-curve claim in [[eventmodeling-what-is-event-modeling]].
- **DDD:** use **swimlanes** to separate physical systems / logical subsystems while keeping
  each area's subject-matter language consistent.
- **Open/Closed Principle:** treat each state transition as independently extendable — even
  "a function written entirely in a different language" (e.g. serverless), mixing technologies.
- **[[event-sourcing]]:** an append-only ledger — "no erasers allowed," like accounting.
  Changing state = appending one event, with no "downhill effect" on other queries. ~80% of
  the work is the same as any UI-on-a-model app; the only addition is an event store
  (ordered, guaranteed-replay log).
- **Vertical slicing** + copy-an-existing-slice is how newcomers ship fast ("up and running
  within an hour or two").

## Touches

[[adam-dymitruk]] · [[adaptech-group]] · [[event-modeling]] · [[event-sourcing]] ·
[[event-storming]] · [[domain-driven-design]] · [[cqrs]]
