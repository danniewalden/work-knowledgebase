---
title: Architecture Fitness Functions
type: concept
created: 2026-06-13
updated: 2026-09-02
sources: [fowler-bockeler-harness-engineering, fowler-bockeler-maintainability-sensors, nick-tune-enforced-application-architecture-agents-humans]
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

## Pushing past the imports-and-folders limit (Tune, 2026-08)

Böckeler's caution above — that these rules "can only express what *imports, file names, and folder
structure* allow" — is the exact limit [[nick-tune]] sets out to move
([[nick-tune-enforced-application-architecture-agents-humans]]). His DSL adds two tiers above layer
rules:

- **Role-based rules.** Code carries a role annotation (`/** @riviere-role value-object */`) and import
  rules filter on **layer + role**, not layer alone. An `/adapters` folder may import from `/domain` —
  but only symbols typed `domain-port`, so business logic cannot accumulate in adapters. `/data-access`
  may import `aggregate` and `value-object` but never `domain-service`.
- **Role shape constraints.** A role's *form* is checked: his `value-object` requires a private
  constructor, a branded private member and `parse`-prefixed statics, and forbids callable data members
  and dependencies on `aggregate` or `domain-service`.

Tune's own stated mechanism is **detection at build time** — "Anything else is a hard fail of the
build," "Violations or anything outside the above rules will fail the build" — the same category as the
`dependency-cruiser` rules already on this page, applied at a finer grain. But he gives one case where
the constraint goes further and makes the wrong shape *unbuildable* rather than merely caught: *"AI
cannot implement an aggregate inside value-object because an aggregate-repository must return an
aggregate. So it wouldn't be able to load it."* Generalising that into a second theory of enforcement —
constraints that remove the shape of an error from the space of buildable programs, rather than
flagging it after the fact — is **this wiki's extension, not his claim**; he offers the single instance.
It is worth naming because it is the one place a fitness function stops being a sensor and becomes a
type.

Two honest limits. First, this is still **structural**, not semantic — it constrains the shape and
direction of code, and Böckeler's deeper point (that coupling and modularity judgment needs an
*inferential* review) survives intact. Second, the payoff is **unmeasured**: no before/after numbers,
and Rivière is Tune's own tool (**author self-report** — see his source page). He splits his own verdict
by tier, calling package/domain/layer rules indispensable for agentic work while the role tier is
unsettled — though note his full sentence, which the tidier quotation loses: *"Yeah, still playing
around with that. Come back in 6 months. I feel confident it's the right approach."* He is uncertain
about the payoff, not the direction. There is also a cost the post does not price: every annotation is
maintenance, and ADR-002 and the executable config "are kept aligned" with no mechanism named.

## Related

[[harness-engineering]] · [[agent-harness]] · [[feedforward-and-feedback-controls]] ·
[[mutation-testing]] · [[birgitta-bockeler]] · [[nick-tune]] · [[thoughtworks]] ·
[[vertical-slice-architecture]] · [[model-as-code-vs-model-as-language]] · [[adr]]

_Sources: [[fowler-bockeler-harness-engineering]] · [[fowler-bockeler-maintainability-sensors]] ·
[[nick-tune-enforced-application-architecture-agents-humans]]._
