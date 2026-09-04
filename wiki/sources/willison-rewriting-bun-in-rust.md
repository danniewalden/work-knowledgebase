---
title: "Willison — Rewriting Bun in Rust (agentic case study)"
type: source
created: 2026-07-10
updated: 2026-07-10
sources: [willison-rewriting-bun-in-rust]
raw_file: [raw/articles/willison-rewriting-bun-in-rust.md]
tags: [loop-engineering, agentic-coding, unattended-coding-agents, agent-harness, conformance-suite, focus]
---

# Willison — "Rewriting Bun in Rust"

Source: [[simon-willison]], link-blog, Simon Willison's Weblog, 2026-07-08. Raw:
`raw/articles/willison-rewriting-bun-in-rust.md`. Willison's commentary on Jarred Sumner's post about
the **agentic Zig→Rust rewrite of Bun** — a concrete, high-stakes worked instance of the stacked-loop /
verification-loop model.

## Summary

Willison flags the Bun rewrite as "an extremely sophisticated piece of agentic engineering, featuring
dynamic workflows, trial runs, adversarial review and all sorts of other interesting tricks." The
motivating pain was memory-management bugs (use-after-free, double-free, "forgot to free" in error
paths) from mixing GC with manual memory in Zig — all **compiler errors** in safe Rust with RAII/`Drop`
cleanup. The deeper point Sumner makes: *"Until very recently, programming language choice was a one-way
decision"* — you should "never stop the world and rewrite" (Joel Spolsky, 2000) — but **coding agents
powered by frontier models change that equation.**

## The loop mechanics (why it's on-thread)

The **enabling factor** was that Bun's test suite was written in TypeScript, so it could act as a
**language-independent conformance suite** — a harness could automate much of the port and grade it
against **~1M assertions**. Sumner's own account of how he built confidence to merge:

- *"For most of those 11 days (and after), I monitored workflows — manually reading the outputs to check
  for issues and bugs, and prompting Claude to edit the loop to fix things"* — **loop-editing** rather
  than hand-fixing.
- *"How do you review a PR with +1 million lines added?... A language-independent test suite with a
  million assertions, adversarial code review and when something does go wrong, **fixing the process
  that generates the code instead of hand-fixing the code**."* — the **hill-climbing / trace loop**.
- Ran **coordinated parallel agents** (worktrees) on the port.

Outcome: the Rust port shipped in **Claude Code v2.1.181 (June 17)**; startup got ~10% faster on Linux
and "otherwise, barely anyone noticed. Boring is good." Cost ≈ **$165,000 at API pricing** (5.9B uncached
input, 690M output, 72B cached-read tokens) — a rare concrete data point on the token economics of a
large unattended run.

## Connections

A concrete real-world case study for [[loop-engineering]]: the TS conformance suite **is** the
grader/verification loop (level 2), "fixing the process not the code" **is** the hill-climbing loop
(level 4) in [[langchain-the-art-of-loop-engineering]], and the whole run is an
[[unattended-coding-agents]] / [[long-running-agents]] instance at extreme scale. Reviewing a +1M-line
LLM-authored PR is the **comprehension-debt / verification-burden** angle (cf.
[[willison-agentic-engineering-patterns]] and the "understand to participate" thread). "Adversarial code
review" is the maker≠checker seam. Same-author thread as [[willison-designing-agentic-loops]]; ties to
[[agent-harness]], [[agentic-coding]], and (as a token-cost datapoint)
[[tornhill-codescene-unhealthy-code-agentic-token-cost]]. Ships on [[anthropic]]'s Mythos/Fable model.

## Caveat

A **link-blog** (Willison's framing over Sumner's first-party account); the underlying data are
Anthropic-internal (tokens weren't paid for) and single-project. Persuasive as an existence proof for
"conformance suite as the loop's grader," not a controlled result.
