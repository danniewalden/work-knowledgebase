---
title: "Vlad Khononov — The Golden Age of Modularity"
type: source
created: 2026-06-17
updated: 2026-06-17
sources: [khononov-golden-age-of-modularity]
raw_file: [raw/notes/khononov-golden-age-of-modularity.md]
tags: [modularity, coupling, business-capabilities, agent-legibility, substrate, focus]
---

# Vlad Khononov — The Golden Age of Modularity

Blog post by **[[vlad-khononov]]** ("Rants on Software Design", vladikk.com), 2025-03-29. Summarized at
`raw/notes/khononov-golden-age-of-modularity.md` (compiler summary, not verbatim).

## What it says

Khononov argues software is entering a **"golden age of modularity,"** and gives a deliberately
practical, two-part test for whether a design is modular:

1. **Localized change** — when you change the codebase, it is crystal clear which parts must be
   touched, and that number is as small as possible (ideally one component).
2. **Predictable effect** — when you make a change, you can predict its effect on the system's behavior.

His move is to connect this to the AI moment: the "vibe coding" hype (apps built with no coding skill,
large fractions of AI-written code) only pays off when the code is modular — i.e. when changes stay
local and effects stay predictable. Boundaries are what make a codebase tractable, for humans *and* for
AI. Underpinned by his **Balanced Coupling** model (assess coupling by its strength × distance ×
volatility — the subject of his book *Balancing Coupling in Software Design*).

## Why it matters here

Establishes [[vlad-khononov]] in the KB and grounds the **coupling/cohesion** axis of
[[business-capabilities]] in a named model (Balanced Coupling) from a recognized DDD author. His
two-part modularity test is essentially [[agent-legibility]] / [[locality-of-reference]] stated from the
design-theory side, and it converges with [[adam-tornhill|Tornhill's]]
[[tornhill-clear-design-principles-agentic-age|CLEAR]] ("reduce the edit surface", "local reasoning"),
[[fritzsche-functional-core-imperative-shell-agentic-coding|Fritzsche]],
[[miller-codebase-is-the-prompt-vertical-slices-ai|Miller]], and
[[dilger-event-modeling-agent-harness|Dilger's]] "coupling, not context-window." A useful theoretical
spine under the otherwise practitioner-heavy "good boundaries make agents cheaper/safer" claim.

## Caveats

Foundational/out-of-window (Mar 2025), surfaced when adding Khononov to the watch — not a new
development. Personal blog; the post is an opinion piece ("hot take"), with the rigor living in his book.
