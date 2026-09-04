---
title: "Adam Tornhill — Hidden Design Decisions: Refactoring Control Coupling"
type: source
created: 2026-06-17
updated: 2026-06-17
sources: [tornhill-hidden-design-decisions-control-coupling]
raw_file: [raw/notes/tornhill-hidden-design-decisions-control-coupling.md]
tags: [ai-readable-code, agentic-coding, refactoring, code-health, focus]
---

# Adam Tornhill — Hidden Design Decisions: Refactoring Control Coupling

Substack post by **[[adam-tornhill]]** ("Code for Humans and Machines"), 2026-06-16. In-window pickup
from the weekly watch. Summarized at `raw/notes/tornhill-hidden-design-decisions-control-coupling.md`
(personal Substack — not captured verbatim). The worked example behind
[[tornhill-clear-design-principles-agentic-age|CLEAR's]] "Explicit intent".

## What it says

A **boolean flag parameter hides a design decision** and forces the caller to select behavior — the
classic **control coupling** smell (Constantine, *Structured Design*, 1979). His Java example,
`incidentUpdate(incident, boolean executiveAudience)`, branches into executive vs. engineering output;
the flag signals **implicit knowledge** at the call site (what does `true` mean?) and **low cohesion**
(one method, two jobs). Fix with the **Strategy pattern** ("a boolean flag is a compressed strategy"):
encapsulate each variant behind an `IncidentAudience` contract so `incidentUpdate(incident,
EXECUTIVE_AUDIENCE)` replaces `incidentUpdate(incident, true)`. A secondary move adds a small **domain
type** (`IncidentNarrative`) that raises the semantic level. Notes: imperfect intermediate steps are
fine (move code so the *next* change is easier); pattern *intent/trade-offs* matter, not a fixed class
hierarchy (classes, method references, or Clojure partial application all work).

## Why it matters here

A concrete, code-level instance of [[ai-readable-code]]: "boolean flags are cheap for humans to write
and expensive for models to interpret" — a flag carries little semantic information, so an agent must
scan extra context to infer behavior (a weak interface), whereas named strategies expose intent at the
call site and **narrow the edit scope**. Tornhill explicitly maps the refactoring to
[[tornhill-clear-design-principles-agentic-age|CLEAR]] (Local Reasoning, Conceptual Alignment, Explicit
Intent, Reduce the Edit Surface) and to the [[open-closed-principle]]. Reinforces the
[[agent-legibility]] / [[locality-of-reference]] thread from the refactoring-pattern angle, and
connects coupling/cohesion to agent cost (cf. [[tornhill-codescene-unhealthy-code-agentic-token-cost]],
[[balanced-coupling]]).

## Caveats

Personal Substack; a teaching example, not an empirical result. One of a series of refactoring
walkthroughs ([[tornhill-ai-readable-code-series]]).
