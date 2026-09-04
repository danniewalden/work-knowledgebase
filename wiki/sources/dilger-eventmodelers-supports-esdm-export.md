---
title: "Dilger — Eventmodelers now exports Event Models to ESDM (UI, API, MCP, CLI)"
type: source
created: 2026-08-14
updated: 2026-08-14
sources: [dilger-eventmodelers-supports-esdm-export]
raw_file: [raw/notes/dilger-eventmodelers-supports-esdm-export.md]
tags: [event-modeling, event-modeled-agent-design, eventmodelers-ai, esdm, model-context-protocol, interop, focus]
---

# Dilger — "The Eventmodelers Plattform now officially supports ESDM"

Source: [[martin-dilger]], LinkedIn post, 2026-08-13. Raw:
`raw/notes/dilger-eventmodelers-supports-esdm-export.md`. Hashtag #eventmodeling.

## Summary

[[eventmodelers-ai]] now officially supports **[[esdm-event-sourced-domain-modeling|ESDM]]** — the
Event Sourced Domain Modeling Language from [[golo-roden]] / [[thenativeweb]]. Dilger says he talked
with Roden at the **Event Modeling Conference in Munich** (June 2026) after Roden's ESDM talk; the
platform had always had its own well-documented format, "but it was always clear I wanted it to be open
to any format." He added **export of any Event Model to ESDM via the UI, and also via API, MCP and the
CLI** — the operative line being:

> "So your agent can request any modeled slice or chapter in the format it needs."

It took under an hour because "the whole plattform is an extension model. Literally anything is an
extension — supported languages, supported datastores, anything." He will work **with Roden on an Event
Modeling extension for ESDM** to better support the **timeline** notion Event Modeling depends on.

## Key points

- **A neutral interchange format for slices, served over [[model-context-protocol|MCP]].** This is the
  concrete plumbing under the long-standing "the model is the agent's spec" claim: not a hosted board
  the agent must be taught, but a *requestable artifact* in a published format, per slice or per
  chapter, over four channels (UI/API/MCP/CLI). See [[agent-readable-model-artifacts]].
- **Closes the KB's standing "ESDM/EmLang materialization" watch item.** The KB had ESDM as a
  specification ([[esdm-event-sourced-domain-modeling]]) and Dilger's own **EmLang** YAML dialect as an
  *import* format ([[dilger-event-modeling-knowledge-hub-emlang]]), but no evidence of the two camps
  meeting. This is the first captured instance of an EM board tool emitting a *third-party* open format.
- **The board-and-file camps converge.** The KB previously framed ESDM (file-first, offline, any LLM
  reads the YAML) as a *contrast* with the board+MCP camp (Fraktalio, prooph board, Eventmodelers).
  Export collapses the contrast: the board becomes an authoring surface that can hand the agent files.
- **The gap ESDM has to close is the timeline.** ESDM models ES/DDD/CQRS *structure*, not the Dymitruk
  timeline/swimlane method — the exact limitation the KB noted at ESDM's capture. A Dilger–Roden joint
  extension aimed at the timeline is the first move to fix it, and is worth watching as a small step
  toward [[em-standardization-foundation|EM standardization]].
- **Extension-model architecture as the enabling claim** — languages, datastores and formats are all
  extensions, which is why format support is cheap. Vendor self-report, but it is a falsifiable
  architectural claim rather than pure positioning.

## Connections

[[agent-readable-model-artifacts]] (the new seam this belongs to) · [[event-modeled-agent-design]]
(the model as the artifact the agent consumes) · [[esdm-event-sourced-domain-modeling]] +
[[golo-roden]] / [[thenativeweb]] (the format and its authors) · [[eventmodelers-ai]] (the platform) ·
[[model-context-protocol]] (the serving channel) · [[dilger-event-modeling-knowledge-hub-emlang]] (the
format-agnostic knowledge-hub framing this executes on) · [[em-standardization-foundation]] (two
tool-makers agreeing on a format is standardization in practice).

## Caveat

LinkedIn self-report by the vendor; no documentation, example output, or independent check captured —
the linked docs URL is a shortener. "Under an hour" and "literally anything is an extension" are
marketing-inflected. The joint ESDM timeline extension is **announced intent, not shipped**.
