---
title: "Source: Dymitruk — Event Modeling: What is it?"
type: source
created: 2026-06-11
updated: 2026-06-11
sources: [eventmodeling-what-is-event-modeling]
tags: [event-modeling, event-sourcing, methodology, ddd, software-design]
---

# Source: Dymitruk — Event Modeling: What is it?

**Raw file:** `raw/articles/eventmodeling-what-is-event-modeling.md`
**Origin:** [eventmodeling.org/posts/what-is-event-modeling](https://eventmodeling.org/posts/what-is-event-modeling/)
**Author:** [[adam-dymitruk]] · **Published:** 2019-06-23 (periodically updated)

## Summary

The canonical introduction to [[event-modeling]], the method [[adam-dymitruk]] developed
at [[adaptech-group]]. It argues that cheap storage means information systems no longer
need to throw history away (the constraint that shaped RDBMS thinking), so we can model a
system as a **timeline of events** — a blueprint read like a story — instead of as current
state. The method is deliberately tiny: **3 building blocks, 4 patterns, 2 ideas**, run as
a **7-step workshop**.

## Key points

- **The blueprint** follows every field from UI → storage → back to a screen/report, on a
  single timeline with no branching. Built with sticky notes on a (often virtual) whiteboard.
- **3 building blocks:** *events* (state-changing facts on the timeline), *commands*
  (a user's intention to change state), *views / read models* (how the system informs the
  user; passive — can't reject a stored event). Wireframes sit across the top in **swimlanes**.
- **4 patterns:** command, view, plus two integration patterns — *translation* (turn external
  data into locally meaningful events) and *automation* (a "todo list" a processor works
  through to call external systems). Specs are written **Given-When-Then**, one per step.
- **7 steps:** brainstorm events → plot the timeline → storyboard (wireframes) → identify
  inputs (commands) → identify outputs (views) → apply [[conways-law|Conway's Law]] (swimlanes)
  → elaborate scenarios. Ends with a **completeness check**: every field has an origin and
  destination.
- **Flat cost curve** is the headline benefit: each workflow step is isolated by explicit
  contracts, so feature cost doesn't rise as the system grows — turning software back into an
  engineering practice (build features in any order, estimate empirically, even fixed-price).
- Also covers **security** (shows where/when sensitive data crosses boundaries) and **legacy
  systems** (freeze the old system; add a side-car using the translate pattern + a Y-valve).
- Pairs naturally with [[event-sourcing]]; evolved from [[event-storming]] and builds on
  [[greg-young]]'s CQRS/ES long-running process specs.

## Touches

[[adam-dymitruk]] · [[adaptech-group]] · [[event-modeling]] · [[event-sourcing]] ·
[[event-storming]] · [[cqrs]] · [[domain-driven-design]] · [[greg-young]] · [[alberto-brandolini]]
