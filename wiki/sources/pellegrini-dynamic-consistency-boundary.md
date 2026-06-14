---
title: "Pellegrini — A name for an idea: Dynamic Consistency Boundary"
type: source
created: 2026-06-14
updated: 2026-06-14
sources: [pellegrini-dynamic-consistency-boundary]
tags: [event-sourcing, dcb, ddd, consistency, seed]
---

# Pellegrini — A name for an idea: Dynamic Consistency Boundary

Origin post by **[[sara-pellegrini]]** (2023-05-15, Event Thinking blog) that *named* the
[[dynamic-consistency-boundaries|Dynamic Consistency Boundary]] concept, growing out of her "Kill
Aggregate" series (Apr 2023). Foundational seed capture for the new DCB concept (filed after the focus
broadened 2026-06-14), not a recent watch item. Raw: `raw/articles/pellegrini-dynamic-consistency-boundary.md`.

## Key points

- **DCB = an optimistic lock specific to event-sourced systems.** A decision is a function: input =
  an ordered stream of relevant past events (the "given"); output = a new ordered stream of events
  (the consequence).
- **The consistency rule:** append the output stream *if and only if* the relevant input stream is
  unchanged at append time vs. load time — i.e. nothing relevant happened in between. The component
  that loads the decision-relevant stream is also responsible for the conditional append.
- **What the event store must provide:** (1) *dynamic query* — read an event stream by criteria;
  (2) *conditional append* — write only if the query result still matches. Immutability makes the
  conditional append cheap (checking the last event suffices).
- **Why it matters / the "Kill Aggregate" thesis:** consistency boundaries are defined *at runtime
  per decision* rather than baked into rigid aggregates up front — removing the aggregate as the
  mandatory consistency unit.

## Links

Entities: [[sara-pellegrini]]. Concepts: [[dynamic-consistency-boundaries]], [[event-sourcing]],
[[cqrs]], [[domain-driven-design]], [[event-storming]]. Related: [[adam-dymitruk]] (also associated
with the DCB idea), [[event-modeling]].
