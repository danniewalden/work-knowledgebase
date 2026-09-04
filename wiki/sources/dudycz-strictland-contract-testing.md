---
title: "Oskar Dudycz — Announcing Strictland (contract testing for message compatibility)"
type: source
created: 2026-06-29
updated: 2026-06-29
sources: [dudycz-strictland-contract-testing]
raw_file: [raw/articles/dudycz-strictland-contract-testing-message-compatibility.md]
tags: [event-versioning-and-upcasting, event-sourcing, testing, cqrs, focus-substrate]
---

# Oskar Dudycz — Announcing Strictland

Blog post by **[[oskar-dudycz]]** (Event-Driven.io, 2026-06-15, CC BY-SA 4.0). Source:
`raw/articles/dudycz-strictland-contract-testing-message-compatibility.md`. Announces **Strictland**, a
JVM (Java/Scala/Kotlin) OSS **contract-testing library for message/event schema compatibility**.

## What it does

Deliberately smaller than Pact / Spring Cloud Contracts / Confluent Schema Registry: it **serializes a
message in an ordinary unit test and commits the output as a snapshot file** next to the code — no
broker, schema registry, mock service, or Docker. Two checks:

- **Snapshot check** (`thenContractIsUnchanged()`) — the message still serializes exactly as approved;
  a failure means the shape drifted (field renamed, date format switched, value added/dropped). The
  approved JSON lives in the repo, so any change shows up in a **normal PR diff**.
- **Compatibility check** — `thenBackwardCompatible()` confirms a newer version still reads what an
  older one wrote (stored events, already-sent requests); `thenForwardCompatible()` confirms a
  not-yet-upgraded reader still reads what the newer version writes (so you can ship the new shape
  before all readers catch up). Both compare shared fields and fail on a missing required field or a
  changed shared value.

Key discipline: **use your application's own serializer/`ObjectMapper`** so the snapshot is the exact
bytes you ship. Pre-1.0; .NET and TypeScript/JS ports planned. (Name: "Strickland," the strict enforcer
in *Back to the Future*, sibling to his Emmett toolkit.)

## Why it matters here

A concrete, low-ceremony tool for the [[event-versioning-and-upcasting]] problem: it catches breaking
schema changes at build time, in the same fast feedback loop and PR as the code that caused them —
relevant to the "explicit serialization / version your events" discipline on [[event-sourcing]] and the
broader substrate. Complements rather than replaces live consumer-driven contract testing (it checks the
serialized *shape*, not a running exchange). Snapshot-as-committed-file is the same instinct as approval
testing. Caveat: vendor self-announcement; pre-1.0, JVM-only for now.

## Touches

[[oskar-dudycz]] · [[event-versioning-and-upcasting]] · [[event-sourcing]] · [[cqrs]] ·
[[given-when-then]]

_Source: `raw/articles/dudycz-strictland-contract-testing-message-compatibility.md`._
