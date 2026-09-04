---
title: "Dilger — Highlighting in Event Modeling: screen markers that give context to agents"
type: source
created: 2026-08-14
updated: 2026-08-14
sources: [dilger-highlighting-markers-give-context-to-agents]
raw_file: [raw/notes/dilger-highlighting-markers-give-context-to-agents.md]
tags: [event-modeling, event-modeled-agent-design, eventmodelers-ai, agent-legibility, focus]
---

# Dilger — "Best Practice: Highlighting in Event Modeling"

Source: [[martin-dilger]], LinkedIn post, 2026-08-12. Raw:
`raw/notes/dilger-highlighting-markers-give-context-to-agents.md`. Hashtags #eventmodelers
#eventmodeling.

## Summary

A method best practice he has taught for years, now with an agent twist. **Don't fear complex screens**
— most real screens are complex — but at any point in time in the system, typically only *one part* of
the screen is interesting. So **mark it**: make explicit what matters *right now*, "not in 5 min, not 5
min ago, right now."

Two craft notes: he now typically uses **HTML screens generated off the design system** rather than
sketching by hand ("just much faster to generate"), while cautioning that **ugly screens are better
early** — "more focus, less distraction. Beautiful comes later."

The new capability on [[eventmodelers-ai]]: **markers** — select anything on a screen, with optional
dynamic blurring of everything outside the marker. And then the line that makes this a focus-area item:

> "But again something I didn't think of.. Those markers give context to agents. They can read them,
> they can understand them. They can validate them and use them to build the UI."

## Key points

- **Attention markup as agent context.** A marker encodes *what is salient at this point on the
  timeline* — information that is implicit for a human reading the screen in sequence but otherwise
  invisible to an agent. It narrows the agent's target from "this screen" to "this region, now."
- **Three agent verbs, not one:** agents **read** markers, **validate** against them, and **build the
  UI** from them. The validate verb puts markers alongside `/wdyt` and the mooted linter in the
  agent-as-model-reviewer direction ([[dilger-the-shapes-event-modeling-anti-patterns]],
  [[dilger-event-model-structure-linter-reference-catalog]]).
- **Third instance of the same pattern in a fortnight** — after coordinate-addressable grid cells
  ([[dilger-planning-like-excel-legible-to-human-and-ai]]) and freeform drawings the agent reads and
  draws back ([[dilger-agentic-collaboration-freeform-drawings]]), markers are a *third* surface where
  a human-facing modeling affordance turns out to be machine-readable. Collected in
  [[agent-readable-model-artifacts]].
- **"Something I didn't think of"** — worth noting as a pattern in his own reports: the agent-facing
  value of these features is discovered *after* shipping them for humans, not designed in. Weak
  evidence, but it is the same claim [[ai-readable-code]] makes from the code side — artifacts made
  legible for humans tend to be legible for machines.
- **Generated HTML screens over hand sketches** is a small but real shift in EM practice, and a mild
  tension with his own "ugly screens are better early" advice; he holds both, scoped by phase.

## Connections

[[agent-readable-model-artifacts]] · [[event-modeled-agent-design]] · [[eventmodelers-ai]] ·
[[event-modeling]] (screens as first-class model elements) · [[agent-legibility]] ·
[[ai-readable-code]] · [[context-engineering]] (a marker is a hand-authored context narrowing).

## Caveat

Vendor self-report on LinkedIn; no example, demo, or evidence that agents actually parse markers
usefully — "they can read them" is a claim, not a measurement. The best-practice half (highlight what
matters now) is long-taught craft and stands independently of the tooling.
