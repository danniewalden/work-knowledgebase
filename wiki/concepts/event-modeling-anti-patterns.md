---
title: Event Modeling Anti-Patterns ("The Shapes")
type: concept
created: 2026-08-10
updated: 2026-08-10
sources: [dilger-the-shapes-event-modeling-anti-patterns, dilger-event-model-structure-linter-reference-catalog]
tags: [event-modeling, event-modeling-anti-patterns, event-modeled-agent-design, focus]
---

# Event Modeling Anti-Patterns ("The Shapes")

A diagnostic vocabulary from [[martin-dilger]] for spotting problems in an [[event-modeling|event model]]
by its **silhouette** — the structural shape of the board tells you where to look before you read the
detail. Introduced in [[dilger-the-shapes-event-modeling-anti-patterns]] (2026-08). Where the method itself
gives you 3 building blocks and 4 (constructive) patterns, this is the complementary catalog of *mis*-shapes.

## "The Shapes"

- **The bed** — *one screen, many commands.* The only **hard red flag**: a single UI surface driving many
  commands usually signals an over-loaded screen / muddy command boundaries.
- **The left chair** — *one command, many events.* A **warning**, not wrong by default (a command can
  legitimately emit several events) — look closer.
- **The right chair** — *one read model, many events.* A **warning**: a view fed by many event types; may
  be fine, may signal a bloated projection.
- **The shelf** — *one slice, all scenarios.* A **warning**: a single slice absorbing every scenario.

Severity is **graded**: only the bed is a categorical problem; the chairs and shelf are heuristics — "places
to look closer before you commit to a design," not defects. Dilger's line: "Once you see them, you can't
unsee them."

## Why it matters for agents

The taxonomy is built to be **agent-operable**. Dilger's most-used AI-skill on [[eventmodelers-ai]],
invoked with **`/wdyt`** ("what do you think"), walks a model, challenges assumptions, and calls out these
anti-pattern shapes where they apply — an **agent as model-reviewer** working *upstream of code*, on the
spec itself. This complements the two dominant directions in [[event-modeled-agent-design]] (agent *authors*
the model; model *governs* the agent) with a third: agent *critiques* the model.

A sibling idea from the same week attacks model quality from the other end: an **EM "linter"** that grades a
board's **structure** (not its correctness) by having Claude Code compare it against a curated **reference
catalog** of well-structured boards ([[dilger-event-model-structure-linter-reference-catalog]]). Heuristic
shape-detection and reference-conformance are two routes to the same goal — an automated, agent-run quality
gate on the model, sitting upstream of the [[given-when-then|GWT]] acceptance gates that grade generated
code.

## Relationships

Extends [[event-modeling]] (the constructive patterns' negative image) and [[event-modeled-agent-design]]
(agent-as-reviewer seam). Adjacent to [[ai-readable-code]] (structural conformance as a machine-checkable
property) and [[given-when-then]] (the downstream, code-level gate). A platform feature of
[[eventmodelers-ai]].

## Caveat

Dilger's own coinage from workshop/conference experience; the shape names are informal and **not part of the
EM "Standard."** No external validation, and the reference-catalog "linter" is a mooted feature, not a
shipped/evaluated one.

_Source pages: [[dilger-the-shapes-event-modeling-anti-patterns]] · [[dilger-event-model-structure-linter-reference-catalog]]._
