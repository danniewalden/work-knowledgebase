---
title: "Böckeler — TDD inside the agent loop: theater or actual value?"
type: source
created: 2026-08-14
updated: 2026-08-14
sources: [bockeler-tdd-inside-the-agent-loop]
raw_file: [raw/articles/bockeler-tdd-inside-the-agent-loop.md]
tags: [harness-engineering, loop-engineering, agentic-coding, testing, mutation-testing, given-when-then, evals]
---

# Böckeler — "TDD inside the agent loop - theater or actual value?"

Source: [[birgitta-bockeler]], martinfowler.com, *Exploring Gen AI* series, 2026-08-10. Raw:
`raw/articles/bockeler-tdd-inside-the-agent-loop.md`.

## Summary

An exploratory eval asking whether instructing a coding agent to follow **TDD fully inside its own
loop** actually improves outcomes. She distinguishes three TDD-with-AI modes — (1) human writes the
tests, AI implements; (2) AI writes a failing test, **human reviews it**, AI implements; (3) fully
inside the agentic loop — and notes that (3) is now by far the most common. Setup: 5 batches over
small/medium/large greenfield business-logic tasks, Sonnet 4.6 generating and judging TDD adherence
from transcripts, Opus 4.8 blind-ranking the solutions on a self-generated rubric, plus
[[mutation-testing|mutation scores]].

**Result: no discernible quality difference**, and non-TDD solutions were ranked *higher* more often
than not; mutation scores showed no meaningful gap; TDD cost **~3–8.5× the tokens** (small 8.50×,
medium 2.96×, large 4.89× — caveated as directional, inflated by counting cache reads).

The mechanism she and Opus land on is the interesting part: the **non-TDD and test-first runs did full
up-front design** (architecture, data types, edge cases, contracts) before writing anything, while TDD
instructions actively work *against* an up-front design step — the design "emerged from the sum of many
locally-minimal decisions and was rarely revisited… it tended to land on whatever shape the first test
happened to lock in," and "behaviour the agent didn't think to write a test for didn't get implemented
at all." Ivett Ördög's training-data theory is quoted as a why: models have seen finished functions and
their descriptions, almost no step-by-step TDD, so their internal representation is requirements→code,
not the *process* of getting there.

## Key points

- **Red-green stops proving anything when the human leaves.** "When the agent both writes the test and
  confirms it failed, a red test tells you the agent ran it and saw failure, **not that the failure was
  for the right reason**." Agents also skipped or faked the red step and over-implemented ahead of the
  current test. This is the [[feedforward-and-feedback-controls|maker≠checker]] problem stated at the
  level of a single test.
- **Test-first doesn't reliably prevent tautological tests** — some TDD runs still checked the
  implementation's output against itself by re-running the same code to produce the "expected" answer.
- **The human-centred goals don't transfer.** YAGNI/restraint and Kent Beck's "managing fear" rationale
  are about *a human* sitting with friction and being given permission to relax; neither applies when
  the agent runs the loop. Agents overshoot minimal implementations anyway "because they had the full
  requirement available."
- **Her conclusion is a general principle, not a TDD verdict:** "being overly specific about *how* we
  want a model to do something is not a sustainable approach. Instead, we should find as many ways as
  we can to monitor the **outcomes** and give feedback… and we need to carefully think about **where we
  insert ourselves as arbiters** of what is good and correct." She has stopped telling coding agents to
  do TDD.
- **Substitutes she proposes**, each mapping onto her existing sensors model
  ([[fowler-bockeler-maintainability-sensors]]): [[mutation-testing]] as the regression-quality sensor
  ("I don't really care *how* regression quality was achieved, as long as I have a mechanism to see how
  good it is"); static analysis + periodic AI modularity review + trends in files-touched and
  tokens-per-change as refactoring triggers; and Ivett Ördög's **"Approved Scenarios"** — human-frozen
  functional scenarios in a bespoke runner that must be re-approved when violated — as a candidate
  confidence mechanism.
- **Costs beyond tokens:** TDD "doesn't seem to come natural to models… an uphill battle against the
  training data," needing heavy prompt iteration, and such a complex instruction set is likely to be
  **more volatile across model releases** than simpler ones — a maintenance burden on the harness.

## Connections

Sits directly under [[loop-engineering]] and [[harness-engineering]] as an *empirical* check on what
belongs inside the loop, and extends her own [[fowler-bockeler-maintainability-sensors|sensors-only
field report]] (same substitutes, now with a negative result motivating them). Sharpens
[[feedforward-and-feedback-controls]]: this is a case where a **guide** (a process instruction) fails
and the recommendation is to spend the budget on **sensors** instead.

**The tension worth naming with [[given-when-then]].** The KB's EM thread holds that GWT scenarios
govern the coding agent ([[jwilger-agent-skills-factory-pipeline]],
[[dilger-event-modeling-agent-harness]]). Böckeler's negative result is *not* a counter to that: her
target is the agent **inventing its own micro-tests step by step inside the loop**, whereas the EM
claim is about an **externally authored acceptance spec** the agent must satisfy — mode (1) in her own
taxonomy, the one she does not test. Read together they actually converge: the value is in a
human-or-model-authored specification and an outcome sensor, not in dictating the agent's inner
process. Her "Approved Scenarios" endorsement is the same instinct as a frozen GWT gate.
Cross-check also with [[esdm-event-sourced-domain-modeling]] (GWT as a machine-validated artifact) and
[[agentic-coding]].

## Caveat

She flags the limits herself: very small sample; "quality" almost fully delegated to Opus's judgment;
no run followed TDD perfectly; all tasks greenfield, small, and pure business logic — so nothing here
speaks to TDD in the agent loop on legacy code or across module boundaries. An honest exploratory
eval, explicitly inviting a larger study, not a result to cite as settled.
