---
title: "Goeleven — Event sourcing ≠ auditing for free"
type: source
created: 2026-06-14
updated: 2026-06-14
sources: [goeleven-event-sourcing-not-auditing-for-free]
raw_file: [raw/articles/goeleven-event-sourcing-not-auditing-for-free.md]
tags: [event-sourcing, auditing, business-capabilities, focus]
---

# Goeleven — Event sourcing ≠ auditing for free

LinkedIn post by **[[yves-goeleven]]** (≈April 2026), captured in a deeper-than-14-day people backfill
(Yves posts in bursts). Raw: `raw/articles/goeleven-event-sourcing-not-auditing-for-free.md`.

## Key points

- **Myth:** event sourcing gives you auditing "for free." **Reality:** it's only a *starting point* —
  you're forced to store each decision (and related data) as an event before applying it, so every
  decision is already on a log.
- To become a real **audit log**, the decision log must be augmented with context on every event:
  **who** requested the decision, **when**, **where**, **what** the decision was, and **why** (both
  **causation and correlation**).
- If you design **around business capabilities** (as he does), each stream represents the full audit
  of the business process realizing that capability.

## Why it matters

A crisp [[event-sourcing]] clarification (event log ≠ audit log without enriched metadata) and a
window into Goeleven's **business-capability** design style — the coupling/cohesion lens (capabilities
as the unit of design/swimlane) that connects to [[event-modeling]], [[domain-driven-design]] and
[[conways-law]]. The who/when/where/what/why metadata maps onto the causation/correlation fields
event-sourced systems already carry.

## Links

Entities: [[yves-goeleven]]. Concepts: [[event-sourcing]], [[event-modeling]],
[[domain-driven-design]], [[cqrs]]. (Goeleven also has a 2023 mini-series on translating an Event
Model into code — a rich vein to ingest from his blog next.)
