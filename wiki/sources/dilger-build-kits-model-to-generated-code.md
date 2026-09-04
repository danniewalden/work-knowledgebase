---
title: "Martin Dilger — Build kits: model to generated code in 30 seconds"
type: source
created: 2026-06-21
updated: 2026-06-21
sources: [dilger-build-kits-model-to-generated-code]
raw_file: [raw/notes/dilger-build-kits-model-to-generated-code-30-seconds.md]
tags: [event-modeling, event-sourcing, agentic-coding, spec-driven-development, focus]
---

# Martin Dilger — Build kits: model to generated code in 30 seconds

LinkedIn post by **[[martin-dilger]]** (~2026-06-20; captured 2026-06-21 via logged-in Chrome).
Source file: `raw/notes/dilger-build-kits-model-to-generated-code-30-seconds.md`. On the tight
EM × agents focus ([[event-modeled-agent-design]]).

## What it says

- Dilger pitches **"build kits"** for [[eventmodelers-ai]]: the goal is **"From Model to generated Code
  in 30 seconds."**
- The driver is pedagogical. When he learned [[event-sourcing]] there were "literally zero real-world
  examples"; he had to assemble the pieces by hand, which "took ages." Build kits collapse that.
- Anecdote: someone with **zero event-sourcing experience** modeled **two slices** following the modeling
  instructions, then **handed them to an agent to build**. His claim: *seeing the modeled system built
  following best practices makes learning ~10x faster.* You iterate — change the model, see how it
  changes the implementation — and learn by watching, then build.
- Caveat from Dilger himself: not "deploy to production immediately." He invites contributions / adopters
  for the build kits.

## Why it matters here

A concrete instance of Dilger's standing thesis — the [[event-modeling]] *slice* as the unit handed to a
coding agent ([[dilger-event-modeling-agent-harness]], [[dilger-model-is-a-living-spec-always-on-agent]])
— now framed as a **learning on-ramp**: model → agent-built reference implementation as the fastest way
to *understand* event-sourced systems, not just ship them. It extends the
[[spec-driven-development]]/"slice is the unit of work" line with a teaching-tool angle and reinforces
[[event-modeled-agent-design]]'s "model is the spec the agent builds from."

## Caveats

Vendor self-report / marketing for [[eventmodelers-ai]]; the "30 seconds" and "10x faster" figures are
promotional. Build kits are announced, not demonstrated here.

## Touches

[[martin-dilger]] · [[eventmodelers-ai]] · [[event-modeling]] · [[event-sourcing]] ·
[[event-modeled-agent-design]] · [[agentic-coding]] · [[spec-driven-development]] ·
[[vertical-slice-architecture]]

_Source: `raw/notes/dilger-build-kits-model-to-generated-code-30-seconds.md`._
