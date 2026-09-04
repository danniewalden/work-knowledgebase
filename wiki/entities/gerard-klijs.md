---
title: Gerard Klijs
type: entity
created: 2026-09-04
updated: 2026-09-04
sources: [klijs-skilj-rust-dcb-library]
tags: [person, event-sourcing, dcb, rust, tooling]
---

# Gerard Klijs

Developer (`@GKlijs` on X) and author of **skilj**, a **Rust** library for event-sourced applications on
**PostgreSQL** that uses **[[dynamic-consistency-boundaries|Dynamic Consistency Boundary]] instead of the
classic aggregate pattern** — announced 2026-08-28 at **v0.0.1**
([[klijs-skilj-rust-dcb-library]]). His pitch: "No more sagas for rules that span two entities."

**Everything the KB knows about him comes from one two-tweet self-announcement**, so treat this page as a
stub. Three caveats travel with it:

- **VENDOR SELF-REPORT / author self-announcement** — the saga-elimination claim is a design pitch, not a
  demonstrated result, and **nothing about the library has been independently evaluated**.
- **v0.0.1**, "early days" by his own description; the post is a request for feedback "especially from
  anyone who's hit the aggregate-boundary problem before."
- **The capture's `source_url` is RECONSTRUCTED and unverified** (X returned the status link as
  blocked/base64 content); the handle, timestamps and text *are* observed. The repo path as tweeted,
  `codeberg.org/gklijs/SklilJ`, **does not match** the crate name `skilj` (`crates.io/crates/skilj`) —
  unresolved. **Resolve both before citing a URL.**

In the KB he matters only as a signal that the **DCB store contract is spreading beyond the JVM
([[axoniq]]'s Axon Framework 5) and .NET ([[critter-stack]]'s Marten 9.0)** — a much weaker signal than
either. Notably, the capture says nothing about the concurrency contract
([[fritzsche-ccc-atomic-append-serialized-write-order|serialized write order]]), which is where an
evaluation of a Postgres-backed DCB library should start.

**Nothing else about him is evidenced.** No employer, location, role or history appears in the capture,
and none is asserted here.

## Related

[[dynamic-consistency-boundaries]] · [[event-sourcing]] · [[sara-pellegrini]] ·
[[command-context-consistency]]

_Source pages: [[klijs-skilj-rust-dcb-library]]._
