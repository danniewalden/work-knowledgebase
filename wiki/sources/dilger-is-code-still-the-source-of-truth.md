---
title: "Martin Dilger — Is Code still the source of truth?"
type: source
created: 2026-06-17
updated: 2026-06-17
sources: [dilger-is-code-still-the-source-of-truth]
raw_file: [raw/notes/dilger-is-code-still-the-source-of-truth.md]
tags: [event-modeling, spec-driven-development, agentic-coding, focus]
---

# Martin Dilger — Is Code still the source of truth?

LinkedIn post by **[[martin-dilger]]** (2026-06-16), responding to a question from Sam Hatoum.
Source file: `raw/notes/dilger-is-code-still-the-source-of-truth.md`.

## What it says

A tight argument that **the model/spec, not the code, is the source of truth** — and that AI makes this
impossible to ignore.

- Defines "source of truth" pragmatically: *where do you go to understand how a piece of functionality
  works?* When code rots (spaghetti, missing logs/monitoring) it "reveals nothing," and the real source
  of truth becomes "the one person who just knows" — which evaporates when they leave.
- Separates **intent** (what the system must do) from **the actual thing** (what the code does). Intent
  usually "lives nowhere" — a closed Jira ticket, a stale Confluence page, a departed PM's head — so you
  can't even verify the system still does what it should.
- **Code is a lagging indicator** — the *result* of intent, always chasing it, never leading. When AI
  generates code from a specification, the **spec becomes the source of intent**, code is just one
  regeneratable output, and where code and model diverge "AI can detect the drift and adapt." Code
  becomes "almost disposable."

## Why it matters here

The cleanest statement yet of the **[[spec-driven-development]]** half of
[[event-modeled-agent-design]]: it argues *why* the [[event-modeling|event model]] must be the durable
artifact and code the disposable projection — the mirror image of the [[event-sourcing]] "events are
truth, read models are rebuildable" stance, lifted up to the design/spec layer. Directly reinforces
[[dilger-model-is-a-living-spec-always-on-agent]] and the new
[[dilger-event-modeling-agent-harness|Agent Harness]] (the model's GWT scenarios as the regeneration
contract), and rhymes with the legibility thread — "intent that lives nowhere" is exactly what
[[agent-legibility]] and [[tornhill-clear-design-principles-agentic-age|CLEAR's]] "explicit intent" push
back on. Note the **"coupling"** through-line: his harness post's "coupling, not context-window" and
this post's "spaghetti reveals nothing" are the same complaint from two angles.

## Caveats

Opinion post; marketing-adjacent for [[eventmodelers-ai]] / the *Spec Driven* book. The "AI detects
drift and adapts" claim is asserted, not demonstrated.
