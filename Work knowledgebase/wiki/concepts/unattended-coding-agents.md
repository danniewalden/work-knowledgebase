---
title: Unattended Coding Agents
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [stripe-minions-one-shot-coding-agents, hashimoto-my-ai-adoption-journey, openai-harness-engineering-codex]
tags: [harness-engineering, coding-agents, autonomy, workflow]
---

# Unattended Coding Agents

Coding agents that run **without a human in the loop during execution** — kicked off with a task,
then left to plan, code, test, and open a pull request on their own. They sit at the high end of the
[[autonomy-ladder]] and are the practical payoff of good [[harness-engineering]]: an agent can only
be trusted to run unattended if the harness reliably catches its mistakes.

## Two scales, same idea

- **Enterprise / at scale:** [[stripe]]'s **minions** ([[stripe-minions-one-shot-coding-agents]]) are
  built to **one-shot** tasks — start from a Slack message, end at a CI-passing PR, 1,000+ merged per
  week with no human-written code. Parallelized across isolated devboxes; especially useful during
  on-call. [[openai-harness-engineering-codex]] is the same pattern taken to a whole product.
- **Individual developer:** [[mitchell-hashimoto]] ([[hashimoto-my-ai-adoption-journey]]) runs
  background/"end-of-day" agents and aims to "always have an agent running," but deliberately keeps to
  *one* agent and report-only triage — a deliberately modest, human-in-control version.

## What makes it work

A constrained, well-instrumented environment: deterministic steps interleaved with the agent loop,
**self-verification** ([[anthropic-effective-harnesses-long-running-agents]]), and **shift-left
feedback** — fast computational sensors run as early as possible
([[feedforward-and-feedback-controls]]). The recurring constraint is **human attention**: unattended
agents exist to parallelize work without spending the scarce resource of developer focus. A shared
discipline across sources — control *when* you check on the agent; don't let it interrupt you
(Hashimoto: turn off notifications).

_Sources: [[stripe-minions-one-shot-coding-agents]] · [[hashimoto-my-ai-adoption-journey]] · [[openai-harness-engineering-codex]]._
