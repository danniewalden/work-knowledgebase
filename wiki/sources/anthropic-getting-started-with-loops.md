---
title: "Anthropic — Getting Started with Loops"
type: source
created: 2026-07-10
updated: 2026-07-10
sources: [anthropic-getting-started-with-loops]
raw_file: [raw/articles/anthropic-getting-started-with-loops.md]
tags: [loop-engineering, harness-engineering, agentic-coding, unattended-coding-agents, agent-harness, focus]
---

# Anthropic — "Getting started with loops"

Source: [[anthropic]] (Claude Code team), claude.com/blog, 2026-06-30, by Delba de Oliveira & Michael
Segner. Raw: `raw/articles/anthropic-getting-started-with-loops.md`. The **vendor-canonical loop
taxonomy** — the counterpart to the Osmani / LangChain / swyx primaries already under
[[loop-engineering]].

## Summary

Opening with the observation that "if you spend some time on X trying to pin down what a loop actually
is, you'll come across multiple different answers," the Claude Code team offers a definition and a
four-type taxonomy. **A loop is an agent repeating cycles of work until a stop condition is met.** Loops
are classified along four axes — how they're **triggered**, how they're **stopped**, which Claude Code
**primitive** implements them, and which **task** each suits. The advice throughout is to *start with
the simplest solution and use these patterns selectively* — not every task needs a complex loop.

## The four loop types

1. **Turn-based loop** — *triggered by* a user prompt; *stops* when Claude judges the task done or needs
   more context; best for shorter, one-off tasks. This is the base [[react-loop|agentic loop]] (gather
   context → act → check → repeat → respond) with **you** as the checker. You improve its verification by
   **encoding your manual checks as a `SKILL.md`** so Claude can self-verify end-to-end — the more
   *quantitative* the checks (screenshots, console-error counts, performance traces), the better.
2. **Goal-based loop (`/goal`)** — *triggered* manually; *stops* when the goal is achieved **or** a turn
   cap is hit; best for tasks with **verifiable exit criteria**. Each time Claude tries to stop, a
   **separate evaluator model** checks the success condition and sends it back until met or the cap is
   reached — which is why deterministic criteria (tests passed, a score threshold) work best. Example:
   `/goal get the homepage Lighthouse score to 90 or above, stop after 5 tries.`
3. **Time-based loop (`/loop` and `/schedule`)** — *triggered* by a time interval; *stops* when you
   cancel or the work completes (PR merges, queue empties); best for recurring work or interfacing with
   external systems. `/loop 5m` re-runs a prompt on a cadence **on your machine**; `/schedule` moves the
   routine **to the cloud**.
4. **Proactive loop** — *triggered* by an event or schedule with **no human in real time**; each task
   exits when its goal is met while the routine runs until turned off; best for recurring streams of
   well-defined work (bug reports, triage, migrations, dependency upgrades). Composed from the primitives
   plus **auto mode** and **dynamic workflows** (research preview) — e.g. `/schedule` checks a channel,
   `/goal` defines done, dynamic workflows explore fixes in parallel worktrees with an adversarial judge.

## Quality & token guidance

- **Code quality is a property of the system around the loop:** keep the codebase clean (Claude copies
  existing patterns), give Claude a way to self-verify (skills), keep framework docs reachable, and use a
  **second reviewer agent with fresh context** (`/code-review`) — *less biased, not influenced by the
  main agent's reasoning* (maker≠checker). When a result misses the bar, **don't just fix the instance —
  encode the fix to improve the system for all future iterations** (the hill-climbing move).
- **Token governance:** pick the right primitive/model (cheaper/faster models for smaller tasks), set
  clear stop criteria, **pilot before large runs** (dynamic workflows can spawn hundreds of agents), use
  **scripts for deterministic work** ("running a script is cheaper than reasoning through the steps"),
  match run frequency to how often the watched thing changes, and inspect `/usage`, `/goal`, `/workflows`.

## Connections

Adds the **vendor-canonical 4-type taxonomy + primitive mapping** to [[loop-engineering]] and maps almost
one-to-one onto [[langchain-the-art-of-loop-engineering|LangChain's four stacked loops]]: Turn-based ≈
the agent loop, Goal-based ≈ the verification/grader loop (the evaluator model), Time-based/Proactive ≈
the event-driven/always-on loop, and "encode the fix to improve the system" ≈ the **hill-climbing**
loop. Co-primary with [[addyosmani-loop-engineering]] and [[swyx-loopcraft-art-of-stacking-loops]];
`SKILL.md`-as-verification echoes [[jwilger-agent-skills-event-modeling]]; proactive loops are
[[unattended-coding-agents]] / [[long-running-agents]]; the reviewer-agent split is the maker≠checker
seam. Ties to [[agent-harness]] and [[ralph-loop]] (the persistent turn-based loop).

## Caveat

A **vendor product doc** — the primitives (`/goal`, `/loop`, `/schedule`, auto mode, dynamic workflows)
are Claude Code-specific, so it is canonical for the *pattern* but framed around one product's features.
Consistent with the independent LangChain taxonomy, which is the cross-check.
