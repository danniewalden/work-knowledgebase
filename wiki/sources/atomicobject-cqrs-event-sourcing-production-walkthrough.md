---
title: "Atomic Object — CQRS and Event Sourcing in TypeScript: A Production Walkthrough"
type: source
created: 2026-06-17
updated: 2026-06-17
sources: [atomicobject-cqrs-event-sourcing-production-walkthrough]
raw_file: [raw/articles/atomicobject-cqrs-event-sourcing-typescript-production-walkthrough.md]
tags: [event-sourcing, cqrs, projections, production, substrate]
---

# Atomic Object — CQRS and Event Sourcing in TypeScript: A Production Walkthrough

Blog post by **Vlad Surganov** (Atomic Object / Atomic Spin), 2026-06-04. Captured verbatim at
`raw/articles/atomicobject-cqrs-event-sourcing-typescript-production-walkthrough.md`. The first
concrete *how-it-looks-in-production* source on the [[event-sourcing]] / [[cqrs]] substrate.

## What it says

A no-toy-code tour of [[cqrs]] + [[event-sourcing]] + projections in a real stack: NestJS +
@nestjs/cqrs, **KurrentDB** (formerly EventStoreDB) as the event log, PostgreSQL + Drizzle on the read
side, and projections as the bridge. One-paragraph thesis: CQRS separates read and write models;
event sourcing stores the *sequence of facts* not current state; **projections translate the fact
stream into whatever read shapes the UI wants.**

Key points:
- **Commands are intents, not payloads** — `ApproveOrganization`, not `PATCH status=approved`; a
  well-named command set is "an executable glossary of the domain."
- **The aggregate is a state machine** — states are real objects accepting different commands; the
  TypeScript type system enforces *exhaustiveness* (`satisfies`, `.exhaustive()`) so impossible states
  and unhandled events fail at compile time.
- **Events are the source of truth** — appended with optimistic concurrency; in-memory state is a
  cached fold; **snapshots** are a performance optimization, never authoritative ("caches are allowed
  to lie").
- **Projections** maintain a "mercifully boring" relational read model; `startFrom: 'start'` makes read
  models **rebuildable**; offset + read-model write share one transaction.
- **Production details tutorials skip:** PostgreSQL **advisory locks** for per-entity serialization
  (cheap alternative to distributed locks); **upcasters** + per-event `SCHEMA_VERSION` for event
  evolution ("install versioning on day one"); **idempotency** because persistent subscriptions deliver
  at-least-once ("duplicates are Tuesday"); **two flavors of projection** — transactional read-model
  vs. async side-effect; correlation IDs give an audit trail "for free."
- **Honest costs:** more code; eventual consistency; harder cross-aggregate queries; real onboarding
  ramp. Worth it when the domain is "eventful" (finance, compliance, healthcare, logistics) or when you
  will need read models you haven't imagined yet.

## Why it matters here

Fills a gap noted in the watch: the KB had the *theory* of [[event-sourcing]]/[[cqrs]] and the
[[dynamic-consistency-boundaries|DCB]] debate, but no grounded production reference. Its
"aggregate is a consistency boundary; keep it small; solve cross-aggregate work with async projections,
not bigger aggregates" advice is the conventional counterpoint to the [[dynamic-consistency-boundaries]]
"kill the aggregate" line ([[pellegrini-dynamic-consistency-boundary]],
[[dilger-dcb-is-what-event-sourcing-should-have-been]]). The exhaustiveness-via-types and
rebuildable-read-models points also rhyme with the agent-legibility/maintainability thread
([[agent-legibility]], [[fowler-bockeler-maintainability-sensors]]).

## Caveats

Vendor/consultancy blog (secondary), one team's stack and conventions; descriptive, not empirical.
