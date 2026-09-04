---
title: "Source: Böckeler — Harness Engineering for Coding Agent Users"
type: source
created: 2026-06-11
updated: 2026-06-11
sources: [fowler-bockeler-harness-engineering]
raw_file: [raw/articles/fowler-bockeler-harness-engineering.md]
tags: [harness-engineering, coding-agents, cybernetics, thoughtworks]
---

# Source: Böckeler — Harness Engineering for Coding Agent Users

Article by [[birgitta-bockeler]] (Distinguished Engineer, [[thoughtworks]]), published on
[[martin-fowler]]'s site 2026-04-02. The most developed *mental model* for [[harness-engineering]]
from the coding-agent user's perspective. Supersedes her February 2026 memo. Raw capture:
`raw/articles/fowler-bockeler-harness-engineering.md`.

## Summary

A harness is "everything in an AI agent except the model itself" ([[agent-harness]]). Böckeler
narrows this to the **outer harness** a coding-agent *user* builds on top of the agent's built-in
harness, to work with less supervision while keeping trust in the output. A well-built outer
harness both raises the probability the agent gets it right first time and gives it a feedback
loop to self-correct before issues reach human eyes — reducing review toil and wasted tokens.

## Key points

- **Guides (feedforward) vs. Sensors (feedback).** Guides anticipate and steer *before* the
  agent acts (AGENTS.md, Skills, ref docs, codemods, LSPs); sensors observe *after* and let it
  self-correct (linters, tests, AI review). Feedback-only → repeats mistakes; feedforward-only →
  never learns whether rules worked. See [[feedforward-and-feedback-controls]].
- **Computational vs. Inferential.** Computational controls are deterministic, fast, cheap
  (tests, linters, type checkers) — run on every change. Inferential controls use an LLM
  ("LLM as judge", AI review) — richer/semantic but slower, costlier, non-deterministic.
- **The steering loop.** The human's job is to *steer* by iterating on the harness: when an
  issue recurs, improve the controls so it becomes less probable. AI can help build the controls.
- **Keep quality left.** Distribute controls across the change lifecycle by cost/speed/criticality,
  plus continuous drift/health sensors outside the lifecycle. Mirrors continuous integration/delivery.
- **Three regulation categories:** *maintainability* harness (easiest — existing tooling),
  *architecture fitness* harness ([[fitness-functions]]), and *behaviour* harness (hardest, unsolved —
  too much faith placed in AI-generated tests).
- **Harnessability & "ambient affordances"** (Ned Letcher): some codebases are more governable —
  strong typing, clear module boundaries, "boring" frameworks. Greenfield can bake it in; legacy
  needs it most where it's hardest to build.
- **Harness templates + Ashby's Law:** committing to a service topology reduces variety, making a
  comprehensive harness achievable; templates may bundle guides+sensors per topology.
- **The human as implicit harness:** agents lack social accountability, taste, and org memory; a
  good harness externalises that — but aims to *direct* human input, not eliminate it.

## Connections / contrast

The conceptual anchor for the whole harness cluster. Frames [[harness-engineering]] as applied
[[context-engineering]] (context engineering supplies the *means* to deliver guides/sensors).
The cybernetic "governor" lens connects to [[agent-governance]]. Its guides/sensors model is the
*user-side* complement to the *builder-side* practices in [[openai-harness-engineering-codex]]
(custom linters, garbage collection) and [[anthropic-effective-harnesses-long-running-agents]]
(feature lists, self-verification). Extends [[agent-engineering]] and [[agentic-coding]].

_Source page: [[fowler-bockeler-harness-engineering]]._
