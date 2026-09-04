---
source_url: https://adamtornhill.substack.com/p/hidden-design-decisions-refactoring
title: "Hidden Design Decisions: Refactoring Control Coupling"
author: Adam Tornhill
publication: "Code for Humans and Machines (Substack)"
published: 2026-06-16
retrieved: 2026-06-17
type: note
---

> Provenance note — SUMMARY in the compiler's own words (personal Substack; not a verbatim capture).
> Read the original at the URL above. This is the worked example behind CLEAR's "Explicit intent".

Tornhill argues that hiding a design decision inside a **boolean flag** is one of the worst things you
can do to code: a flag parameter forces the *caller* to select behavior, which is the classic smell
**control coupling** (Larry Constantine, *Structured Design*, 1979 — one module controls another's
internal execution flow). His running example is a Java `incidentUpdate(incident, boolean
executiveAudience)` that branches into an "executive" vs "engineering" message; the flag signals two
problems — **implicit knowledge** at the call site (what does `true` mean?) and **low cohesion** (one
method doing two jobs).

Fix: the **Strategy pattern** — a boolean flag is "a compressed strategy." Encapsulate each variant
behind a common contract (`IncidentAudience` with `ExecutiveAudienceUpdate` / `EngineeringAudienceUpdate`),
so `incidentUpdate(incident, EXECUTIVE_AUDIENCE)` replaces `incidentUpdate(incident, true)` — policy and
intent now visible at the call site. A secondary move introduces a small **domain type**
(`IncidentNarrative`) to carry shared interpreted facts, raising the semantic level and sharpening the
strategy contract. He notes the imperfect intermediate step is fine ("perfection is the enemy of getting
things done"; move the code so the *next* change is easier), and that the implementation form is
flexible — small classes, method references, or (in Clojure) partial application — because a pattern is
defined by *intent and trade-offs*, not a fixed class hierarchy.

Why it matters for AI: boolean flags are "cheap for humans to write and expensive for models to
interpret" — a flag carries little semantic information, so a model must scan extra context to infer
what it selects (a weak interface). Named strategy objects expose meaning directly, improving **local
reasoning**, narrowing edit scope, and making automated refactoring safer; the domain type delivers
**explicit intent** by aligning behavior with the domain concept structurally. The refactoring also
yields Open-Closed extensibility (add a new audience, don't reopen a long method). Explicitly maps to
**CLEAR**: Local Reasoning, Conceptual Alignment, Explicit Intent, Reduce the Edit Surface.
