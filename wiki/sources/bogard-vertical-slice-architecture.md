---
title: "Bogard — Vertical Slice Architecture"
type: source
created: 2026-06-14
updated: 2026-06-14
sources: [bogard-vertical-slice-architecture]
tags: [vertical-slice-architecture, cqrs, ddd, architecture, seed]
---

# Bogard — Vertical Slice Architecture

Origin post by **[[jimmy-bogard]]** (2018-04-19) that named
[[vertical-slice-architecture|Vertical Slice Architecture]]. Foundational seed capture for the new VSA
concept (filed after the focus broadened 2026-06-14). Raw: `raw/articles/bogard-vertical-slice-architecture.md`.

## Key points

- **Origin story.** Started a long-term project on onion architecture; cracks showed within months;
  moved to [[cqrs]] (before it had the name) and to organizing code by **vertical slices instead of
  layers** — their exclusive approach for 7-8 years since.
- **Core rule.** "**Minimize coupling between slices, and maximize coupling in a slice.**" A slice is
  a distinct request that encapsulates all concerns front-end to back; you remove the gates/barriers
  between layers and couple along the **axis of change**.
- **CQRS falls out for free.** Requests split naturally into command vs. query, so VSA "gives CQRS
  out of the gate."
- **Abstractions melt away.** No mandatory shared repositories/services/controllers; start simple
  (Transaction Script) and refactor per-slice as code smells emerge. New features mostly *add* code
  rather than changing shared code.
- **Caveat (from the author).** Assumes the team understands code smells and refactoring (Fowler/
  Kerievsky); without that discipline, the pattern isn't for you.

## Links

Entities: [[jimmy-bogard]]. Concepts: [[vertical-slice-architecture]], [[cqrs]],
[[domain-driven-design]], [[event-modeling]] (slices echo Event Modeling's vertical "slices" of a
feature). Related: [[open-closed-principle]] (new features add code).
