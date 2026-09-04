---
title: "Rico Fritzsche — Autonomous Domain Capabilities & Command Context Consistency"
type: source
created: 2026-06-15
updated: 2026-06-15
sources: [rico-fritzsche-autonomous-domain-capabilities-ccc]
raw_file: [raw/notes/rico-fritzsche-autonomous-domain-capabilities-ccc.md]
tags: [business-capabilities, vertical-slice-architecture, event-sourcing, agentic-coding, ddd, focus]
---

# Rico Fritzsche — Autonomous Domain Capabilities & Command Context Consistency

LinkedIn post by **[[rico-fritzsche]]** (2026-06-08; captured 06-15 via logged-in Chrome).
A longer Medium version is linked in the post's first comment and is **not yet captured**.
Source file: `raw/notes/rico-fritzsche-autonomous-domain-capabilities-ccc.md`.

## What it argues

AI coding agents now generate and change code so fast that an old structural weakness is exposed:
**most architectures give a domain capability no clear "home."**

- **Layered (Clean / Hexagonal) splits a capability across technical ownership boundaries** — request
  handling, application layer, repositories, mappings, shared domain structures all participate in one
  capability. Repositories are the worst offenders: they become shared access points for many unrelated
  capabilities, so behavior isn't local and must be reconstructed from the architecture.
- **[[vertical-slice-architecture|Vertical Slice]] improves visibility** by making Commands and Queries
  explicit and moving code closer to the request — but the deeper ownership problem remains *when the
  handler still depends on shared domain models, shared repositories, or aggregate structures*. The
  slice becomes a local entry point into a larger shared structure rather than the place the capability
  fully owns its processing.

His framing question: *if software is used through Commands and Queries, why attach those interactions
to a centralized object model?*

## The proposal — Autonomous Domain Capabilities + CCC

- A Command doesn't need routing into a shared object model to mean something. It can **define the facts
  it needs, build a local context from those facts, make a decision, and produce consequences.** A Query
  does the same for reading: define facts → derive a projection → return a result.
- This is **Command Context Consistency (CCC)**: each capability is realized by a **Request Processing
  Unit (RPU)** that builds its own context, makes its own decision, and keeps behavior local.
- **Recorded facts (events) are the Application State, but they are not the domain by themselves.** The
  domain becomes visible through the *capabilities* that interpret those facts and produce new ones:
  *domain = recorded state + the capabilities that know how to work with it.*
- Result: behavior, ownership, and change all stay **local to the capability**. (Diagram: an outer ring
  of RPUs around a central "Application State (Recorded Events)" core, the whole labelled "Domain.")

## Why it matters here

This is the sharpest statement in the KB of *why [[business-capabilities]] are the right boundary in
the agent era* — and it ties three focus threads together at once: capability-as-boundary,
[[vertical-slice-architecture]] (and where VSA still leaks ownership), and [[event-sourcing]] (recorded
events as application state). The RPU is effectively a capability-scoped, event-sourced slice with **no
shared object model** — a natural unit for [[event-modeled-agent-design|agent ownership]] (contracted
blast-radius, build context from the log, decide, emit). It rhymes closely with **[[sara-pellegrini]]**'s
[[dynamic-consistency-boundaries|DCB]] (build the decision's context from the relevant events, not from
an aggregate) and with **[[yves-goeleven]]**'s capability-swimlane Event Modeling.

## Caveats

LinkedIn-length argument; the worked detail is in the uncaptured Medium article. CCC/RPU is
Fritzsche's own coinage, not (yet) an established pattern with independent adoption — assertion-level,
but a clean articulation of a direction multiple practitioners are converging on.

## Touches

[[rico-fritzsche]] · [[business-capabilities]] · [[vertical-slice-architecture]] · [[event-sourcing]] ·
[[dynamic-consistency-boundaries]] · [[agentic-coding]] · [[event-modeled-agent-design]] ·
[[domain-driven-design]] · [[cqrs]]

_Source: `raw/notes/rico-fritzsche-autonomous-domain-capabilities-ccc.md`._
