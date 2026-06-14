---
title: Domain-Driven Design (DDD)
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [semaphore-dymitruk-event-modeling]
tags: [ddd, software-design, methodology]
---

# Domain-Driven Design (DDD)

A software development approach that **matches code components to the business/application
domain** and unifies the language of domain experts and developers so terminology stays
consistent within each area.

## Relationship to Event Modeling

Per [[adam-dymitruk]] ([[semaphore-dymitruk-event-modeling]]), [[event-modeling]] represents
DDD on the blueprint through **swimlanes** — arranged to separate physical systems and
logical subsystems while preserving each area's subject-matter language (e.g. inventory vs.
invoicing). This connects to the step in event modeling where [[conways-law|Conway's Law]] is
applied to give teams ownership of autonomous parts of the system.

## Related

[[event-modeling]] · [[event-sourcing]] · [[business-capabilities]] (capabilities as stable
boundaries — a sibling lens to bounded contexts) · [[open-closed-principle]] · [[event-storming]] ·
[[conways-law]]

_Source pages: [[semaphore-dymitruk-event-modeling]]._
