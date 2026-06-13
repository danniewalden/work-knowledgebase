---
title: Agentic Coding
type: concept
created: 2026-06-11
updated: 2026-06-13
sources: [anthropic-building-effective-agents, langchain-state-of-agent-engineering-2026, svitla-agentic-ai-market-trends-2026, jwilger-agent-skills-event-modeling]
tags: [agentic-ai, use-case, software-development, coding]
---

# Agentic Coding

Software development is one of [[anthropic]]'s two showcase agent domains and, per
[[langchain-state-of-agent-engineering-2026]], the **most-used agent type in daily
workflows**. Coding is a strong fit because solutions are **verifiable through automated
tests**, agents can iterate using test results as feedback, the problem space is structured,
and output quality is objectively measurable. Anthropic's coding agents resolve real GitHub
issues on **SWE-bench Verified** from the PR description alone — though human review remains
crucial.

## State of play

- Daily-driver tools named by practitioners: **Claude Code, Cursor, GitHub Copilot, Amazon
  Q, Windsurf, Antigravity** ([[langchain-state-of-agent-engineering-2026]]).
- GitHub Copilot reportedly generates ~41% of code where used; [[gartner]] forecasts ~75% of
  developers using AI coding agents by 2028 (vs <10% in 2023).
- The shift is from autocomplete → agents that **plan, execute, test, and iterate** with
  minimal guidance.

## Caution

Letting agents commit/deploy without review amplifies quality risk — one cited report finds
AI-written code carries ~1.7× the issue rate and ~45% security-flaw rate, and agents tend to
avoid refactoring ([[svitla-agentic-ai-market-trends-2026]]). Reinforces the
[[agent-observability-and-evals]] and [[agent-governance]] themes.

## Building trust: harness engineering

The emerging answer to that risk is **[[harness-engineering]]** — wrapping the coding agent in
guides and sensors ([[feedforward-and-feedback-controls]]) that raise first-try quality and let it
self-correct before code reaches human review. See [[openai-harness-engineering-codex]] (zero
hand-written code at scale), [[anthropic-effective-harnesses-long-running-agents]]
([[long-running-agents]] across context windows), and [[fowler-bockeler-harness-engineering]]
(the user-side mental model).

The frontier of this use case is **[[unattended-coding-agents]]** — agents that run with no human in
the loop until a PR is ready. [[stripe-minions-one-shot-coding-agents|Stripe's minions]] merge 1,000+
such PRs/week; [[mitchell-hashimoto]] documents the individual-developer version (background and
"always-running" agents).

A complementary thread is **spec-driven** agentic coding: rather than prompting freely, the human
first produces a specification the agent builds against. [[john-wilger]]'s `agent-skills`
([[jwilger-agent-skills-event-modeling]]) uses [[event-modeling]] for that spec — vertical slices and
Given-When-Then scenarios become TDD acceptance gates in an autonomous factory pipeline — directly
linking [[agentic-coding]] to [[event-modeled-agent-design]].

_Source pages: [[anthropic-building-effective-agents]] · [[langchain-state-of-agent-engineering-2026]] · [[svitla-agentic-ai-market-trends-2026]]._
