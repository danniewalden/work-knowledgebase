---
title: "Dilger — Free-form drawings on the board: the agent reads sketches and draws back"
type: source
created: 2026-08-10
updated: 2026-08-10
sources: [dilger-agentic-collaboration-freeform-drawings]
raw_file: [raw/notes/dilger-agentic-collaboration-freeform-drawings.md]
tags: [event-modeling, event-modeled-agent-design, eventmodelers-ai, model-context-protocol, focus]
---

# Dilger — "This starts to feel like true agentic collaboration"

Source: [[martin-dilger]], LinkedIn post, ~2026-08-09 (1d old at capture). Raw:
`raw/notes/dilger-agentic-collaboration-freeform-drawings.md`. Hashtags #eventmodeling #eventmodelers.

## Summary

Dilger adds a **"free form drawings"** layer to [[eventmodelers-ai]] alongside the structured, Excel-like
**Chapters** grid ([[dilger-planning-like-excel-legible-to-human-and-ai]]) — and reports it unlocked more
than expected. He drew on the board himself, then drew **by voice** (Voice Mode), then lassoed a group of
nodes and wrote a question inside it ("Does this make sense?"). The surprise: **the agents read the drawings
as context** — what's inside vs. outside a boundary, where an arrow points. The "true magic" came when he
added **[[model-context-protocol|MCP]] tools that let the agent draw *itself*.** Combined with his `/wdyt`
review skill, the agent now returns not just text comments but **sketches, arrows, question marks, and
written questions on the board** — "like having a colleague somewhere remote joining the Board and just
working with you."

## Key points

- **A new EM×agents interaction modality** — beyond structured YAML / grid coordinates, the agent both
  **consumes** freeform visual context (spatial grouping, arrow direction, lasso-scoped questions) and
  **produces** it (draws back). Visual annotation becomes a two-way channel between human and agent.
- **Voice + drawing** as model input — voice-mode sketching lowers the authoring friction further.
- **MCP as the agent's drawing hands** — the agent's ability to draw is exposed through MCP tools, the same
  board-as-tool pattern as [[fraktalio-event-modeler-connect-ai-agents-mcp]] / [[proophboard-skills-ai-agent-event-modeling]],
  extended from structured elements to freeform marks.

## Connections

Extends [[event-modeled-agent-design]] (agent-authors/reviews-the-model direction) and [[eventmodelers-ai]]
(freeform layer added atop the Excel grid). Companion to [[dilger-planning-like-excel-legible-to-human-and-ai]]
(structured addressability) — together, structured *and* freeform surfaces the agent can read/write. Relates
to [[ai-readable-code]] (a spec legible to human and machine at once, now visually).

## Caveat

Single-vendor self-report / LinkedIn marketing for [[eventmodelers-ai]]; an enthusiastic experiment write-up,
no demo, reliability data, or independent evaluation of how well the agent actually parses freeform drawings.
