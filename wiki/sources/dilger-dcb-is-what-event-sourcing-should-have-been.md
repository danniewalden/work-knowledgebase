---
title: "Martin Dilger — DCB is event sourcing what it always should have been"
type: source
created: 2026-06-15
updated: 2026-06-15
sources: [dilger-dcb-is-what-event-sourcing-should-have-been]
raw_file: [raw/notes/dilger-dcb-is-what-event-sourcing-should-have-been.md]
tags: [event-sourcing, dcb, naming, focus]
---

# Martin Dilger — DCB is event sourcing what it always should have been

Short LinkedIn post by **[[martin-dilger]]** (2026-06-15; captured same day via logged-in Chrome).
Source file: `raw/notes/dilger-dcb-is-what-event-sourcing-should-have-been.md`.

## What it says

A naming provocation about **[[dynamic-consistency-boundaries|Dynamic Consistency Boundaries]]**:

- People complain "Dynamic Consistency Boundaries" is a complex, un-marketable technical term — and
  Dilger agrees.
- His point: we already *had* a good name for what DCB describes — **"Event Sourcing."** DCB is event
  sourcing done the way it always should have been.
- The thing that actually deserved a qualifying name is the **aggregate-based approach** people
  struggle with — call *that* "**Static Consistency Boundaries**." Framed as a choice: would you rather
  work with "Static Consistency Boundaries" or with "Event Sourcing"?
- Aside: **DCB gets a prominent place in the 2nd edition of his book *"Understanding Eventsourcing."***

## Why it matters here

A primary practitioner voice reframing the DCB-vs-aggregate debate on the [[event-sourcing]] /
[[dynamic-consistency-boundaries]] substrate thread: it casts the **aggregate as the special case**
(a *static* boundary) and per-decision DCB as the default, un-named-until-now norm. Useful context for
why the [[sara-pellegrini|"Kill Aggregate"]] line of thinking is gaining traction, and a pointer to
where the canonical treatment is heading (the 2nd edition of his book). Pairs directly with
[[pellegrini-dynamic-consistency-boundary]] (the origin/naming source already ingested) and rhymes with
[[rico-fritzsche-autonomous-domain-capabilities-ccc|Fritzsche's]] "build context from recorded facts,
not a shared object model."

## Caveats

Opinion-length naming take, not a technical argument; Dilger has a commercial interest (his book). The
"Static Consistency Boundaries" coinage is rhetorical, not an adopted term.

## Touches

[[martin-dilger]] · [[dynamic-consistency-boundaries]] · [[event-sourcing]] · [[sara-pellegrini]] ·
[[pellegrini-dynamic-consistency-boundary]]

_Source: `raw/notes/dilger-dcb-is-what-event-sourcing-should-have-been.md`._
