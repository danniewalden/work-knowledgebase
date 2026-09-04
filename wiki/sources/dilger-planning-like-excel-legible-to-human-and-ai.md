---
title: "Dilger — Planning Like It's Excel: a spec legible to human and AI at once"
type: source
created: 2026-07-10
updated: 2026-07-10
sources: [dilger-planning-like-excel-legible-to-human-and-ai]
raw_file: [raw/notes/dilger-planning-like-excel-legible-to-human-and-ai.md]
tags: [event-modeling, event-modeled-agent-design, spec-driven-development, ai-readable-code, eventmodelers-ai, focus]
---

# Dilger — "Planning like it's Excel"

Source: [[martin-dilger]], LinkedIn post, 2026-07-09 (~17h old at capture). Raw:
`raw/notes/dilger-planning-like-excel-legible-to-human-and-ai.md`. Hashtags #eventmodeling
#eventsourcing #eventmodelersai.

## Summary

Dilger argues that **freeform whiteboards degrade** — diagrams are great for live discussion, but
"after a week nobody knows what they mean anymore," and [[event-modeling|Event Models]] rot the same
way if nobody owns them. His fix is structural: model **"like it's Excel."** A whiteboard lets people
draw anywhere, move things, and invent new patterns mid-session "because the medium lets them, not
because it's needed" — so six months later nobody outside the room can read the board. An **Excel-like
left-to-right grid** instead **enforces a plot / storyboard**: you can't jump around and lose the
thread because the grid won't let you.

The agent-facing payoff is the second property: the grid gives **every element a coordinate, like a
cell reference.** That makes the model *addressable* in both directions — "I can tell an AI *'add a
field in B3, adjust all dependents'* and it means something precise. It talks back the same way — on a
real project it once flagged: *'there's a problem in B3, adding items might be missing the price.'*"
He built **[[eventmodelers-ai]]** around this Excel idea, claiming "humans and Agents love it alike."

## Key points

- **Thesis:** *"Clear structure isn't nostalgia. It's what makes a spec legible to a human and an AI at
  once — and why both get it immediately."* The through-line of his [[spec-driven-development]] /
  [[event-modeled-agent-design]] argument, now reduced to a UI-design principle.
- **Anti-degradation:** structure is the antidote to Event-Model rot; freeform expressiveness is a
  liability, not a feature, once you need the model to stay readable and ownable over months.
- **Coordinate-addressability** is the concrete mechanism: a grid coordinate is a stable, precise
  reference an agent can be *instructed with* and can *report against* — a two-way, unambiguous handle
  on the spec (contrast the ambiguity of "the box near the middle").
- Announces a **video series on agentic event modeling** ("how software planning and building looks in
  2026 and beyond"): *Getting started, Agentic Modeling, Git Version Control, Spec-Driven-Building,
  On-Prem Deployment, Sketching, The timeline idea* — asks which to publish next.

## Connections

Tightest-focus [[event-modeled-agent-design]] material: it names *why* a structured model is
**agent-legible** — the coordinate is what makes the model an API the agent reads and edits precisely,
a sharper mechanism than the general "model as spec" claim. Ties to [[event-modeling]] (structure over
freeform; the grid enforces the storyboard/plot), [[eventmodelers-ai]] (the Excel grid is the
platform's core design bet), [[ai-readable-code]] (a spec optimized for human *and* machine reading),
[[spec-driven-development]], and [[given-when-then]]. Consistent with his "coupling, not context-window"
and model-as-source-of-truth lines ([[dilger-is-code-still-the-source-of-truth]],
[[dilger-event-modeling-agent-harness]]).

## Caveat

LinkedIn marketing for [[eventmodelers-ai]] — strong framing, single-vendor self-report, no demo or
independent evaluation of the "Excel grid" claim captured. The coordinate-addressability idea is
plausible and concrete but unverified against a running project beyond his own anecdote.
