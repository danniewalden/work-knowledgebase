---
title: "Martin Dilger — Extending Event Modeling: an optional \"Query\" (WHEN) on the read side"
type: source
created: 2026-06-30
updated: 2026-06-30
sources: [dilger-extending-event-modeling-query-when]
raw_file: [raw/notes/dilger-extending-event-modeling-query-when.md]
tags: [event-modeling, given-when-then, cqrs, method-evolution, focus]
---

# Martin Dilger — Extending Event Modeling: an optional "Query" (WHEN) on the read side

LinkedIn post by **[[martin-dilger]]** (2026-06-29; captured 2026-06-30 via logged-in Chrome).
Source file: `raw/notes/dilger-extending-event-modeling-query-when.md`. Directly on the EM-method focus —
this is the **first change to the [[event-modeling]] method** captured in the KB.

## What it argues

Dilger frames this as significant: **the first time he deviates from the Event Modeling "Standard."**
Writing *Understanding Eventsourcing* he "completely stuck to" the standard — no new elements, just what
Adam Dymitruk defined — and built the [[eventmodelers-ai|Event Modelers Platform]] as "probably the
platform closest to the standard" (same colors, elements, so a reader of the book or Dymitruk's original
article "feels at home immediately"). He is a simplicity maximalist ("what is not strictly required can be
left out"), so he stresses he is adding this **"not lightheartedly."**

The change: an **optional WHEN on the read side, named "Query."** [[given-when-then|Given-When-Then]] on
the write side already carries a WHEN (GIVEN a user was registered / WHEN the user tried to register again
/ THEN error — users can only register once). For the read side he had "taught people for years to just
leave out the WHEN" — GIVEN a user was registered / THEN we expect this data to be available. The extension
adds an optional Query WHEN:

> GIVEN a user was registered / **WHEN we query with the user's email-address** / THEN we expect the user
> to be returned.

The motivation is **being able to express complex queries in scenarios** — you can now state *how* a read
model is interrogated, not just that its data exists.

## Provenance and stance

- It surfaced at the **first Event Modeling Conference (Munich)** — "it was clear something was missing…
  it came up in several discussions by independent people" ([[dilger-first-event-modeling-conference-munich-recap]]).
- By coincidence he had **already discussed the same with [[adam-dymitruk]]** beforehand.
- He is explicit that he **"wouldn't add this myself — I'm seeking feedback from everybody"**; it ships as
  **optional** on the platform, where feedback is "already positive, seems many people have been waiting."
- He notes he **recorded every piece of feedback from conference participants and has addressed every one**.
- It will feed a new section of his online course ("Implementing …").

## Why it matters here

Every prior Dilger capture treated the EM standard as fixed; this is the standard *evolving in public*,
through the conference he hosts, co-signed by the method's creator. For agent work the read-side Query
gives the read model an explicit, testable contract (the [[cqrs|CQRS]] query side gains a GWT of its own),
which fits the [[spec-driven-development]] / [[event-modeled-agent-design]] line that the model must be a
runnable spec — a query scenario is another acceptance gate an agent can generate tests from. Compare the
podcast's "Event Modeling 2.0" recasting of GWT ([[event-modeling]]) — method refinement is now a recurring
theme, not a one-off.

## Caveats

Short LinkedIn post; vendor context (his own platform, his own course). Proposed and optional, explicitly
pending community feedback — not (yet) a ratified part of the standard. No formal notation spec captured
beyond the one example.

## Touches

[[martin-dilger]] · [[event-modeling]] · [[given-when-then]] · [[cqrs]] · [[eventmodelers-ai]] ·
[[adam-dymitruk]] · [[dilger-first-event-modeling-conference-munich-recap]] · [[spec-driven-development]] ·
[[event-modeled-agent-design]]

_Source: `raw/notes/dilger-extending-event-modeling-query-when.md`._
