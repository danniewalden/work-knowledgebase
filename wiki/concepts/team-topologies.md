---
title: Team Topologies
type: concept
created: 2026-06-22
updated: 2026-07-31
sources: [coupling-research-note, skelton-team-topologies-foundation-ai-roi]
tags: [software-design, organization, coupling-cohesion, business-capabilities, conways-law, agentic-ai, focus]
---

# Team Topologies

**Team Topologies** (Matthew Skelton & Manuel Pais, IT Revolution, 2019) is an organizational-design
model for software teams. Its relevance to this KB, via the [[coupling-research-note]], is as the
**partition-side** lens on boundaries — what makes a boundary a good *team* boundary — as opposed to the
edge-side coupling models in [[coupling-taxonomy]] / [[balanced-coupling]]. It offers **no edge weights**
and is not the default lens for software-model boundaries, but it applies when an editor reads a boundary
as "a team."

## The pieces that bear on boundary design

**Interaction modes** — three ways teams relate: **Collaboration**, **X-as-a-Service**, and
**Facilitation**. These are categorical interaction *modes*, not a graded edge scale.

**Cognitive load** — a team should own only as much as it can hold in its head. Operationalized via a
**Team Cognitive Load Assessment** (a Likert survey). This is a *partition-side constraint* (does this
boundary overload the team?), not a property of an edge. A common quota: roughly **≤1 complex OR ≤1
complicated domain per team**.

**Independent Service Heuristics (ISH)** — a yes/maybe/no checklist for whether a candidate boundary is
a good **stream-aligned** boundary. Its real anchors are **autonomy and self-containment** — *"Could this
run as a SaaS / separate business?"* and *"Could the team act independently?"* — a partition-side
**validator**, not a cognitive-load test (see caveat).

## How it fits the coupling work

For the user-needs-map's edge-weighting feature, Team Topologies sits on the **constraint** side, not the
**edge** side: cognitive load and ISH validate or constrain a *candidate partition* after boundaries are
drawn; they don't tell you what a dependency edge between two capabilities is worth. This is the same
distinction that puts Khononov's **Distance** on the partition side rather than the edge side
([[balanced-coupling]]). It connects to [[conways-law]] (teams and architecture take the same shape) and
to [[business-capabilities]] (a capability as a team-ownable, self-contained unit).

## Agent-era extension — value-flow teams as agent boundaries (Skelton, 2026)

Co-author **[[matthew-skelton]]** applies Team Topologies directly to AI in
[[skelton-team-topologies-foundation-ai-roi]] (2026-07-04), reading the **2026 DORA ROI report**. The
argument: **AI is an amplifier** — it magnifies a high performer's strengths and a struggling org's
dysfunctions alike — so ROI comes from the *organizational system* (platform quality, workflow clarity,
team alignment), not the tools. The new claim for this KB is that a **stream-aligned, value-flow team
boundary doubles as an agent boundary**: a team with end-to-end responsibility for a flow of value gives
autonomous agents "clear objectives and anchoring points … to understand what to build and how." This is
the [[conways-law]] homomorphic force in the agent era — the same boundary that shapes team
communication also scopes an agent.

Two further moves matter here:
- **Data (and platforms) as a product, for humans *and* agents.** DORA's "AI-accessible data ecosystems
  with clean, domain-aligned APIs," stewarded by the team that owns the service, so context is
  "digestible for both human engineers and AI agents" — the platform/enabling-team pattern extended to
  make a capability's data legible to agents ([[agent-legibility]]).
- **Automating the verification tax.** AI-amplified output volume creates a heavy review burden (DORA's
  "J-Curve" dip); the fix is to move specialists out of manual review and into **enabling / platform
  teams** that provide automated testing and validation *as a service* (a "complicated subsystem") —
  the organizational analog of CEAD's verifier gates ([[agent-governance]]).

This is the organization-side mirror of [[john-devadoss|deVadoss's]] architecture-side
capability-before-agent thesis ([[devadoss-cead-capability-aligned-agent-design]]): both put the durable
value/capability boundary before the tooling. It also gives this concept a **named author** for the
first time (previously ingested only via the [[coupling-research-note]]).

## Caveats (from the research-run verification)

- The Dunbar-style **group-size cutoffs** (~5 / ~15 / ~50 / ~150) were claimed as *hard upper bounds*;
  **refuted 0-3**. Treat as heuristics, not constraints.
- **ISH** was claimed as a *bounded-cognitive-load* criterion; **refuted 0-3**. Its actual anchors are
  autonomy and self-containment, per above.

## Related

[[coupling-taxonomy]] · [[balanced-coupling]] · [[conways-law]] · [[business-capabilities]] ·
[[domain-driven-design]] · [[matthew-skelton]] · [[devadoss-cead-capability-aligned-agent-design]] ·
[[agent-legibility]] · [[agent-governance]] · [[coupling-research-note]]

_Sources: [[coupling-research-note]] · [[skelton-team-topologies-foundation-ai-roi]]._
