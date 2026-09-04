---
title: "Dilger — A 'linter' for Event Modeling: Claude Code grades a board against a reference catalog"
type: source
created: 2026-08-10
updated: 2026-08-10
sources: [dilger-event-model-structure-linter-reference-catalog]
raw_file: [raw/notes/dilger-event-model-structure-linter-reference-catalog.md]
tags: [event-modeling, event-modeling-anti-patterns, event-modeled-agent-design, given-when-then, eventmodelers-ai, focus]
---

# Dilger — "Rating the structure of an Event Model based on heuristics"

Source: [[martin-dilger]], LinkedIn post, ~2026-08-07 (3d old, edited, at capture). Raw:
`raw/notes/dilger-event-model-structure-linter-reference-catalog.md`. Hashtags #eventmodeling #eventmodelers.

## Summary

A reader, **William Power**, wanted to know whether some freshly-created [[event-modeling|event models]]
were **structurally sound**. He asked Dilger for publicly available boards Dilger considers "well
structured"; Dilger pointed him at the **catalog**. Power then used **Claude Code to compare his own boards
against the "Reference"** to gauge whether the structure was similar. Dilger calls this "a **'linter' for
Event Modeling**" — it doesn't tell you whether the *processes* are modeled correctly, only that they are
**structured** correctly — and is considering shipping it as an [[eventmodelers-ai]] feature.

## Key points

- **Structure vs. correctness** — the check is explicitly about structural conformance to good exemplars,
  not semantic correctness of the domain; a deliberately modest, useful signal.
- **Reference-catalog-as-rubric** — a curated set of "well-structured" public boards becomes the oracle an
  agent grades against, an interesting alternative to hard-coded rules or the heuristic
  [[event-modeling-anti-patterns|"Shapes"]] taxonomy.
- **Agent-graded model quality** — Claude Code performs the comparison; pairs with the `/wdyt` reviewer
  ([[dilger-the-shapes-event-modeling-anti-patterns]]) as a second agent-driven EM quality gate, upstream of
  the [[given-when-then|GWT]] acceptance gates that grade the *code*.

## Connections

Sibling to [[dilger-the-shapes-event-modeling-anti-patterns]] (both are agent-driven EM structural-quality
ideas from the same week — heuristic taxonomy vs. reference comparison). Feeds [[event-modeling-anti-patterns]]
and [[event-modeled-agent-design]] (agent critiques the model). Relates to [[ai-readable-code]] (structural
conformance as a machine-checkable property) and [[eventmodelers-ai]] (mooted platform feature).

## Caveat

An idea Dilger is "thinking about," credited to a reader's experiment — not a shipped, evaluated feature.
"Well-structured" is defined only by Dilger's own catalog; the notion of a canonical reference set is
unvalidated.
