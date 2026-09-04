---
title: "Böckeler — Maintainability Sensors for Coding Agents"
type: source
created: 2026-06-14
updated: 2026-06-14
sources: [fowler-bockeler-maintainability-sensors]
raw_file: [raw/articles/fowler-bockeler-maintainability-sensors.md]
tags: [harness-engineering, coding-agents, sensors, static-analysis, testing, thoughtworks]
---

# Böckeler — Maintainability Sensors for Coding Agents

Practical follow-up to [[birgitta-bockeler|Böckeler]]'s anchor [[harness-engineering]] article
([[fowler-bockeler-harness-engineering]]). Where that piece gave the *mental model* (guides &
sensors × computational & inferential — see [[feedforward-and-feedback-controls]]), this one is a
**worked field report**: she rebuilt an internal analytics dashboard (TypeScript/NextJS/React) from
scratch with AI agents (Cursor, Claude Code, OpenCode; Sonnet/Opus/composer-2), deliberately using
**almost no guides** so she could observe what *sensors alone* achieve on the **maintainability**
regulation category. Published in installments on martinfowler.com: basic linting (19 May), dependency
rules + coupling data + AI modularity review (20 May), test suite as regression sensor + conclusion
(27 May 2026).

## The thesis

Maintainability = "internal quality" — keeping change easy and low-risk *over time*. Internal-quality
problems hurt AI agents the same way they hurt humans: an agent in a tangled codebase looks in the
wrong place, duplicates code it didn't notice, or must load more context than a task needs. The
tell-tale early signal: the number of files touched for a small change starts creeping up.

## Sensors, by layer (and what worked)

- **Basic linting (computational) — file/function level.** ESLint targeting AI's low-hanging failure
  modes: max args, file length, function length, cyclomatic complexity — *none active by default*, she
  had to set the maximums. Two harness techniques stand out: (1) **custom lint messages as
  self-correction guidance** ("positive prompt injection") that embed the *why* and the exact
  suppression syntax; (2) letting the agent **slightly raise a threshold** (rather than suppress
  forever) so the rule re-fires if things get worse — "constraints preserved without a binary
  suppress-or-comply choice." Suppressions/threshold-bumps became her **code-review starting point**.
  Verdict: surprisingly powerful at this level; the cost-benefit flipped because AI makes custom rules
  cheap to write. Risk: **false sense of security** and **feedback overload** sending the agent into
  over-engineered refactor spirals.

- **Dependency rules (computational) — cross-module.** `dependency-cruiser` rules enforce a layered
  structure (routes → services → clients + domain). The agent violated rules a few times then
  **self-corrected on the feedback**. A useful *replacement for describing structure in a markdown
  guide* — but limited to what imports/filenames/folders can express. (This is an
  [[fitness-functions|architecture fitness]] check operating as a live [[feedforward-and-feedback-controls|sensor]].)

- **Coupling data (computational + inferential) — cross-module.** A custom agent-built tool emits
  coupling metrics (fan-in/out) via the TS compiler, with a web view (for humans) and a CLI (for the
  agent). Human DSM visualisations were **tedious and didn't reduce cognitive load**. Feeding the raw
  data to an LLM was **lackluster**: it flagged a deliberate DI-style factory and a legitimate shared
  `zod` contract as "god modules." Conclusion: **raw coupling data isn't useful to AI on its own** —
  good/bad isn't binary, it's *appropriate*, which needs context the import graph lacks.

- **AI modularity review (inferential) — cross-module.** Going *fully* inferential with Vlad
  Khononov's "Modularity Skills" was **the most fruitful** experiment: it found duplicate route code,
  an inconsistent backend-calling pattern, a date-range argument touching **40+ files** (recommend a
  wrapping object), auth logic misplaced in the wiring factory, and correctly *contextualised* the
  "god classes" the raw coupling tool had over-flagged. Grounding it in the coupling CLI added little.
  Re-running surfaced a finding the first run missed → **run LLM analyses multiple times when it
  matters**. This is "**garbage collection**" in the [[harness-engineering]] sense, and shows the agent
  was **compounding inadvertent technical debt** without it.

- **Test suite as regression sensor (computational).** Tests are the "ultimate specification"; a
  failing pre-existing test makes the agent *ask whether it broke something or is intentionally
  changing behaviour*. Two risks of unreviewed AI-generated tests: **coverage ≠ effectiveness**, and
  tests may encode faulty behaviour. Toolbox by cost: coverage ($), property-based ($), fuzz ($$),
  **mutation testing** ($$). See [[mutation-testing]].

## Mutation-testing finding (the headline)

A `mappers.ts` file showed **100% statement / 75% branch coverage but had no unit tests** — coverage
was high only because a big acceptance test executed those lines. Stryker reported **13 surviving
mutants**. Coverage tells you a line *ran*, not that its impact was *verified*. With the industry
trend toward AI-generated end-to-end/acceptance tests (assertion-light), **mutation testing becomes
crucial** to monitor the effectiveness gap — though it's resource-intensive. (She built a
`query_stryker.py` so the agent could query results without clogging its context — "AI helping me
help AI.")

## Conclusions & open questions

- **Computational sensors shine at the file/function level**; **cross-file** concerns (modularity,
  coupling) are too noisy without an **inferential** sensor's semantic judgment.
- **Sensor conflicts** are a looming issue: `max-lines` / `max-lines-per-function` pushed complexity
  *out of* functions and *into* long React component-property chains.
- Sensors **improve human review/trust** but are **not a take-the-human-out-of-the-loop** solution.
- Open: as confidence in sensors grows, **which guides can we delete?** Do good sensors make **weaker
  models** viable? How do we keep guides and sensors **consistent**?

## Touches

[[birgitta-bockeler]] · [[thoughtworks]] · [[harness-engineering]] · [[feedforward-and-feedback-controls]] ·
[[fitness-functions]] · [[mutation-testing]] · [[context-engineering]] · [[agent-legibility]] · [[agentic-coding]] ·
[[fowler-bockeler-harness-engineering]]

_Source: [[fowler-bockeler-maintainability-sensors]] (raw/articles/fowler-bockeler-maintainability-sensors.md)._
