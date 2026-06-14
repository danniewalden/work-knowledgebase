---
title: Feedforward and Feedback Controls (Guides & Sensors)
type: concept
created: 2026-06-11
updated: 2026-06-14
sources: [fowler-bockeler-harness-engineering, openai-harness-engineering-codex, stripe-minions-one-shot-coding-agents, fowler-bockeler-maintainability-sensors]
tags: [harness-engineering, cybernetics, controls]
---

# Feedforward and Feedback Controls (Guides & Sensors)

[[birgitta-bockeler|Böckeler]]'s organising distinction for the controls inside a coding-agent
[[agent-harness]] ([[fowler-bockeler-harness-engineering]]). The harness acts as a cybernetic
**governor** combining both directions to regulate a codebase toward its desired state.

- **Guides (feedforward)** — anticipate behaviour and steer the agent *before* it acts. Raise the
  probability of a good result first time. Examples: AGENTS.md, Skills, reference docs, how-tos,
  codemods, language servers/CLIs.
- **Sensors (feedback)** — observe *after* the agent acts and let it self-correct. Most powerful
  when their output is optimised for LLM consumption (e.g. linter messages that embed the fix — a
  "positive prompt injection," exactly what [[openai-harness-engineering-codex]] does with custom
  lints). Examples: tests, linters, static analysis, logs, AI review.

Using only one direction fails: feedback-only repeats mistakes; feedforward-only never learns
whether the rules worked.

## Crossed with execution type

Each control is also **computational** (deterministic, fast, cheap — CPU: tests, linters, type
checkers) or **inferential** (LLM-based — semantic judgment, AI review; slower, costlier,
non-deterministic). Controls should be distributed across the change lifecycle by
cost/speed/criticality ("keep quality left"), plus continuous drift/health sensors outside the
lifecycle. This control system is the substance of [[harness-engineering]].

**Production example — [[stripe]]'s "shift feedback left"** ([[stripe-minions-one-shot-coding-agents]]):
a tiered computational-sensor stack — heuristic pre-push lints in <5s, then selective CI over 3M+
tests with **autofixes applied automatically** and only failures-without-autofix returned to the
agent, capped at "often one, at most two" CI rounds. A concrete illustration of running cheap sensors
as far left as possible and reserving expensive ones for later.

## Worked field report ([[fowler-bockeler-maintainability-sensors]])

Böckeler's sensors-only experiment sharpens the taxonomy with practice:

- **Computational sensors shine at the file/function level** (ESLint: max args/length/complexity;
  `dependency-cruiser` layer rules — an [[fitness-functions|architecture-fitness]] check used as a live
  sensor). The agent self-corrects on their feedback, and they can *replace* a markdown structure guide.
- **Self-correction guidance** is the key technique: custom lint/error messages that embed the *why*
  plus the exact fix ("positive prompt injection"), and **threshold-raising** instead of binary
  suppression so a rule re-fires if things degrade further.
- **Cross-file concerns need inferential sensors.** Raw coupling data fed to an LLM was noisy and
  over-flagged legitimate patterns; a full **inferential modularity review** ("garbage collection")
  was the most valuable, catching duplication and a date-range argument touching 40+ files. Good/bad
  isn't binary — it's *appropriate*, which needs context the import graph lacks.
- **[[mutation-testing]]** is the computational sensor behind the behaviour category: coverage ≠
  effectiveness (a 100%-covered file had 13 surviving mutants and no unit tests).
- **Sensor conflicts** are a real risk: `max-lines` vs `max-lines-per-function` pushed complexity out
  of functions and into long component-property chains.

_Sources: [[fowler-bockeler-harness-engineering]] · [[openai-harness-engineering-codex]] · [[fowler-bockeler-maintainability-sensors]]._
