---
title: "Source: Dudycz — Archiving old events: slice streams per lifetime (LinkedIn)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [dudycz-archiving-events-stream-lifetime-slicing]
raw_file: [raw/notes/dudycz-archiving-events-stream-lifetime-slicing.md]
tags: [event-sourcing, operations, stream-lifetime, substrate]
---

# Source: Dudycz — Archiving old events: slice streams per lifetime (LinkedIn)

LinkedIn post by **[[oskar-dudycz]]**, part of his **#EventDrivenDiary** series. Raw capture:
`raw/notes/dudycz-archiving-events-stream-lifetime-slicing.md` — captured verbatim via **live logged-in
Chrome**; only edit is collapsing LinkedIn's `hashtag\n#x` markup.

**Two date caveats that must travel.** The stamp is **2026-08-28, accurate to the day, not the hour**
(derived from the relative age at retrieval), **and** the capture note records that it appeared in the
feed **as a self-repost, so the original may predate that date** — treat 2026-08-28 as the *repost* date,
not necessarily first publication. **Register:** PRACTITIONER GUIDANCE from client work, **not
measurement**.

## Summary

The post answers the objection that always follows a proposal to archive old events: someone in the room
says the domain has a long legal tail. His examples of the real cases: "we may want to verify the cashier
shift report and add corrections if, for example, cash was wrongly calculated"; "generate the invoice
correction if the initial one had wrong data"; "retrofit data that we got with a delay. Also some
entities just have a longer lifetime."

His answers, in order of increasing effort:

1. **Often, do nothing.** "Event stores usually scale well with the number of streams. If they're not
   actively accessed and are not long, then it's okay to keep them. Of course, as long as we have enough
   storage on disk."
2. **Archiving need not be uniform.** "You don't need to have a uniform archiving strategy for all. We
   can select different ones case by case" — keep longer-lived streams, or delay their archiving, via a
   multi-stream approach.
3. **Slice streams by lifetime.** "We can slice our streams per lifetime (e.g. bank account to accounting
   period, point of sales to cashier shifts etc.). We could even keep just the **last summary event**,
   archive the rest. Thanks to that we can keep only single event instead of multiple ones, and if we need
   to reopen or perform additional action, then we start **from the summary event instead of the full
   history**."

The payoff: "our event storage stops growing infinitely, which is a common concern for people starting
with Event Sourcing."

## Key points

- **Stream lifetime is a design axis, not an operational afterthought.** Choosing "bank account →
  accounting period" or "point of sale → cashier shift" as the stream grain is a *modelling* decision
  that determines whether archiving is ever possible.
- **Summary events are the hinge.** A closing summary event lets a stream be archived while leaving a
  resumable starting point — the same construct he treats as an integration/public event elsewhere
  ([[dudycz-backend-for-frontends-for-event-driven-apis]]), used here for lifecycle rather than
  integration.
- **"Keep streams short"** is presented as prior guidance from earlier diary chapters (uncaptured), of
  which this post is the exception-handling instalment.
- **The counter-argument he takes seriously** is regulatory/edge-case reopening, not storage cost — the
  storage concern is dispatched in a sentence.

## Connections / contrast

- **Answers the infinite-growth objection [[event-sourcing]] does not currently address.** The page
  covers snapshots as a non-authoritative optimisation (via
  [[atomicobject-cqrs-event-sourcing-production-walkthrough]]) but says nothing about archiving or stream
  lifetime. Note the distinction worth preserving: a **snapshot** is a performance device that leaves the
  history in place; a **summary event + archive** actually removes events from the hot store, and is
  therefore a modelling commitment with legal consequences.
- **In tension with the "keep everything forever" framing of the audit sources.**
  [[axoniq-government-ai-explainability-requirements]] argues public institutions "carry their history
  forward indefinitely" and that this is the architecture's selling point; Dudycz treats indefinite
  retention as a cost to be managed by slicing. Both can be right for different domains, but a page
  citing either should not present indefinite retention as a settled property of event sourcing.
- **Complements [[dudycz-fixing-bugs-in-event-sourcing]]** — which depends on old events still being
  there ("the 14 March events are still there"). Read together, they bound each other: archive by
  lifetime, but understand that archiving is what removes the material a late correction would need. He
  does not draw that connection himself.
- Adjacent: [[event-versioning-and-upcasting]] (long-lived events are the other reason old data is
  awkward) · [[cqrs]] · [[dudycz-checklist-first-event-sourcing-feature]] (question 6, "Does the stream
  end?", is this post as a selection criterion).

## Limits

- **~300-word social post.** No mechanics: no archival storage target, no retrieval path for archived
  streams, no cost figures, no discussion of projections that span an archive boundary.
- **Nothing measured.** "Event stores usually scale well with the number of streams" is an unqualified
  generalisation across products — no store named, no numbers.
- **The legal cases are gestured at, not resolved**: nothing on retention mandates, erasure requests, or
  who signs off that an archived stream is still reachable within a statutory window.
- **Date is a repost date at best** (see caveat above), and the series chapters it builds on are not
  captured.

_Source: `raw/notes/dudycz-archiving-events-stream-lifetime-slicing.md`._
