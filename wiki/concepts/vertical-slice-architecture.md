---
title: Vertical Slice Architecture (VSA)
type: concept
created: 2026-06-14
updated: 2026-06-14
sources: [bogard-vertical-slice-architecture]
tags: [vertical-slice-architecture, cqrs, ddd, architecture, focus]
---

# Vertical Slice Architecture (VSA)

**Concept stub** (added 2026-06-14 when Dannie broadened the focus to the Event Modeling design
substrate). VSA organizes code **by feature/request instead of by technical layer**: each "slice"
encapsulates all concerns front-to-back for one request. Named by **[[jimmy-bogard]]**
([[bogard-vertical-slice-architecture]], 2018), emerging from a move off onion/layered architecture
toward [[cqrs]].

## The idea

"**Minimize coupling between slices, and maximize coupling in a slice.**" Remove the gates/barriers
between layers and couple along the **axis of change** — when you add a feature you touch UI, model,
validation, persistence for *that* slice, not a horizontal layer shared across features. Shared
abstractions (repositories/services/controllers) largely melt away; each slice picks its own
implementation, starting simple (Transaction Script) and refactoring as code smells appear. Splitting
requests into command vs. query means VSA "gives [[cqrs]] out of the gate." Caveat (Bogard): it
assumes a team fluent in refactoring and knowing when to push logic into the domain.

## Where it sits / why it's in the focus

- **Event Modeling fit (the key link).** Event Modeling builds a system as **vertical slices** of a
  feature (a UI→command→event→read-model path), each with its own Given-When-Then — the same
  feature-not-layer decomposition VSA names. The KB's focus material already leans on this: in
  [[jwilger-agent-skills-event-modeling]] the event model's **vertical slices + GWT** become the
  contract that governs an autonomous coding factory, and in
  [[dilger-model-is-a-living-spec-always-on-agent]] a "slice" placed in `planned` is the unit an agent
  picks up (generate tests → implement → PR). VSA is the architecture that those agent slices land in.
- **Substrate cluster.** Sits with [[event-sourcing]], [[cqrs]], [[domain-driven-design]] and
  [[open-closed-principle]] (new features *add* code rather than modify shared code — echoing Event
  Modeling's flat feature-cost curve).

## What's open / to capture next

A source explicitly mapping VSA slices to Event Modeling slices and to agent task units (Oskar Dudycz's
"Vertical Slices, CQRS, Semantic Diffusion" and the verticalslicearchitecture.com material are
candidates). This stub should grow as on-topic sources are ingested.

_Sources: [[bogard-vertical-slice-architecture]]._
