---
title: Harness Engineering
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [fowler-bockeler-harness-engineering, openai-harness-engineering-codex, anthropic-effective-harnesses-long-running-agents, langchain-anatomy-of-an-agent-harness, firecrawl-what-is-an-agent-harness, hashimoto-my-ai-adoption-journey, stripe-minions-one-shot-coding-agents]
tags: [harness-engineering, agentic-ai, reliability, coding-agents]
---

# Harness Engineering

**Hub page.** Harness engineering is the practice of building and continuously improving the
[[agent-harness]] — everything around an LLM except the model itself — so that a non-deterministic
model does reliable work. Its defining stance, shared across sources: **treat every agent failure
as a system problem to permanently fix, not a prompt to retry** ([[mitchell-hashimoto]], via
[[firecrawl-what-is-an-agent-harness]]). When the agent makes a mistake, you engineer the
environment so it (mechanically) can't make that mistake again.

## Why it emerged

The term spread in early 2026: [[mitchell-hashimoto]] named it in
[[hashimoto-my-ai-adoption-journey|his adoption essay]] (Feb 5) — "anytime you find an agent makes a
mistake, you take the time to engineer a solution such that the agent never makes that mistake again"
— [[openai]] published a flagship case study days later, and
[[birgitta-bockeler]]/[[thoughtworks]] gave it a mental model. It names something practitioners were
already doing — the scaffolding that turns a stateless model into a
[[long-running-agents|long-running agent]]. As [[langchain]]'s Harrison Chase argues, better models
*expand* what harnesses must do rather than shrinking them (Claude Code is 512k+ LOC and growing).

[[mitchell-hashimoto|Hashimoto]]'s two concrete forms set the template: (1) **better implicit
prompting** via AGENTS.md (each line derived from an observed bad behavior); (2) **actual programmed
tools** (screenshot scripts, filtered test runners) that let the agent verify itself.

## The mental model ([[birgitta-bockeler|Böckeler]])

Two control directions × two execution types (see [[feedforward-and-feedback-controls]]):

- **Guides (feedforward)** steer *before* the agent acts; **Sensors (feedback)** let it
  self-correct *after*.
- **Computational** controls are deterministic/fast/cheap (tests, linters, type checkers);
  **Inferential** controls use an LLM (AI review, "LLM as judge") — richer but slower and
  non-deterministic.

The human's job is the **steering loop**: when an issue recurs, improve the controls. Three
regulation categories — *maintainability* (easiest), *architecture fitness*, and *behaviour*
(hardest, still unsolved). Not every codebase is equally **harnessable** ("ambient affordances":
strong typing, clear module boundaries, boring frameworks).

## How it shows up in practice

- **Repository as system of record** ([[openai-harness-engineering-codex]]): a ~100-line AGENTS.md
  *table of contents* over a structured `docs/` tree (**progressive disclosure**), custom linters
  whose error messages inject remediation instructions, and "garbage-collection" agents that fix
  drift. The goal is **[[agent-legibility]]** — "what the agent can't see doesn't exist."
- **Initializer + coding-agent structure** ([[anthropic-effective-harnesses-long-running-agents]]):
  feature lists (JSON), progress files, git, `init.sh`, and end-to-end self-verification.
- **Core primitives** ([[langchain-anatomy-of-an-agent-harness]]): filesystem, bash/sandbox,
  memory, compaction, [[ralph-loop]]s.
- **Shift-left feedback at scale** ([[stripe-minions-one-shot-coding-agents]]): heuristic <5s
  pre-push lints + selective CI over millions of tests with autofixes, capped at "often one, at most
  two" CI runs — powering [[unattended-coding-agents]] (1,000+ merged PRs/week).

## Relationship to neighbours

- **[[context-engineering]]:** harness engineering *uses* context engineering. Context engineering
  optimises *what the model sees*; harness engineering controls *the environment it operates in* —
  what it can access, what gets verified, what forces a retry. Building a coding-agent user harness
  is a specific form of context engineering ([[birgitta-bockeler|Böckeler]]).
- **[[agent-engineering]]:** the broader discipline of iterating LLMs into reliable systems;
  harness engineering is its environment-and-controls arm.
- **[[agent-governance]]:** the harness acts as a cybernetic *governor*; enforcement of invariants
  and audit trails overlaps with governance.
- Distinct from **prompt engineering** (a single call) and from agent **frameworks/orchestrators**
  (see [[agent-harness]]).

## Open questions

How to keep a growing harness coherent (guides/sensors not contradicting); how to evaluate harness
coverage/quality (a "code coverage" for harnesses); whether single general-purpose vs. specialised
agents work best; the unsolved **behaviour harness**; and how much migrates into models over time.

_Sources: [[fowler-bockeler-harness-engineering]] · [[openai-harness-engineering-codex]] · [[anthropic-effective-harnesses-long-running-agents]] · [[langchain-anatomy-of-an-agent-harness]] · [[firecrawl-what-is-an-agent-harness]]._
