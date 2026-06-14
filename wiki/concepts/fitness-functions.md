---
title: Architecture Fitness Functions
type: concept
created: 2026-06-13
updated: 2026-06-14
sources: [fowler-bockeler-harness-engineering, fowler-bockeler-maintainability-sensors]
tags: [software-architecture, harness-engineering, controls]
---

# Architecture Fitness Functions

An **architecture fitness function** is an automated check that objectively measures whether
a system still satisfies an architectural characteristic — dependency direction, layering,
coupling limits, performance budgets, and so on. The term comes from evolutionary architecture
(Ford, Parsons, Kua): rather than relying on review to catch architectural drift, you encode
the desired property as a test that fails when the property is violated.

## Why it matters in this wiki

In [[birgitta-bockeler]]'s harness-engineering mental model
([[fowler-bockeler-harness-engineering]]), fitness functions are one of **three regulation
categories** an [[agent-harness]] can apply, ranked by difficulty:

- **maintainability harness** — easiest, mostly existing tooling (linters, formatters, tests);
- **architecture fitness harness** — fitness functions, this page;
- **behaviour harness** — hardest and still largely unsolved (too much faith is placed in
  AI-generated tests).

Fitness functions matter for agents because they are a **computational sensor** in the
[[feedforward-and-feedback-controls]] sense: a deterministic, automated feedback signal that
tells the agent (or the steering human) when generated code has broken an architectural
invariant. They embody the "enforce invariants, not implementations" stance of
[[harness-engineering]] and the "keep quality left" principle — catching drift early and cheaply
rather than at review time.

[[fowler-bockeler-maintainability-sensors|Böckeler's field report]] shows a fitness function working
as a *live sensor*: `dependency-cruiser` rules that enforce a routes → services → clients + domain
layering, which the agent violated a few times and then self-corrected on. The same report cautions
that such rules can only express what *imports, file names, and folder structure* allow — deeper
coupling/modularity judgment needs an **inferential** review, not a computational fitness function.
For *test*-quality (the behaviour category) the analogous check is [[mutation-testing]].

## Related

[[harness-engineering]] · [[agent-harness]] · [[feedforward-and-feedback-controls]] · [[mutation-testing]] · [[birgitta-bockeler]] · [[thoughtworks]]

_Sources: [[fowler-bockeler-harness-engineering]] · [[fowler-bockeler-maintainability-sensors]]._
