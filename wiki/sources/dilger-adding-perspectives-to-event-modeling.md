---
title: "Martin Dilger — Adding Perspectives to Event Modeling"
type: source
created: 2026-06-17
updated: 2026-06-17
sources: [dilger-adding-perspectives-to-event-modeling]
raw_file: [raw/notes/dilger-adding-perspectives-to-event-modeling.md]
tags: [event-modeling, tooling, eventmodelers-ai, focus]
---

# Martin Dilger — Adding Perspectives to Event Modeling

LinkedIn post (with a short video) by **[[martin-dilger]]** (2026-06-17).
Source file: `raw/notes/dilger-adding-perspectives-to-event-modeling.md`.

## What it says

Announces a **"Perspectives"** feature in [[eventmodelers-ai]]: one event model rendered at different
levels of detail for different audiences, because "not every audience needs the same level of detail."

- The audiences he names: **C-Level** (big picture — how many slices, overall scope, when done),
  **Engineers** (full story — business rules, edge cases, workflows), **Architects** (higher-level but
  focused on components, boundaries, integrations, system structure), **Stakeholders** (the narrative /
  business process).
- First shipped perspective: the **High-Level View** ("strips away the noise… the overall flow").
- Speculates about an **Architect Perspective** — *deriving architecture views directly from an Event
  Model, maybe auto-generating something like **C4** from the model.*

## Why it matters here

A small but telling tooling move on the [[event-modeled-agent-design]] thread: it treats the
[[event-modeling|event model]] as a **single source the tool can project into multiple views** — the
same "model is the truth, views are generated" stance as [[dilger-is-code-still-the-source-of-truth]],
applied to *diagrams* rather than code. The "derive C4 from the model automatically" idea is the
architecture-diagram analog of code generation from the model, and connects the method to the
[[business-capabilities]] "components/boundaries/integrations" framing. Mostly a product feature, but it
extends the model-as-single-source-of-truth claim into the visualization layer.

## Caveats

Product announcement for [[eventmodelers-ai]]; the Architect Perspective / C4 generation is floated as a
future idea, not shipped.
