---
title: "Fritzsche — Choosing Storage Is Choosing What Your System Forgets"
type: source
created: 2026-08-03
updated: 2026-08-03
sources: [fritzsche-choosing-storage-is-choosing-what-your-system-forgets]
raw_file: [raw/articles/fritzsche-choosing-storage-is-choosing-what-your-system-forgets.md]
tags: [event-sourcing, facts, state, storage, thinking-in-events, substrate, focus]
---

# Fritzsche — Choosing Storage Is Choosing What Your System Forgets

Blog article by **[[rico-fritzsche]]** (ricofritzsche.me, 2026-07-29). A conceptual grounding piece that
holds four words apart — **state, fact, event, record** — to settle what an event store keeps that a
current-state database forgets. Raw:
`raw/articles/fritzsche-choosing-storage-is-choosing-what-your-system-forgets.md`.

## The four words

- **State** — what holds at a moment; it *holds*, it never *happens* (Ryle/Vendler). After a happening, a
  new state holds (`s → s′`).
- **Event** — a change of state at one moment; it *occurs*, once. Von Wright's insight: a change is an
  ordered pair `(s, s′)`, but the pair **leaves a gap** — two different happenings can produce the same
  before/after (a guest booking vs. a host blocking leave the *same* calendar difference). The event
  **type** carries what the pair loses.
- **Fact** — a *true* statement about state and/or causality, **bound to the moment it is about**. A fact
  cannot change (Hickey: "you cannot update a fact, because you can't change the past"); new knowledge is
  a new fact that *supersedes* the old, which stays true about its own moment.
- **Record** — a fact **written into a store**. The record is *not* the fact. Overwriting a record
  changes no fact — it **destroys the system's only access** to that fact.

Three layers: state + events are *in the world*; facts *state* them; records are *what the system keeps*.
Everything a system knows, it knows through records.

## The payoff

- **What an event store keeps:** append-only records, each a domain-named type (`ReservationConfirmed`,
  `NightsBlocked`) that preserves what the state-difference loses; current state is **derived** (Greg
  Young: "Current State is a Left Fold of previous behaviours"). Datomic's typeless datom is a *fact*
  store; the **domain-named type** is what makes it an *event* store.
- **What a current-state DB keeps:** each row states what holds *now* (Darwen/Date: a database is "a set
  of (true) propositions"). An `UPDATE` changes a record and nothing else — the prior fact stays true
  about its moment but its record is destroyed, and the *happening* was never written at all (Hickey's
  "place-oriented programming," born of scarce memory).
- **The dividing line is the discipline of the record, nothing else:** a relational table written
  **append-only keeps facts** (accountants' ledgers); an event log **edited in place keeps state under a
  misleading name.** "Overwritten records keep state. Appended records keep facts."
- **The decision:** *"Choosing storage is choosing what the system may forget."* Business questions asked
  later ("why is this night unavailable? what price did the guest agree to?") are questions about facts
  and events — answerable only while their records exist. **Event Sourcing is a storage decision;
  "thinking in events" does not depend on it.**

## Why it matters here

- The KB's clearest *conceptual* grounding for [[event-sourcing]] — separating the method
  ("thinking in events") from the storage choice, and giving [[agent-explainability]] its substrate (the
  "why" only survives if the records survive). Pairs with
  [[fritzsche-why-your-software-cannot-explain-business-decisions]] (the same "storage is a separate
  decision" thesis) and [[goeleven-event-sourcing-not-auditing-for-free]] (what the log does/doesn't give
  you for free). Reinforces the [[roden-event-sourcing-meets-mcp-whole-story-for-llms|"whole story for
  LLMs"]] angle: an event store is the store that *doesn't forget*.
- Caveat: philosophy-of-storage essay; definitional, not empirical.

## Links

Entities: [[rico-fritzsche]], [[greg-young]]. Concepts: [[event-sourcing]], [[agent-explainability]],
[[cqrs]], [[event-driven-architecture]].
Related sources: [[fritzsche-why-your-software-cannot-explain-business-decisions]],
[[goeleven-event-sourcing-not-auditing-for-free]], [[roden-event-sourcing-meets-mcp-whole-story-for-llms]],
[[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]].

_Raw source: `raw/articles/fritzsche-choosing-storage-is-choosing-what-your-system-forgets.md`._
