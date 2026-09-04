---
title: Coupling Taxonomy (the coupling landscape)
type: concept
created: 2026-06-22
updated: 2026-07-31
sources: [coupling-research-note, devadoss-cead-capability-aligned-agent-design]
tags: [coupling-cohesion, software-design, modularity, substrate, agentic-ai]
---

# Coupling Taxonomy (the coupling landscape)

A map of the main ways the field has tried to **name and grade coupling** between software parts, and
where each one fits (or doesn't) as a model for **edge weights on a capability/user-needs graph**.
Assembled from the [[coupling-research-note]]. The modern recommendation for this KB's product context
lives in [[balanced-coupling]]; this page is the surrounding landscape.

## 1. Classical — Stevens / Myers / Constantine (1974)

The original coupling taxonomy. [[larry-constantine|Larry Constantine]] developed it in the mid-1960s,
first presented at the 1968 National Symposium on Modular Programming, and it was widely cited in
Stevens, Myers & Constantine, **"Structured Design," *IBM Systems Journal* 13(2), May 1974** (DOI
10.1147/sj.132.0115). Yourdon & Constantine's *Structured Design* (1979) formalized coupling as

> "the measure of the strength of interconnection" — "the more we must know of module B to understand
> module A, the more closely connected A is to B."

Six levels, **strongest/worst → weakest/best**:

| # | Level | Definition |
|---|---|---|
| 1 | **Content** | One module modifies/references another's internals (jumps into private code, alters local data). |
| 2 | **Common** | Modules share a global data region (shared writable globals). |
| 3 | **External** | Modules share an externally imposed data format / protocol. |
| 4 | **Control** | One module passes flags/switches that direct another's flow. |
| 5 | **Stamp** | Modules share a composite data structure but use only a subset. |
| 6 | **Data** | Modules share only the elementary data they actually need. |

Foundational vocabulary, but **intra-program module connection** — pre-distributed-systems. A historical
anchor, *not* a viable edge-weight scheme for a capability graph (vocabulary mismatch). Its strongest
level (content) maps to Khononov's **Intrusive** strength.

## 2. Modern — Khononov (2024)

[[balanced-coupling|Balanced Coupling]]: three dimensions (**Integration Strength × Distance ×
Volatility**) plus a numeric balance formula. The **direct fit** for software-boundary placement
(bounded contexts, services, modules) and the model this KB recommends. Full treatment on its own page.

## 3. Team-shaped — Team Topologies (2019)

[[team-topologies|Team Topologies]] grades not edges but **interaction modes** (Collaboration /
X-as-a-Service / Facilitation) and supplies *partition-side constraints* (cognitive load, the
Independent Service Heuristics). No edge scale; relevant when a boundary is read as "a team."

## 4. Telemetry-derived — change coupling (Tornhill / CodeScene)

**Change-coupling** (a.k.a. logical/temporal coupling): files/modules that **change together** in
version control, regardless of static dependency. Continuous, VCS-mineable (same commit / same
author-window / shared ticket id) — see [[adam-tornhill]] and
[[tornhill-hidden-design-decisions-control-coupling]]. Because it is *measured*, not judged, it is the
**wrong shape** for an editor-dial product: asking a human to estimate it is a category error. Its
judgment-based analog is Khononov **Volatility-coupling**.

## Adjacent measurement frameworks (context, not edge-weight candidates)

- **Martin's instability metric.** `I = Ce / (Ca + Ce)`, where `Ca` is afferent (incoming) and `Ce`
  efferent (outgoing) coupling. A per-*component direction* metric — useful for diagnosis ("which
  capabilities are most depended-upon") but not an edge weight.
- **Newman / Louvain modularity (graph partitioning).** *Objective functions* that tell you **how** to
  partition a weighted graph — not **what the weights should mean**. Built for large sparse graphs; on
  the 10–15-node graphs typical of one user-needs map the optimal partition is often visually obvious
  and the algorithm's confidence sits near the noise floor.

> Caveat: Martin's instability and Newman/Louvain are stated from general knowledge in the research run,
> **not** from its verified-claim pool. Treat as context.

## Side-by-side

| | Stevens/Myers/Constantine 1974 | [[balanced-coupling\|Khononov 2024]] | [[team-topologies\|Team Topologies 2019]] | Change-coupling (Tornhill) |
|---|---|---|---|---|
| Scale | 6 ordinal levels | 4-level strength + distance + volatility | categorical interaction modes (no edge scale) | continuous co-change frequency |
| Scope | intra-program modules | components / services / systems | teams & the architectures they shape | files/modules in a VCS |
| Distance? | no | yes | implicit (handover chains) | no |
| Volatility? | no | yes (via DDD subdomain) | no | implicit (co-change rate) |
| Quantitative? | qualitative ordinal | yes (numeric balance) | no | yes (mineable) |
| How obtained | static analysis + reading internals | editor judgment + observable distance | Likert survey + ISH checklist | VCS-mineable |
| Fits capability-map edges? | vocabulary mismatch | **direct fit** | constraint-side, not edge | wrong shape (telemetry) |

## Agent-era note — "agent sprawl = distributed monolith"

The classic **distributed monolith** — microservices decomposed without discipline, so nominally
independent services must change together through shared structures — reappears one tier up with AI
agents. [[john-devadoss|deVadoss's]] **CEAD** ([[devadoss-cead-capability-aligned-agent-design]]) names
**micro-agent proliferation** as the "most likely enterprise anti-pattern": many prompt-wrapped agents
with duplicated capabilities, unclear ownership, unnecessary handoff/latency chains, inconsistent tool
permissions, and cascading errors where "one agent's confident mistake becomes another agent's input."
In coupling terms this is high **Integration Strength** across a long **Distance** on **Volatile** parts
— the worst quadrant of [[balanced-coupling|Khononov's]] model — and his simulation shows it degrading
sharply past ~16–32 agents. The prescription is the coupling/cohesion one restated for agents: decompose
only around durable **[[business-capabilities|capability]]** boundaries with distinct ownership, data,
and evaluation. The microservices→monolith backtracking literature CEAD cites is the same lesson from the
service tier.

## Related

[[balanced-coupling]] · [[team-topologies]] · [[larry-constantine]] · [[vlad-khononov]] ·
[[adam-tornhill]] · [[business-capabilities]] · [[domain-driven-design]] · [[conways-law]] ·
[[locality-of-reference]] · [[multi-agent-orchestration]] ·
[[devadoss-cead-capability-aligned-agent-design]] · [[coupling-research-note]]

_Sources: [[coupling-research-note]] · [[devadoss-cead-capability-aligned-agent-design]]._
