---
title: "Source: Klijs — skilj, a Rust DCB library for event-sourced apps on Postgres"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [klijs-skilj-rust-dcb-library]
raw_file: [raw/notes/klijs-skilj-rust-dcb-library.md]
tags: [event-sourcing, dcb, rust, tooling, substrate]
---

# Source: Klijs — skilj, a Rust DCB library for event-sourced apps on Postgres

Two-tweet X thread by **Gerard Klijs** (`@GKlijs`), 2026-08-28, announcing his own library. Raw capture:
`raw/notes/klijs-skilj-rust-dcb-library.md` — captured verbatim via live logged-in Chrome from an X
timeline search (`"dynamic consistency boundary" OR #eventsourcing`, live tab); both tweets were short
and captured whole.

**Two warnings from the capture note, both of which must travel with any citation of this page.**

1. **The `source_url` is RECONSTRUCTED, not observed.** X's DOM returned the first tweet's status link as
   blocked/base64 content, so the numeric status id in the raw frontmatter is **not verified**. The
   author handle, the two timestamps (2026-08-28T20:42:21Z and :22Z) and the text **are** observed.
   **Resolve the real permalink before citing this as a URL.**
2. **VENDOR SELF-REPORT / author self-announcement.** This is the library's author announcing his own
   library at **v0.0.1**. The headline capability claim is his design pitch, not a demonstrated result,
   and **nothing here has been independently evaluated.**

## Summary

**skilj** is a newly open-sourced **Rust** library for event-sourced applications on **PostgreSQL** that
uses **[[dynamic-consistency-boundaries|Dynamic Consistency Boundary]] instead of the classic aggregate
pattern**. The pitch is one sentence: **"No more sagas for rules that span two entities"** — i.e. the
DCB selling point (a decision's consistency scope can span what would have been several aggregates,
without orchestration) delivered as a Rust crate. It is explicitly **"Early days (0.0.1)"** and the post
is a request for feedback, "especially from anyone who's hit the aggregate-boundary problem before."

## Key points

- **Stack:** Rust, PostgreSQL as the event store. Repo and crate links as tweeted:
  `codeberg.org/gklijs/SklilJ` and `crates.io/crates/skilj`. **Note the casing/spelling of the repo path
  as tweeted (`SklilJ`) does not match the crate name `skilj`** — transcribed as tweeted, unresolved.
- **Positioning:** DCB *in place of* aggregates, not alongside them — the "Kill Aggregate" line
  ([[sara-pellegrini]]) taken as the library's premise.
- **The claim being made** is about eliminating **sagas for cross-entity rules**. That is the same payoff
  [[axoniq]] advertises for Axon Framework 5 — in AxonIQ's own words, "enforcing business rules
  atomically across multiple entities without complex Saga orchestration"
  ([[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]], **VENDOR SELF-REPORT**) —
  and it is equally unquantified in both places.
- **Maturity:** v0.0.1, author-stated. No users, benchmarks, production reference, or third-party review
  in the capture.

## Connections / contrast

- **Widens the DCB implementation landscape beyond the JVM and .NET.** [[dynamic-consistency-boundaries]]
  currently names Axon Framework 5 (JVM, [[axoniq]]) and Marten 9.0 ([[critter-stack]], PostgreSQL
  HSTORE) as the canonical implementations. skilj adds a **Rust** entry on the same substrate
  (PostgreSQL), which is a small signal that the DCB *store contract* is spreading across ecosystems —
  but a v0.0.1 personal project is a far weaker signal than either of those.
- **What it does not settle.** The hard part identified by
  [[fritzsche-ccc-atomic-append-serialized-write-order|Fritzsche]] — that an atomic conditional append is
  insufficient without a **serialized write order** under READ COMMITTED — is exactly the kind of thing
  a new Postgres-backed DCB library has to get right, and the capture says nothing about it. Anyone
  evaluating skilj should start there.
- Also adjacent: [[pellegrini-dcb-tag-dilemma]] (what a tag is, from DCB's originator),
  [[command-context-consistency]], [[event-sourcing]], [[enzler-event-sourcing-aggregates-dcb-or-what]]
  (the "you may need neither" counterweight).
- **New entity.** Gerard Klijs has no entity page in the KB yet; proposed in the batch deltas.

## Limits

- **Nothing is evaluated.** v0.0.1, author self-announcement, no measurement, no independent use. Do not
  cite this as evidence that DCB-instead-of-aggregates works in Rust — only that someone has published a
  library that attempts it.
- **The URL is unverified** (see warning 1) and the **repo path spelling is inconsistent** with the crate
  name; both need resolving before this page is used as a reference.
- Short-form social post: no design detail, no API surface, no discussion of the concurrency contract.

_Source: `raw/notes/klijs-skilj-rust-dcb-library.md`._
