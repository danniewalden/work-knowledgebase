---
title: "Source: Stripe — Minions (One-Shot, End-to-End Coding Agents)"
type: source
created: 2026-06-11
updated: 2026-06-11
sources: [stripe-minions-one-shot-coding-agents]
raw_file: [raw/articles/stripe-minions-one-shot-coding-agents.md]
tags: [harness-engineering, unattended-agents, coding-agents, stripe]
---

# Source: Stripe — Minions (One-Shot, End-to-End Coding Agents)

Engineering blog by Alistair Gray (Leverage team), [[stripe]], 2026-02-09. Part 1 of two. The
production case study [[fowler-bockeler-harness-engineering|Böckeler]] cites for "shift feedback
left" and heuristic pre-push linting. Raw capture:
`raw/articles/stripe-minions-one-shot-coding-agents.md`.

## Summary

**Minions** are Stripe's homegrown, fully **unattended** coding agents, built to **one-shot** tasks.
**1,000+ minion-produced PRs merge each week** — human-reviewed but containing no human-written code. **Vendor self-report:** this is Stripe's own engineering blog describing Stripe's own tooling. There is no external verification of the figure, no denominator (what share of all merged PRs), and no quality measure attached to it. Cite it with the attribution attached, per `CLAUDE.md`.
A run typically starts from a Slack mention and ends at a CI-passing PR ready for review, with no
interaction in between; engineers spin up many in parallel (handy during on-call).

## Key points

- **Why build it themselves:** Stripe's codebase is hundreds of millions of LOC, mostly Ruby (not
  Rails) with Sorbet typing and many homegrown libraries unfamiliar to LLMs; code moves >$1T/yr with
  heavy compliance constraints. Iterating in a large, mature codebase is far harder than greenfield —
  so the **harness tightly integrates Stripe's existing developer tooling**. Principle: *"if it's
  good for humans, it's good for LLMs, too."*
- **Entry points:** Slack (most common — reads the whole thread + links as context), CLI, web, and
  embedded buttons in internal tools (docs platform, feature flags, ticketing — e.g. flaky-test
  tickets carry a "fix with a minion" button). A web UI shows the minion's decisions/actions.
- **Devboxes:** runs start in pre-warmed isolated dev environments spun up in ~10s, with code/services
  preloaded, isolated from production and the internet (so no human permission checks needed). Gives
  parallelization without git-worktree overhead.
- **Agent loop:** a fork of Block's **goose** agent, with an opinionated orchestration that
  **interleaves agent loops with deterministic code** (git ops, linters, testing) so required steps
  always run. Reads the same agent rule files as Cursor/Claude Code; rules are **conditionally applied
  by subdirectory** (avoiding too many unconditional rules — echoes OpenAI's "too much guidance
  becomes non-guidance").
- **Context via MCP + Toolshed:** minions use [[model-context-protocol|MCP]] to gather docs, ticket
  details, build status, Sourcegraph code intelligence. A central internal MCP server, **Toolshed**,
  hosts **400+ tools**; agents get curated subsets. Relevant MCP tools are run deterministically over
  likely links *before* a run starts, to hydrate context.
- **Feedback layers ("shift feedback left"):** (1) a local executable using **heuristics to select
  and run relevant lints on each git push in <5s**; (2) CI selectively runs from **3M+ tests**, many
  with **autofixes** applied automatically; failures without autofix go back to the minion. (3)
  Deliberately **at most two CI rounds** — "often one, at most two… and only after we've fixed
  everything we can locally" — balancing speed vs. token/compute cost.

## Connections / contrast

The strongest **production datapoint** in the cluster for [[unattended-coding-agents]] and
[[agentic-coding]]. Its layered, shift-left lint/test feedback is a concrete instance of
[[feedforward-and-feedback-controls]] (computational sensors run as far left as possible) and of
[[harness-engineering]]'s "make correctness mechanically enforced." Conditional-by-subdirectory rules
parallel [[openai-harness-engineering-codex]]'s progressive disclosure / [[agent-legibility]]. The
deterministic-loop-around-the-agent design is the same "harness wraps the model" idea as
[[langchain-anatomy-of-an-agent-harness]]; Toolshed is a large-scale [[model-context-protocol]]
deployment ([[multi-agent-orchestration]]).

_Source page: [[stripe-minions-one-shot-coding-agents]]._
