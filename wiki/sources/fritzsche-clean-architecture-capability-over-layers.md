---
title: "Fritzsche — Clean Architecture is untouchable; the real concern is the domain capability"
type: source
created: 2026-06-29
updated: 2026-06-29
sources: [fritzsche-clean-architecture-capability-over-layers]
raw_file: [raw/notes/fritzsche-clean-architecture-untouchable-capability-over-layers.md]
tags: [business-capabilities, vertical-slice-architecture, ddd, agentic-coding, focus]
---

# Fritzsche — Clean Architecture is untouchable; the real concern is the domain capability

LinkedIn post by **[[rico-fritzsche]]** (2026-06-28; captured 2026-06-29 via logged-in Chrome).
Source file: `raw/notes/fritzsche-clean-architecture-untouchable-capability-over-layers.md`. A fuller
article is linked in the first comment (not captured). Credits **Ralf Westphal**'s work on functional
dependencies.

## What it says

A critique of **Clean Architecture** as an idea that has become "almost untouchable — the more diagrams
are shared, the less often their assumptions are questioned." His points:

- **Dependency Inversion changes the *direction* of dependencies but does not remove the *functional*
  dependencies inside the behavior.** (Per the post image: DI keeps concrete infrastructure outside the
  domain, but it only swaps a concrete dependency for an abstract one — the business logic still depends
  on I/O.)
- **Separation of Concerns is not achieved by horizontal technical layers; the real concern is the
  [[business-capabilities|domain capability]].**
- **CRUD is not domain language.** Domain experts think in processes, flows, decisions, and state
  transitions — not Create/Read/Update/Delete.
- **Functional Core / Imperative Shell** keeps behavior independent from side effects and is a much
  stronger foundation for coherent domain capabilities.

## Why it matters here

This is the **capability-over-layers** argument ([[autonomous-domain-capabilities]],
[[rico-fritzsche-rpu-reactor-vocabulary]]) turned specifically against Clean/Hexagonal architecture, and
it reinforces the [[fritzsche-functional-core-imperative-shell-agentic-coding|FC/IS-inside-a-slice]]
recipe. Same throughline as his earlier "layered architecture = *distributed technical ownership*" line:
horizontal layers fragment a capability; capability should be the boundary, with technical separation
living *locally* (FC/IS) rather than *globally* across layers. The "CRUD is not domain language" point
echoes the [[event-modeling]]/[[event-sourcing]] stance that decisions and events — not data operations —
are the modeling primitives.

## Caveats

LinkedIn opinion post; the supporting article (first comment) is uncaptured. Restates a thesis already
well-represented in the KB (capability-as-boundary, FC/IS) — its novelty is the explicit Clean
Architecture target and the DI-doesn't-remove-functional-dependency point, not a new model. One author's
view; "the real concern is the domain capability" is asserted, not demonstrated here.

## Touches

[[rico-fritzsche]] · [[business-capabilities]] · [[autonomous-domain-capabilities]] ·
[[vertical-slice-architecture]] · [[domain-driven-design]] · [[event-modeling]] ·
[[fritzsche-functional-core-imperative-shell-agentic-coding]]

_Source: `raw/notes/fritzsche-clean-architecture-untouchable-capability-over-layers.md`._
