---
title: Zalando
type: entity
created: 2026-09-04
updated: 2026-09-04
sources: [zalando-agentic-engineering-snapshot]
tags: [org, agentic-coding, agent-governance, em-standardization-foundation]
---

# Zalando

European fashion retailer with **more than 250 engineering teams**. In the KB it is the **second
non-vendor production-scale account** of agentic engineering after
[[stripe-minions-one-shot-coding-agents|Stripe's minions]], and the **first about organization rather
than tooling** ([[zalando-agentic-engineering-snapshot]]).

## Positions worth recording

- **Deliberate non-convergence** — it is *"way too early"* to standardise on one agent or workflow.
- **No central tool mandate**; teams choose.
- **An LLM proxy from day one** (Jan 2024) — the governance primitive that made everything else
  observable.
- **A risk-based PR approval bot** — low-risk PRs auto-approved; see [[autonomy-ladder]].
- *"Using coding agents usually inhibits learning"* — stated plainly by a company deploying them at
  scale.

## Its figures, and why the KB refuses them

- *"33% of our PRs are low-risk and are auto-approved"* and *"reduced PR lead time by 20–40%"* are
  **VENDOR SELF-REPORT** — Zalando on Zalando's own bot. The lead-time figure is stated *"compared with
  all PRs"*, which is a **selection-biased comparison**: low-risk PRs would merge faster anyway, so the
  delta is not attributable to the bot from what is published.
- The CCN / PR-size / commit-message **inflection points** come from **four codebases with no control
  arm**, with agent adoption partly *inferred* from inconsistent `Co-authored-by` markers, and **all four
  figures are untranscribed images**. Illustrative, not causal — as the author presents them.
- [[martin-fowler]] repeating the 20–40% figure in [[fowler-fragments-2026-08-24]] **adds no
  independence and is not a second source for it.**

## Related

[[agentic-coding]] · [[agent-governance]] · [[autonomy-ladder]] · [[software-factory]] ·
[[em-standardization-foundation]] · [[comprehension-debt]]

_Source pages: [[zalando-agentic-engineering-snapshot]]._
