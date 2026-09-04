---
title: "Dilger — Slicing keeps the cost curve flat (Triplet Architecture)"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [dilger-slicing-keeps-the-cost-curve-flat]
raw_file: [raw/notes/dilger-slicing-keeps-the-cost-curve-flat-triplet-architecture.md]
tags: [event-modeling, event-sourcing, vertical-slice-architecture, spec-driven-development, agentic-coding, focus]
---

# Dilger — Slicing keeps the cost curve flat

LinkedIn post by **[[martin-dilger]]**, 2026-08-29. Raw capture:
`raw/notes/dilger-slicing-keeps-the-cost-curve-flat-triplet-architecture.md`. A **restatement** of
[[dilger-triplet-flexible-agent-enabled-architecture]] rather than a new idea — but it states the
economic claim more bluntly than the newsletter does, and it is where he names the pattern for a general
audience.

## The claim

> "Building a feature in 5 years costs exactly as much or less as today. That's the only purpose of
> architecture."

Followed immediately by the concession that nobody believes it: *"most engineers smile. yeah.. good one.
it's not what happens in reality. Every feature added adds friction. The reason is coupling that slowly
accumulates."*

The remedy: *"The only way I found too keep the cost curve flat ( even slowly declining ) is consistently
slicing the system. **This must happen in while specifying already.**"* (sic, both.) — slicing as a specification-time
activity, not a refactoring one. Combined with Event Modeling and event sourcing, that is
[[triplet-architecture]].

## The AI-specific stake

The sharpest line, and the reason this post matters beyond restatement:

> "This is what makes working with AI so hard in grown code bases. Attempting Spec-Driven-Development
> without having a solution to this is like playing russian roulette. play it long enough and you'll
> inevitably loose."

That is the strongest statement in the KB of why [[spec-driven-development]] is not sufficient alone: a
spec handed to an agent needs somewhere clean to land, and an accumulated-coupling codebase is not it.
It is also a *conditional* claim rather than a rejection — which distinguishes him from the four SDD
critics ([[gojko-adzic]], [[birgitta-bockeler]], Zaninotto, Eberhardt), who argue the spec artifact
itself is the problem.

Also here: **"Slices are like Candy for AI"** — the KB's most-quoted phrasing of the token-economics
claim, arrived at independently by [[jeremy-miller]] from the other pole of
[[model-as-code-vs-model-as-language]], and measured by neither.

## Caveats

- Vendor marketing; assertion with no measurement, and the flat-cost claim is a five-year claim nobody
  has held still long enough to test.
- The post links a "detailed article" on Triplet-Architecture behind an `lnkd.in` shortlink that has
  never resolved — **still an uncaptured candidate primary**, possibly a fuller version of the
  newsletter piece.

## Related

[[triplet-architecture]] · [[slice]] · [[vertical-slice-architecture]] · [[spec-driven-development]] ·
[[event-sourcing]] · [[open-closed-principle]] · [[martin-dilger]] ·
[[dilger-triplet-flexible-agent-enabled-architecture]]
