---
title: Business Capabilities
type: concept
created: 2026-06-14
updated: 2026-06-14
sources: [homann-business-oriented-foundation-service-orientation, goeleven-event-model-to-code-series, goeleven-event-sourcing-not-auditing-for-free, daniel-event-modeling-and-wardley-mapping]
tags: [business-capabilities, coupling-cohesion, ddd, event-modeling, architecture, focus]
---

# Business Capabilities

A **business capability** is *what* an organization is able to do — a stable, outcome-oriented ability
(e.g. "Booking", "Payments", "Catalog Management") — independent of *how* it's currently realized
(the process, org chart, or technology). Capability-based design uses these as the **long-term-stable
boundaries** around which you organize processes, teams, and software. A focus-area concept for Dannie
(flagged important, 2026-06-14).

## Primary definition (Homann, 2006)

The seminal source is **[[ulrich-homann]]**'s *A Business-Oriented Foundation for Service Orientation*
([[homann-business-capabilities]]), the most-cited origin of capability mapping (referenced by the
BIZBOK Guide):

- A **business capability** is "a particular ability or capacity that a business may possess or
  exchange to achieve a specific purpose or outcome" — it describes *what* the business does (outcomes
  + service levels) and **encapsulates** people, process, technology and information.
- A capability is a **"black box"**: external, observable, measurable behavior with defined
  inputs/outputs and a contracted **service-level expectation**; the internal "how" is irrelevant at
  this level. (This is why capabilities map onto services — and onto agent boundaries.)
- **Capability connectors** link capabilities and carry rich semantics (information exchange +
  control/policy). Homann's striking claim: discovering the *connections* "may be as valuable as
  defining the capabilities" — you manage change through connectors while the black boxes stay stable.
- A **business capability map** is a **nested taxonomy** (L1 Foundation: Operations vs Environmental →
  L2 Capability Groups → L3…n Business Capabilities), spanning the whole value network. **Process ≠
  capability:** process is the implementation of the capability blueprint at a point in time.

## Why capabilities make good boundaries

The core argument is **coupling and cohesion**: *how* a business does something changes often (process
tweaks, reorgs, new tech), but *what* it does is far more stable. Drawing boundaries around the stable
"what" means change tends to stay **inside** one capability instead of rippling across many — high
cohesion within, low coupling between. This is the same instinct behind [[domain-driven-design]]'s
**bounded contexts**, [[conways-law]] (teams own capabilities, so the architecture mirrors a sensible
org structure), the [[open-closed-principle]] (extend a capability without modifying others), and
[[vertical-slice-architecture]] (features cut vertically through a capability, not across layers).

## In this KB — Goeleven's capability-centric Event Modeling

[[yves-goeleven]] is the KB's clearest practitioner of capability-based design
([[goeleven-event-model-to-code-series]]):

- In an [[event-modeling|Event Model]], the **bottom swimlanes are business capabilities** (top
  swimlanes are roles). Capabilities are "the long-term stable boundaries within which part of the
  business process gets performed."
- **Decisions are owned by the capability, not the individual** — a business decision is recorded as
  an event inside the capability swimlane "even when the decision is taken in the mind of an authorized
  person." Different roles may be *authorized* to take it, but ownership belongs to the capability.
- Humans send **intent (commands)** to a capability; the capability reports back **state (read
  models/projections)** derived from its own decisions. Each capability is realized differently per
  org.
- **Contract between capabilities is required:** a capability's *internal* events should not double as
  integration events with other capabilities — otherwise you couple them as tightly as a shared
  database (the Dragan Stepanović exchange). Integration needs an explicit, owned contract (event,
  state, or UI). This is the crisp coupling/cohesion rule of the approach.
- Each capability's event stream also gives a per-process **audit** when enriched with
  who/when/where/what/why ([[goeleven-event-sourcing-not-auditing-for-free]]).

## Relation to the focus (agents)

Stable capability boundaries are a natural unit for **agent ownership and autonomy**: an agent (or
multi-agent group) can own a capability, act through its commands, and emit/consume its events — the
same "agent as user/processor on a swimlane" mapping as [[event-modeled-agent-design]]
([[dymitruk-event-modeling-future-proof-agents]]). Capabilities give agents a contracted blast-radius;
cf. the legibility/contract themes in [[harness-engineering]] and the [[agentic-event-driven-systems]]
"agents subscribe→reason→publish, never call each other directly" pattern.

## Strategy lens — capabilities × Wardley Mapping

Capabilities tell you the stable *what*; [[wardley-mapping]] tells you how each capability is
**evolving** (Genesis → Custom → Product → Commodity) and therefore how to treat it strategically
(build vs buy, differentiating vs utility). **Chris Daniel**'s *Event Modeling and Wardley Mapping*
series ([[daniel-event-modeling-wardley-mapping]]) frames the trio: **Wardley** = where to go and why;
**capabilities** = the stable units; **[[event-modeling]]** = what to build (the concrete design).
Adam Dymitruk has also referenced the EM × Wardley connection.

## Lineage / provenance

- **Primary, now captured:** [[ulrich-homann]] 2006 ([[homann-business-capabilities]]) — the
  capability-mapping foundation (cited by the BIZBOK Guide). Earlier business-architecture /
  capability-based-planning lineage and **DDD strategic design** (bounded contexts, subdomains) sit
  alongside it.
- **Practitioner application:** [[yves-goeleven]] ([[goeleven-event-model-to-code-series]]) — capability
  swimlanes in Event Modeling; the "contract between capabilities" coupling rule.
- *To capture next:* a primary from **Simon Wardley** (the *Wardley Maps* book/blog); a transcript of
  the Daniel series; Dymitruk's EM × Wardley talk; and a BIZBOK-level treatment of capability maps.

_Sources: [[homann-business-capabilities]] · [[goeleven-event-model-to-code-series]] · [[goeleven-event-sourcing-not-auditing-for-free]] · [[daniel-event-modeling-wardley-mapping]]._

_Sources: [[goeleven-event-model-to-code-series]] · [[goeleven-event-sourcing-not-auditing-for-free]]._
