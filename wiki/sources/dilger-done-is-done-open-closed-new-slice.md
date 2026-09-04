---
title: "Martin Dilger — \"Done is Done\": a new concept is a new slice, not an extension"
type: source
created: 2026-06-19
updated: 2026-06-19
sources: [dilger-done-is-done-open-closed-new-slice]
raw_file: [raw/notes/dilger-done-is-done-open-closed-new-slice.md]
tags: [event-modeling, open-closed-principle, vertical-slice-architecture, event-sourcing, agentic-coding, focus]
---

# Martin Dilger — "Done is Done": a new concept is a new slice, not an extension

LinkedIn post by **[[martin-dilger]]** (2026-06-18; captured same day via logged-in Chrome).
Source file: `raw/notes/dilger-done-is-done-open-closed-new-slice.md`. On the tight EM × agents focus.

## What it argues

The question engineers under-ask: *"Can I build this without touching any existing code that already
works?"* Dilger calls this **"Done is Done"** and identifies it with the **[[open-closed-principle]]**
(open for extension, closed for modification): unless there's a compelling reason, you don't change
existing behaviour.

Worked example: a client asked for **Guest Invitations** for the [[eventmodelers-ai|Eventmodelers
Platform]]. His first instinct was to reuse the existing invitation logic, add a `BoardId`, and extend
it. He stopped, because it's a **live event-sourced system** — changing existing flows means retesting
everything and potentially dealing with **migrations / upcasters** ([[event-versioning-and-upcasting]]).
Re-asking "Done is Done," he concluded Guest Invitations only *look* like Invitations: different rules
and lifecycle, so it's **a different concept → a new [[vertical-slice-architecture|slice]], an addition,
not an extension.** The trap is defaulting to reuse to save a few lines and ending up **coupling concepts
that should stay separate** — a cost that shows up later as change becomes expensive, risky, and slow.

Two focus-relevant details: he **modeled the new slice in ~30 minutes so an agent could implement it**
while he taught a workshop ("that part still feels slightly surreal") — a concrete instance of
[[event-modeled-agent-design]] (human models the slice, agent builds it autonomously); and the whole
post is a **coupling-over-reuse** argument.

## Why it matters here

It's the cleanest in-KB link between **OCP / Event Modeling's flat feature-cost curve** and the
**slice as the unit of addition**: new features arrive as new slices, not edits to working code. It
reinforces the coupling-over-reuse theme from [[dilger-event-modeling-agent-harness]] ("coupling, not
context-window") and the [[balanced-coupling]] / [[business-capabilities]] idea that a distinct concept
deserves a distinct boundary. It also gives a practical reason to prefer a new slice in an
[[event-sourcing|event-sourced]] system: avoiding migrations/upcasters on a live event log
([[event-versioning-and-upcasting]]).

## Caveats

Short LinkedIn post; vendor context (his own platform). The OCP↔slice mapping is asserted via one
example, not argued at length. "Done is Done" is Dilger's branding for OCP applied to slices.

## Touches

[[martin-dilger]] · [[open-closed-principle]] · [[vertical-slice-architecture]] · [[event-sourcing]] ·
[[event-versioning-and-upcasting]] · [[event-modeled-agent-design]] · [[balanced-coupling]] ·
[[business-capabilities]] · [[eventmodelers-ai]]

_Source: `raw/notes/dilger-done-is-done-open-closed-new-slice.md`._
