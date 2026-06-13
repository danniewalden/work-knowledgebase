---
title: Autonomy Ladder
type: concept
created: 2026-06-11
updated: 2026-06-13
sources: [svitla-agentic-ai-market-trends-2026, anthropic-building-effective-agents, jwilger-agent-skills-event-modeling]
tags: [agentic-ai, framework, autonomy, maturity]
---

# Autonomy Ladder

A four-level framework (by analogy to self-driving-car levels) for how much autonomy an agent
actually has ([[svitla-agentic-ai-market-trends-2026]]):

1. **Level 1 — Chain:** rule-based automation, fixed sequence. *Where most "agents" sit today.*
2. **Level 2 — Workflow:** predefined actions, sequence chosen by logic or an LLM; steps known,
   order adapts to context.
3. **Level 3 — Partially autonomous:** plans, executes, and adjusts with minimal oversight;
   handles exceptions within guardrails.
4. **Level 4 — Fully autonomous:** sets goals, learns from outcomes, operates with little
   human input over extended periods.

Most 2026 production deployments are **Level 1–2**, while marketing implies Level 3–4 — the
disconnect behind [[agentwashing]]. The ladder is the maturity-graded version of
[[anthropic]]'s [[agent-vs-workflow]] distinction (Levels 1–2 ≈ workflows, 3–4 ≈ agents).
[[gartner]] projects ~15% of day-to-day work decisions made autonomously by 2028 (from ~zero
in 2024) — i.e. the center of gravity climbing toward Level 3.

A concrete coding-agent instance: [[john-wilger]]'s factory pipeline
([[jwilger-agent-skills-event-modeling]]) ships a **Conservative → Standard → Full** autonomy dial
(human approves every slice → human reviews batches → agent auto-merges on green gates), where the
operator climbs the ladder only as the [[event-modeling]]-derived quality gates prove out — autonomy
earned against passing tests rather than asserted.

_Source pages: [[svitla-agentic-ai-market-trends-2026]] · [[anthropic-building-effective-agents]]._
