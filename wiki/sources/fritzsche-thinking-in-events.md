---
title: "Source: Fritzsche — Thinking in Events"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [fritzsche-thinking-in-events]
raw_file: [raw/articles/fritzsche-thinking-in-events.md]
tags: [event-modeling, event-sourcing, ddd, ubiquitous-language, substrate, focus]
---

# Source: Fritzsche — Thinking in Events

Article by **[[rico-fritzsche]]** (ricofritzsche.me, 2026-07-03), subtitled *"Separating the Modeling of
What Happened from the Decision of How to Store It."* Raw capture:
`raw/articles/fritzsche-thinking-in-events.md`. Unusually for this author it carries a **sources list**
(Dymitruk, Fowler, Azure Architecture Center, SE Radio's [[martin-dilger]] episode, plus Booking.com and
Airbnb help pages used as evidence of real domain vocabulary).

**Register:** an explanatory/definitional essay rather than a position paper — the most conventional
piece in this batch. No measurement, and none claimed.

## Summary

The article's job is one distinction: **[[event-modeling]] is a modeling discipline;
[[event-sourcing]] is an implementation choice, and confusing them "turns a useful way of thinking into
another technical prescription."** Thinking in events does *not* require an event store.

The diagnosis is linguistic. Projects fail not because a team cannot persist data but because "a business
situation is translated into technical structure too early" — "a conversation about reservations,
availability, guests, hosts, payments, stays, and cancellations slowly turns into records, fields, flags,
status columns, handlers, and database operations." Architecture discussion (layers, ports, adapters,
repositories) "none of these fix a weak understanding of the domain. They only give shape to whatever
understanding already exists."

Event Modeling starts elsewhere: following [[adam-dymitruk]]'s hotel-booking framing, imagine the system
already exists and ask which facts would have been captured as time moves forward, then add what users
see. The decisive test he applies to an event name is whether it preserves the *reason*:
`ReservationUpdated` "is weak because it says that something changed, but not why it changed. It hides
the difference between a guest changing dates, a host canceling a reservation, support correcting a
mistake, or the platform marking a guest as a no-show." **"Generic update language preserves the data
change but loses the business reason."**

Where authority lives is what decides whether you are event-sourced: "If the event history is the
authoritative application state, the system is using Event Sourcing. If the current tables are
authoritative and events only appear in the model, logs, messages, audit trails, or integration
notifications, the system may be event-aware or event-driven, **but it is not Event Sourcing.**"

## Key points

- **The Dymitruk quote that carries the whole argument:** *"Events happen — whether we store them or not
  is our choice."* Fritzsche calls it "the clean boundary," and notes Dymitruk himself shows Event
  Modeling applied with table storage.
- **The building blocks, and where their value lies:** events, views, commands, automations, external
  systems — "their value is not in the notation itself… [it is] that they connect user-visible
  information, intent, fact, and consequence in one shared description."
- **Event Modeling vs [[event-storming]]:** Storming "is mainly used to explore the problem space"; Event
  Modeling "takes the discovered behavior and describes how the system should work over time." Discovery
  and system description "are related, but they are not the same activity."
- **Ubiquitous Language, with the emphasis on *rigorous*.** Citing [[martin-fowler]]'s "common, rigorous
  language": "Shared language is not a soft communication exercise. Software does not handle ambiguity
  well, and business ambiguity does not disappear because the code compiles." His evidence that the
  vocabulary is real, not invented for screens: **Booking.com and Airbnb's own help material** distinguish
  reservation, host, guest, listing, stay, cancellation, refund, no-show, check-in/out.
- **Why a model is "less forgiving" than a schema:** "A table can contain a status column without
  explaining who is allowed to change the status, when the change is valid, or which consequence follows…
  An Event Model is less forgiving because every fact has to stand in the timeline and explain its place."
  Naming a fact makes the next questions concrete (who cancelled, before or after the free-cancellation
  window, does the property become available again, is a refund due, who is notified).
- **The symmetric warning, and the sharpest line in the piece:** "an event store does not guarantee a
  good model. If the stored events are named `ReservationUpdated`, `GuestUpdated`, or `PropertyChanged`,
  the system may technically use Event Sourcing while still preserving a CRUD-shaped understanding of the
  domain. **Storing vague events only preserves the vagueness permanently.**"
- **When he says ES *is* the right call:** "when the factual history is valuable as the authoritative
  application state: for auditability, temporal reasoning, reconstruction of past state, independent read
  models, or a clear record of why state changed. These benefits come with costs. Events are long-lived
  facts. Projections, queries, concurrency, and versioning need explicit design."
- **The closing rule:** "Event Modeling should improve the storage decision, not replace it… Its first
  job is to make the behavior clear. The implementation should preserve that clarity instead of turning
  the model back into anonymous data mutations."

## Connections / contrast

- **The KB's cleanest statement of the EM ≠ ES separation, from outside the Event Modeling community's
  own advocacy.** [[event-modeling]] and [[event-sourcing]] are described as partner patterns across the
  KB; this article is the source to cite for the boundary between them, and for the *authority* test that
  decides which one a system is using.
- **It pairs with, and slightly predates, his storage essay.**
  [[fritzsche-choosing-storage-is-choosing-what-your-system-forgets]] (2026-07-29) hardens the same split
  into four words (state / event / fact / record) and the "discipline of the record" criterion. This
  article is the *method-side* half; that one is the *store-side* half.
- **A CRUD-shaped event store is the failure mode nobody else in the KB names.**
  [[event-modeling-anti-patterns]] catalogues bad *board shapes*; this names a bad *vocabulary* that
  survives adoption of the right technology — closer to
  [[dudycz-backend-for-frontends-for-event-driven-apis|Dudycz's "Poor Man's replication through the
  queue"]] (`SthSthCreated/Updated/Deleted` published as if they were events) than to anything on the
  anti-patterns page. Two authors, same week-range, same diagnosis of `SomethingUpdated`.
- **Chronological note within his own arc.** This article is *milder* than the August pair
  ([[fritzsche-why-the-entity-model-is-an-illusion]], [[fritzsche-how-event-sourcing-grows-with-the-business]]):
  here relational tables remain a legitimate implementation of a good event model; there the entity model
  itself is the error. And here **auditability is listed as a reason to choose ES**, which the August note
  [[fritzsche-event-sourcing-is-not-an-audit-feature]] calls a fundamentally wrong motivation. The KB
  should treat his position as **having hardened over July–August 2026**, and not quote one month's
  framing as his settled view.
- **Supports Dilger's "traditional systems" line and Enzler's pragmatism.** The claim that a model is
  useful without an event store is the same permission [[dilger-99-percent-software-boring-two-patterns]]
  and [[enzler-event-sourcing-aggregates-dcb-or-what]] grant from other directions.
- Adjacent: [[given-when-then]] · [[domain-driven-design]] · [[cqrs]] · [[slice]] ·
  [[event-modeled-agent-design]] · [[martin-fowler]] · [[adam-dymitruk]].

## Limits

- **No agent content at all.** This is a pure modeling/architecture essay; nothing here supports or
  weakens the KB's agent-substrate claims.
- **No measurement and no case study** — the booking domain is a worked illustration, and the
  Booking.com/Airbnb references establish only that the *vocabulary* exists, not that any team benefited.
- **Secondary citation throughout.** Fowler's definitions of Ubiquitous Language and Event Sourcing, the
  Azure pattern page and Dymitruk's posts are quoted in Fritzsche's framing; none is captured in the KB as
  a primary from this page.
- **The "not Event Sourcing" test is definitional, not operational** — it tells you what to call a
  system, not how to decide whether to make the log authoritative. His own answer to that ("choose it
  because the system benefits from events as the source of truth") is a criterion without a procedure.
- Blog primary; client-rendered site (headless watches miss it).

_Source: `raw/articles/fritzsche-thinking-in-events.md`._
