---
title: "Dilger — The Shapes: 4 patterns + 4 anti-patterns you can read off an event model's silhouette"
type: source
created: 2026-08-10
updated: 2026-08-10
sources: [dilger-the-shapes-event-modeling-anti-patterns]
raw_file: [raw/notes/dilger-the-shapes-event-modeling-anti-patterns.md]
tags: [event-modeling, event-modeling-anti-patterns, event-modeled-agent-design, given-when-then, eventmodelers-ai, focus]
---

# Dilger — "The Shapes"

Source: [[martin-dilger]], LinkedIn post, ~2026-08-10 (42m old at capture). Raw:
`raw/notes/dilger-the-shapes-event-modeling-anti-patterns.md`. Hashtag #eventmodeling.

## Summary

Dilger names a diagnostic vocabulary for reading [[event-modeling|event models]] by their **silhouette**.
After reviewing dozens of models at the AxonIQ conference he found "the shape alone told the story," so he
started calling recurring structures **"The Shapes"**: the **bed** (one screen, many commands), the **left
chair** (one command, many events), the **right chair** (one read model, many events), and the **shelf**
(one slice, all scenarios). Only the **bed is a hard red flag**; the rest are *warnings* — places to look
closer before committing to a design, not defects by default.

The agent seam: his **most-used AI-Skill on [[eventmodelers-ai]]**, invoked with **`/wdyt`** ("what do you
think"), walks a model, asks meaningful questions, challenges assumptions, and **calls out the anti-pattern
shapes where they make sense**. He uses it constantly "in modeling, in building and as a sparring-partner" —
framing the agent as a reviewer that surfaces the "that looks weird there" observations a colleague would.

## Key points

- **A named anti-pattern taxonomy for Event Modeling** — the KB had the method's 3 building blocks / 4
  patterns but no catalog of *mis*-shapes; "The Shapes" fills that, and does it in visual/structural terms
  (silhouette) rather than prose rules.
- **Only the bed is a hard red flag** (one screen issuing many commands ≈ an over-loaded UI/command
  boundary); the left/right chairs and shelf are heuristic warnings, not errors — a graded severity model.
- **Agent-as-model-reviewer** — `/wdyt` operationalizes the taxonomy as an AI skill that lints a model and
  challenges it; the review target is the *model*, upstream of code, which fits the spec-first thesis
  ([[spec-driven-development]], [[dilger-harness-is-20-percent-requirements-are-80]]).

## Connections

Introduces [[event-modeling-anti-patterns]] (new concept). Reinforces [[event-modeled-agent-design]] (the
agent reviews/critiques the model, a companion to the model *governing* the agent) and [[eventmodelers-ai]]
(the `/wdyt` skill as a platform feature). Sibling to [[dilger-event-model-structure-linter-reference-catalog]]
(another EM structural-quality-via-agent idea, same week) and to the acceptance-gate role of
[[given-when-then]].

## Caveat

LinkedIn post promoting [[eventmodelers-ai]]; the taxonomy is Dilger's own coinage from workshop experience,
no external validation. "The Shapes" names are informal and not (yet) part of the EM "Standard."
