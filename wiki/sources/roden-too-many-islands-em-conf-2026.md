---
title: "Roden — Too Many Islands, Too Few Bridges (EM Conference 2026 recap)"
type: source
created: 2026-07-31
updated: 2026-07-31
sources: [roden-too-many-islands-em-conf-2026]
raw_file: [raw/articles/roden-too-many-islands-too-few-bridges-em-conf-2026.md]
tags: [event-modeling, event-sourcing, ddd, conference, standardization, esdm, focus]
---

# Roden — Too Many Islands, Too Few Bridges (EM Conference 2026 recap)

Raw: `raw/articles/roden-too-many-islands-too-few-bridges-em-conf-2026.md` —
[[golo-roden]], the native web / EventSourcingDB blog, 2026-06-29. **The long-awaited
published recap of the 2nd Event Modeling Conference (Munich, Jun 25-26 2026)** — a
standing KB gap since 07-18, finally captured via live logged-in Chrome. Complements
the practitioner reflection from [[johansen-is-it-safe-to-jump-em-conf-2026]]
(ChronosHub side) with the vendor/organizer-adjacent view.

## Summary

Roden frames the conference as a community "at the edge of something," but its
defining theme was a problem: the Event Sourcing / CQRS / DDD world is **"an
archipelago" — too many islands, too few bridges**. On day two the room crystallized a
concrete response: a proposed **community foundation** (Linux-Foundation/CNCF spirit)
for **standardization**, signed on a flip chart as **"The Munich Event."** Roden's own
talk — *"Your Domain Model Belongs in the Repository"* — argued the model must live as
versioned plain text in Git beside the code, and demoed [[esdm-event-sourced-domain-modeling|ESDM]]
round-tripping code↔model↔code live with an AI assistant.

## Key points

- **Logistics:** Impact Hub Munich (former industrial site), sold out at ~40 people,
  organized by [[nebulit]], hosted by [[martin-dilger]]; [[adam-dymitruk]] opened with a
  keynote **by video** (couldn't attend in person). Format: keynotes, talks, workshops,
  open-space, a pitch marketplace — with deliberate "breathing room" for side-room deep
  dives.
- **The fragmentation thesis (the heart of it):** the field isn't one field. Methodology
  splits (aggregates vs [[dynamic-consistency-boundaries|DCB]]; [[event-storming]] vs
  [[event-modeling]] vs Domain Storytelling), **vocabulary** splits (event vs domain
  event, command vs intent, read model vs projection), **canonical-example** splits (WPS's
  cinema box office; Waidelich & [[sara-pellegrini]]'s course enrollment; the native web's
  city library), and **tooling** splits (Axon; in-house unpublished frameworks;
  EventSourcingDB/OpenCQRS/Nimbus). Each island is internally coherent, externally hard to
  reconcile — and the cost lands on newcomers. "Diversity without shared reference points
  isn't richness. It is fragmentation."
- **"The Munich Event":** a signed flip-chart commitment to pursue a foundation. Aims,
  in priority order: **standardization** (shared terminology, file formats, examples — the
  connective tissue) and **spreading the word**. No charter/bylaws yet; the point was that
  rival islands agreed to build toward each other. See [[em-standardization-foundation]].
- **Roden's talk — "Your Domain Model Belongs in the Repository":** two claims — (1) the
  field needs far more standardization; (2) *models die the moment the workshop ends* (photo
  → wiki → never updated). Fix: the model belongs in a **Git repository** next to the code as
  a versioned plain-text artifact — diffs, history, review, blame, one source of truth,
  changed with the code in one PR. [[esdm-event-sourced-domain-modeling|ESDM]] (YAML for
  DDD/CQRS/ES building blocks) is his bridge; because it's structured, "so can an AI" read it.
  **Live demo:** AI reverse-engineered an ESDM model *out of* an existing app, then generated
  *two* implementations (Kotlin + Python) *from* that one model.

## Connections

Closes the standing "2nd Munich recap" open thread. The fragmentation/standardization theme
seeds the new [[em-standardization-foundation]] concept and reframes why Dilger's method work
(the Query/WHEN extension [[dilger-extending-event-modeling-query-when]], the Dymitruk/Dilger
standardization JV noted in [[dilger-first-event-modeling-conference-munich-recap]]) matters.
Roden's "model belongs in the repo, versioned, AI-readable" argument is the same conviction as
[[esdm-event-sourced-domain-modeling]], [[dilger-drawio-model-in-code]] (model-in-code + a
framework the agent can follow), and [[dilger-is-code-still-the-source-of-truth]] — and is in
direct tension with [[yordis-prieto-code-is-the-ultimate-diagram]] (Prieto: regenerate the
*diagram from the code*; Roden/Dilger: keep the *model* as a co-equal versioned artifact). The
code↔model↔code AI demo is a worked instance of [[event-modeled-agent-design]] and the
"structured history/models are what AI needs" line ties to [[roden-event-sourcing-meets-mcp-whole-story-for-llms]].

_Sources: [[roden-too-many-islands-em-conf-2026]]._
