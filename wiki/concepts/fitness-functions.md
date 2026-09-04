---
title: Architecture Fitness Functions
type: concept
created: 2026-06-13
updated: 2026-09-04
sources: [fowler-bockeler-harness-engineering, fowler-bockeler-maintainability-sensors, nick-tune-enforced-application-architecture-agents-humans, laycock-maybe-we-shouldnt-be-reviewing-all-this-code, addyosmani-agentic-code-quality, addyosmani-human-judgment-relocates]
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

## What they are *for* when nobody reads every diff (Laycock, 2026-09)

[[rachel-laycock]] gives the purpose statement this page implies but never states
([[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]]). Her argument is that code review has been
carrying six jobs at once — "quality gate, security check, architecture review, mentoring mechanism,
knowledge-sharing system, ownership model" — and that agent output volume breaks the arrangement. Each
job then moves to where it belongs, and fitness functions get one specific job: *"If we want
**architectural alignment**, design together… and then **encode the important constraints as fitness
functions**."* Everything deterministic (formatting, linting, known security problems) is automated
outright — "we really shouldn't still be arguing about whitespace in 2026" — and what is left for humans
is **review by exception**.

So on her account a fitness function is not a supplement to review but the **mechanism that carries
architectural intent forward when per-diff human inspection stops being the gate**. That is the same
role [[nick-tune]] builds machinery for above (make the violation fail the build) and the same role
[[adam-tornhill]] assigns to deterministic checks in [[tornhill-controlling-the-uncertainty-machine]]
("enforce what you don't inspect" — **VENDOR SELF-REPORT**, his stack includes CodeScene's own MCP).
It is also, as she says, useless against the classes of problem
[[fowler-bockeler-maintainability-sensors|Böckeler]] identifies and against
[[willison-conceptual-integrity-and-counting-lines-of-code|conceptual-integrity drift]], where each
individual change is defensible and the whole stops cohering — which is why her list keeps humans for
"a change with a huge blast radius" and for "simply something where the team says, 'I'm not confident
about this.'" **NOT INDEPENDENT**: Thoughtworks' CTO on martinfowler.com prescribing a
Thoughtworks-originated practice, with no data. See [[verification-burden]].

## Prose is not a constraint — three sources agree ([[addyosmani-agentic-code-quality|Osmani, 2026-08]])

If Laycock says *what* a fitness function is now for, this says *why prose cannot do the job instead*.
*"Folks can define their own constraints too, including **architecture rules that linting tools like
ESLint can enforce**. Many of these tools have built-in hooks that can be used to pull in agents, or
humans, when things break."* Same move as
[[nick-tune-enforced-application-architecture-agents-humans|Tune's enforced application architecture]] and
[[dilger-keep-command-handlers-pure|Dilger's]] finding that *"a written skill had to be **enforced**, not
just stated"* — **architectural intent expressed as prose does not survive contact with an agent, and must
be expressed as a failing check.**

Osmani's addition to that argument is the **portfolio** view: quality is *"a collection of signals of
varying importance to you and your team"* spanning correctness, maintainability, performance, security,
efficiency and **comprehensibility** — and *"while it matters how many constraints we have in place, it
matters more **whether they're challenging enough** to meet our bar."* The complements are the two rules
now filed under [[software-factory]] and [[feedforward-and-feedback-controls]]: **"number of checks !=
quality"**, and the **verification budget** — fast deterministic checks (lint, type checking) early;
heavy-but-valuable ones (full suite, [[mutation-testing]], browser testing, security scans) at or after
the draft-PR gate, *"budget[ed] for them in the right places because you don't want to slow down your
development loop."*

## Related

[[harness-engineering]] · [[agent-harness]] · [[feedforward-and-feedback-controls]] ·
[[mutation-testing]] · [[birgitta-bockeler]] · [[nick-tune]] · [[thoughtworks]] ·
[[vertical-slice-architecture]] · [[model-as-code-vs-model-as-language]] · [[adr]] ·
[[verification-burden]] · [[rachel-laycock]] · [[addy-osmani]]

_Sources: [[fowler-bockeler-harness-engineering]] · [[fowler-bockeler-maintainability-sensors]] ·
[[nick-tune-enforced-application-architecture-agents-humans]] ·
[[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]] · [[addyosmani-agentic-code-quality]] ·
[[addyosmani-human-judgment-relocates]]._
