---
title: "Dilger — User stories need Event Modeling's framework"
type: source
created: 2026-07-13
updated: 2026-07-13
sources: [dilger-user-stories-need-event-modeling-framework]
raw_file: [raw/notes/dilger-user-stories-need-event-modeling-framework.md]
tags: [event-modeling, spec-driven-development, requirements, user-stories, focus]
---

# Dilger — User stories need Event Modeling's framework

LinkedIn post by **[[martin-dilger]]** (~2026-07-12).
Source file: `raw/notes/dilger-user-stories-need-event-modeling-framework.md`. Filed by the
2026-07-13 live-Chrome sweep. Method-wide [[event-modeling]] thread (a concrete requirements anecdote,
no explicit agent angle).

## Why it matters

The cleanest short statement of Dilger's **requirements-first** argument aimed at a mainstream audience:
the problem isn't that teams lack *discipline* writing user stories, it's that a user-story template is a
**format with no framework behind it**. It grounds the abstract [[spec-driven-development]] /
"[[dilger-harness-is-20-percent-requirements-are-80|requirements are the 80%]]" thesis in an everyday
pain (writer's block at the empty template).

## Core thesis

- **A user story is "a sentence structure" that leaves you alone with it** — "no framework behind it, no
  way to know what's missing." A team mandated to deliver all requirements as user stories sat "paralyzed…
  writers block" for weeks: what to write, how much context, where to start.
- **What was missing wasn't discipline — it was a visual way to design the business solution.** Dilger
  showed the [[event-modeling]] method "in 15 minutes" and it clicked because it solved that exact
  problem: **add a timeline and the writer's block disappears — you always know what comes next.** The
  model is also a **shared language between business and engineering**.
- **The model subsumes the user story, then replaces it.** The projected sequence: (1) user stories
  "easy to generate straight from the timeline" instead of invented from nothing → (2) stories quietly get
  better ("what changed?") → (3) the team stops translating and **hands over the modeled timeline itself**
  ("engineers are much happier with that") → (4) small use cases get clarified live, **adjusting the model
  as they speak** (claimed **60–80% faster**) → (5) they do the timeline together from the start, removing
  handovers, waiting, and guessing.

## Relevance / links

A requirements-side worked anecdote for [[spec-driven-development]] and
[[dilger-harness-is-20-percent-requirements-are-80]] (the "human/communications 80%"): Event Modeling as
the missing scaffold *underneath* user stories, and eventually as their replacement. Reinforces
[[event-modeling]]'s "shared language" and timeline claims and the "generate the story from the model, not
the other way round" inversion also seen in [[dilger-is-code-still-the-source-of-truth]] (the model, not
the downstream artifact, is the source of truth). Caveat: LinkedIn marketing framed around a prospective
client — strong on framing, a single un-booked anecdote for evidence.

_Raw source: `raw/notes/dilger-user-stories-need-event-modeling-framework.md`._
