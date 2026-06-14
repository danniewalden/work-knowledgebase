---
title: "Dilger — On the Faros AI Report: AI amplifies unclear requirements"
type: source
created: 2026-06-13
updated: 2026-06-13
sources: [dilger-faros-ai-report-amplifies-unclear-requirements]
tags: [event-modeling, agentic-coding, spec-driven-development, requirements, metrics, focus]
---

# Dilger — On the Faros AI Report: AI amplifies unclear requirements

LinkedIn post by **[[martin-dilger]]** (2026-06-13) reacting to the **Faros AI Report**
(22,000 developers across 4,000 teams). His thesis, repeated "in every workshop": **AI doesn't
fix unclear requirements, it amplifies them** — and now there's a large dataset behind it. Raw
capture: `raw/articles/dilger-faros-ai-report-amplifies-unclear-requirements.md`.

## The numbers he pulls out

Throughput looks great on the surface — **task completion +33.7%**, **epics/developer +66.2%**,
AI-generated code now **60% of accepted** (up from 20%). The other side of the coin:

- **Bugs per developer: +54%**
- **Incidents per PR: +242.7%** (more than triple)
- **PRs merged with zero review: +31.3%**
- **Median review time: +441.5%**

The finding he flags as most uncomfortable: this happens **even to teams with strong engineering
practices**. Good process alone doesn't absorb what AI now produces. AI writes code that *looks*
correct — idiomatic, well-named — but "looking right and being right are different things," and the
gaps are invisible on the surface, pushing slow senior-engineer review into the bottleneck.

## The argument (why it's on-thread)

Dilger reads the report's own conclusion — more reviewers and stricter gates only treat the
symptom; **the fix is upstream: give AI (and humans) a clear spec before any code is written** — as
validation of [[event-modeling]] applied to [[agentic-coding]]. An Event Model gives the agent *and*
its reviewers a shared source of truth (which events exist, what triggers them, how the pieces fit)
instead of guessing intent from a messy codebase. Outcome he claims: smaller PRs, reviewers who know
what a change is *supposed* to do, "an AI that's no longer guessing." This is the requirements/spec
framing of [[event-modeled-agent-design]] and dovetails with his [[spec-driven-development]] thread.

## Caveats

A LinkedIn marketing post (he's "building the agentic modeling plattform on eventmodelers.ai", see
[[eventmodelers-ai]]), not an analysis of the underlying report — the Faros figures are quoted, not
independently verified here, and the Event-Modeling-as-fix conclusion is his. Treat the percentages
as **claimed** pending a look at the primary Faros report.

## Links

Entities: [[martin-dilger]], [[eventmodelers-ai]]. Concepts: [[event-modeling]],
[[spec-driven-development]], [[event-modeled-agent-design]], [[agentic-coding]],
[[unattended-coding-agents]], [[agent-governance]].
Related sources: [[dilger-spec-driven-development-applied]], [[dilger-keep-command-handlers-pure]],
[[jwilger-agent-skills-event-modeling]], [[openai-harness-engineering-codex]],
[[stripe-minions-one-shot-coding-agents]].
