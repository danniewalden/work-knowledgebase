---
title: "Willison — Agentic Engineering Patterns (guide)"
type: source
created: 2026-07-06
updated: 2026-07-06
sources: [willison-agentic-engineering-patterns]
raw_file: [raw/articles/willison-what-is-agentic-engineering.md]
tags: [agentic-coding, coding-agents, loop-engineering, harness-engineering, guide]
---

# Willison — Agentic Engineering Patterns

Summary of [[simon-willison]]'s living guide **Agentic Engineering Patterns**
(simonwillison.net/guides/agentic-engineering-patterns/, started 2026-02-23;
principles chapter captured verbatim, created 2026-03-15).
Source file: `raw/articles/willison-what-is-agentic-engineering.md`.

## What it is

A deliberately **evolving** guide collecting patterns for getting good results out of
**coding agents** — Claude Code, OpenAI Codex, Gemini CLI. Willison frames it as a work in
progress aimed at patterns "unlikely to become outdated as the tools advance," updated
continuously rather than finished.

## Key points

- **Coins/uses "agentic engineering"** for developing software with the assistance of coding
  agents — a practitioner counterpart to [[martin-fowler]]'s "agentic programming"
  ([[fowler-agentic-programming]]). Both land on the same boundary the KB's
  [[agentic-coding]] page uses.
- **Crisp agent definition:** *"Agents run tools in a loop to achieve a goal."* The agent
  calls an LLM with the prompt + tool definitions, runs requested tools, feeds results back —
  and for coding agents one of those tools **executes code**. This is the plain-language
  statement of the [[react-loop|tools-in-a-loop]] model underneath [[loop-engineering]] and
  the [[agent-harness]].
- **Code execution is the defining capability:** without running the code, LLM output "is of
  limited value"; with it, agents "iterate towards software that demonstrably works" — the
  verify-and-iterate feedback loop ([[feedforward-and-feedback-controls]]).
- **The human job shifts, not shrinks:** deciding *what* code to write, specifying problems at
  the right level of detail, and **verifying/iterating** — echoing the "requirements are the
  80%" line ([[dilger-harness-is-20-percent-requirements-are-80]]) and [[spec-driven-development]].
- **Agents don't learn, harnesses do:** "LLMs don't learn from their past mistakes, but coding
  agents can, provided we deliberately update our instructions and **tool harnesses**" — a
  direct statement of [[harness-engineering]] as accumulated, edited context.
- **Vibe coding ≠ agentic engineering:** keeps Karpathy's original narrow sense of
  [[vibe-modeling|vibe coding]] (unreviewed, prototype-quality, "forget the code exists") and
  argues against inflating it to mean any LLM-written code — the same distinction the
  [[agentic-coding]] page draws.

## Structure (chapters)

Principles (what/cheap code/hoarding skills/better code/anti-patterns) · Working with coding
agents (how they work, Git, **subagents** → [[multi-agent-orchestration]]) · Testing & QA
(red/green TDD, first run the tests, agentic manual testing → the sensor/[[fitness-functions]]
side) · Understanding code (linear walkthroughs, interactive explanations) · Annotated prompts ·
Appendix (prompts he uses).

## Relevance to the KB

Willison is a **practitioner-voice anchor** on the [[agentic-coding]] / [[loop-engineering]] /
[[harness-engineering]] threads — the hands-on "what actually works with coding agents"
complement to Fowler/Böckeler (conceptual) and Osmani/swyx ([[addyosmani-loop-engineering]],
loop framing). Not an [[event-modeling]] voice; captured for the design-substrate-meets-agents
edge.

_Raw source: `raw/articles/willison-what-is-agentic-engineering.md`._
