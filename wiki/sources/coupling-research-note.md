---
title: "Coupling — research note (boundary edge-weights)"
type: source
created: 2026-06-22
updated: 2026-06-22
sources: [coupling-research-note]
raw_file: [raw/notes/coupling-research-note.md]
tags: [coupling-cohesion, modularity, ddd, business-capabilities, team-topologies, substrate, focus, research-input]
---

# Coupling — research note (boundary edge-weights)

A deep-research run for **Dannie** (2026-06-22), captured verbatim at
`raw/notes/coupling-research-note.md`. It surveys coupling frameworks to answer a single product
question: **what should the weight on a dependency edge mean** on a *user-needs map*, in service of a
future "boundary-weighting / coupling-cost-score" feature that would score or suggest boundary
configurations. Explicitly **research input, not a decision**.

## Product framing (the "why")

The user-needs-map product treats boundaries as **interpretive** (team / system / domain / make-buy),
but its primary intent is **software-model boundaries** — bounded contexts, system seams, module
decomposition. That framing decides which literature applies: a software-boundary-placement model fits;
a module-internal taxonomy or a team-topology lens is adjacent at best. The feature concept is an
**editor-judgment** tool (no telemetry / no git mining), which further filters the candidate dimensions.

## What it concludes

- **[[vlad-khononov|Khononov]]'s Balanced Coupling is the direct fit** and the primary recommendation.
  Of his three dimensions, the two that suit an editor-dial UX are the ones he himself defines as
  *subjective*: **Integration Strength** (4-level: intrusive → functional → model → contract) as the
  primary dial, and **Volatility** (judged via DDD subdomain, *not* commit history) as the secondary.
  See the enriched [[balanced-coupling]] page for the scales and the `BALANCE = (STRENGTH XOR DISTANCE)
  OR NOT VOLATILITY` formula.
- **Distance is not an edge weight** — it is a property of the *candidate partition*, only meaningful
  once a boundary is drawn. Recommendation: **two dials, not three** (also a UX/cognitive-load call).
- The **classical [[coupling-taxonomy|Stevens/Myers/Constantine 1974]]** six-level taxonomy is a
  historical anchor but a *vocabulary mismatch* — intra-program module connection, not capability-graph
  edges.
- **[[team-topologies|Team Topologies]]** supplies *partition-side constraints* (cognitive load, ISH),
  not edge weights — relevant only if a boundary is read as "a team."
- **Change-coupling ([[adam-tornhill|Tornhill]] / CodeScene)** is the wrong shape: VCS-mineable
  telemetry, so asking an editor to estimate it is a category error. Volatility-coupling is its
  judgment-based human analog.

## Open product questions it leaves

Per-map vs global edge weights; linear vs exponential numeric mapping of Integration Strength; how to
fold Distance into *partition* scoring (the BALANCE formula is per-site, not per-partition); live score
vs auto-suggester (keeping the editor in the structural-thinking loop); and the unresolved
**[[yves-goeleven|Goeleven]]** taxonomy gap.

## Why it matters here

This is the first source that turns the KB's **"good boundaries make code tractable"** strand (the
[[balanced-coupling]] / [[business-capabilities]] / [[ai-readable-code]] thread) into a concrete
**edge-weight semantics** question for a real product. It grounds Khononov's model with a primary not
previously in `raw/` (the 2024 book *Balancing Coupling*, ISBN 9780137353538, plus his coupling.dev site
and GitHub skill) — partly closing the "capture a primary for Balanced Coupling" to-do flagged on the
old [[balanced-coupling]] page. It also seeds two new concept pages ([[coupling-taxonomy]],
[[team-topologies]]) and a new originator entity ([[larry-constantine]]).

## Caveats

- The **recommendation section is synthesis** (design opinion grounded in verified inputs), not a
  verified-source claim.
- Several adjacent claims were adversarially **refuted** and should be treated carefully: Khononov's
  Distance over-specified as "encapsulation boundaries"; Team Topologies' Dunbar-style group-size
  cutoffs as *hard* bounds; ISH as a *cognitive-load* criterion (its real anchors are autonomy /
  self-containment). Martin's instability metric and Newman/Louvain modularity are stated from general
  knowledge, not the verified pool.
- Provenance is a Claude deep-research run, not a single authored document; treat the verified-source
  citations (Section 9 of the note) as the durable backbone and the synthesis as Dannie's working view.

_Source: verbatim note at `raw/notes/coupling-research-note.md`. Run stats: 23 sources fetched, 25
claims adversarially verified (22 confirmed, 3 killed)._
