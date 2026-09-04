---
title: EM Standardization & "The Munich Event"
type: concept
created: 2026-07-31
updated: 2026-08-31
sources: [roden-too-many-islands-em-conf-2026, johansen-is-it-safe-to-jump-em-conf-2026, dilger-first-event-modeling-conference-munich-recap, dilger-eventmodelers-supports-esdm-export]
tags: [event-modeling, event-sourcing, ddd, standardization, community, focus]
---

# EM Standardization & "The Munich Event"

The idea, crystallized at the 2nd Event Modeling Conference (Munich, Jun 25-26 2026), that
the Event Sourcing / CQRS / DDD community needs **shared standards** — terminology, file
formats, canonical examples, and tooling conventions — and possibly a **neutral foundation**
(in the spirit of the Linux Foundation or CNCF) to steward them.

## The problem: "too many islands, too few bridges"

[[golo-roden]]'s recap ([[roden-too-many-islands-em-conf-2026]]) names the field an
"archipelago." The fragmentation runs on four axes:

- **Methodology** — aggregates vs [[dynamic-consistency-boundaries|DCB]];
  [[event-storming]] vs [[event-modeling]] vs Domain Storytelling.
- **Vocabulary** — event vs *domain* event, command vs *intent*, read model vs *projection*.
- **Canonical examples** — every teacher has a different "hello world" (cinema box office;
  course enrollment; city library), so a newcomer must independently discover they're all
  the same handful of ideas.
- **Tooling** — Axon, unpublished in-house frameworks, EventSourcingDB/OpenCQRS/Nimbus; each
  island's assumptions quietly leak into how people think the whole field works.

Each island is internally coherent and externally hard to reconcile, and the cost falls on
the newcomers the community most wants to welcome. Roden's line: "diversity without shared
reference points isn't richness. It is fragmentation."

## "The Munich Event"

On the afternoon of day two the frustration became a concrete proposal: a community
foundation to provide a shared backbone. The open questions (who stewards it? what does it
own first? neutral enough to be trusted, opinionated enough to be useful?) went unresolved,
but the room signed a flip-chart commitment — **"The Munich Event"** — to pursue it. Stated
aims, sharpest-pain-first: **standardization** (shared terminology, file formats, examples —
"connective tissue") and **spreading the word** to a wider audience.

## Why it matters here

This is the community-level frame behind several already-tracked moves: the Dymitruk/Dilger
"standardization JV" noted at the *first* conference ([[dilger-first-event-modeling-conference-munich-recap]]),
Dilger's careful, standard-respecting method extension ([[dilger-extending-event-modeling-query-when]]),
and the push for a plain-text, versioned, AI-readable model format
([[esdm-event-sourced-domain-modeling]], [[dilger-event-modeling-knowledge-hub-emlang]],
[[dilger-drawio-model-in-code]]). It also reframes [[johansen-is-it-safe-to-jump-em-conf-2026]]'s
"the constraint is narrative/adoption, not technique" thesis: standardization *is* the
adoption play. Open question for this KB: whether a shared file format (ESDM / EmLang) becomes
the de-facto bridge, and whether the foundation materializes beyond the flip chart.

## First bridge actually built (2026-08-13)

The format half of that open question got its first concrete answer, and it came from a bilateral deal
rather than a foundation. Following a conversation at the Munich conference,
[[martin-dilger]]'s [[eventmodelers-ai]] now **exports any Event Model to
[[esdm-event-sourced-domain-modeling|ESDM]]** — [[golo-roden]]'s format, i.e. a *competitor's* — over
UI, API, [[model-context-protocol|MCP]] and CLI, and the two announced joint work on an **ESDM extension
carrying Event Modeling's timeline**, the notion ESDM currently lacks
([[dilger-eventmodelers-supports-esdm-export]]). Two observations: (1) this is exactly the bridge Roden's
own [[roden-too-many-islands-em-conf-2026|"too many islands"]] complaint asked for, arriving as vendor
interop rather than governance; (2) it suggests the de-facto standard may be settled by **export
compatibility** between the two or three serious tools long before any foundation ratifies anything —
worth watching against the flip-chart proposal. Still early: announced intent for the timeline
extension, no shipped spec, and one direction only (export, not round-trip).

## Related

[[model-as-code-vs-model-as-language]]

_Sources: [[roden-too-many-islands-em-conf-2026]] · [[johansen-is-it-safe-to-jump-em-conf-2026]] · [[dilger-first-event-modeling-conference-munich-recap]] · [[dilger-eventmodelers-supports-esdm-export]]._
