---
title: "Source: Dudycz — Backend-for-frontends for event-driven APIs (LinkedIn)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [dudycz-backend-for-frontends-for-event-driven-apis]
raw_file: [raw/notes/dudycz-backend-for-frontends-for-event-driven-apis.md]
tags: [event-driven-architecture, event-sourcing, integration, coupling, substrate, focus]
---

# Source: Dudycz — Backend-for-frontends for event-driven APIs (LinkedIn)

LinkedIn post by **[[oskar-dudycz]]**, 2026-08-29, part of his **#EventDrivenDiary** series. Raw
capture: `raw/notes/dudycz-backend-for-frontends-for-event-driven-apis.md` — captured verbatim via
**live logged-in Chrome** (the headless watch cannot render this feed); only edit is collapsing
LinkedIn's `hashtag\n#x` markup. **Date accurate to the day, not the hour** (relative age stamp at
retrieval).

**Register:** PRACTITIONER ARGUMENT drawn from "my past projects, in my client work" — an experience
report, **not measurement**. Cites **Gregor Hohpe** for the events/commands/state message split (Hohpe
is not captured in the KB).

## Summary

The move is to take **backend-for-frontends** — a familiar answer to different Web API consumers having
different needs — and ask why we stop there: "Why don't we do the same for other types of APIs? For
instance, an **event-driven API**?"

The failure he reports is teams "trying to satisfy totally different customer needs by publishing
uniform events. What's worse, those events aren't actually events; most of the time, **they're just state
notifications: `SthSthCreated`, `SthSthUpdated`, `SthSthDeleted`.** I'm calling them: **Poor Man's
replication through the queue.**"

Two splits fix it. First, **internal vs external events** — internal (also *private* or *domain*) events
are "meaningful inside the module context… typically smaller and more focused, as internally we know our
domain"; external (also *public* or *integration*) events are "meaningful in the whole system context",
close to **pivotal events from EventStorming** or the **Summary Events** of an earlier diary chapter.
Second, **messages are not only events** — per Hohpe there are also **commands** and **state**.

## Key points

- **"Poor Man's replication through the queue"** is the coinage worth keeping: a `SomethingUpdated`
  broadcast is database replication wearing an event's clothes. It is the messaging-layer twin of
  [[fritzsche-thinking-in-events|Fritzsche's]] "storing vague events only preserves the vagueness
  permanently."
- **Why the message-type split matters, in his words:**
  - **state change** "just tells us what has changed; consumers won't know why this state changed or
    what has happened. This is useful for the data sync between modules mentioned earlier" — so it is a
    legitimate message type, *provided you call it what it is*.
  - **commands** "represent the intention to perform a certain business operation; they're **directed,
    not broadcast** as events. They can also be **rejected**. If we mistake them for events, we end up
    with **passive-aggressive communication**, which can lead to dropped communication if we accidentally
    throw an error."
- **Two named failure modes of getting it wrong:**
  "If we broadcast all internal events, we create a **leaking abstraction and a spider web of
  dependencies.**"
  "If we broadcast events while ignoring other message types, our communication looks like parliament: a
  room filled with shouting people. **This is a first step to a distributed monolith.**"
- **The framing principle:** "We shouldn't lie to ourselves about our intentions, as that ends badly." He
  also carries over the Web-API lesson: a uniform API is fine "if our API is our product, or if it's
  generic enough that we can dictate its form" — otherwise negotiate and meet in the middle.

## Connections / contrast

- **The KB has no concept page for the internal/external event split, and it needs one.**
  [[event-driven-architecture]] describes brokers and decoupling; [[event-sourcing]] describes the log;
  neither states that the events you *store* and the events you *publish* are different populations with
  different design rules. This post is the primary for that, and the batch deltas propose it as a
  concept.
- **Directly constrains the KB's agent-EDA thread.** [[agentic-event-driven-systems]],
  [[atlan-event-driven-architecture-for-ai-agents]], [[confluent-agentic-event-driven-systems-architecture]]
  and [[solace-multi-agent-systems-real-time-context-eda]] all argue agents should communicate over
  events. This post says **what those events must not be** — if inter-agent messages are
  `AgentStateUpdated` broadcasts, the architecture has bought a distributed monolith with extra latency,
  and the commands-vs-events distinction (directed, rejectable) is exactly what agent-to-agent protocols
  need to get right (see [[agent2agent-protocol]], [[multi-agent-orchestration]]).
- **Sharpens the [[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember|event store vs
  event stream]] line from a third angle:** AxonIQ distinguishes them by *capability* (a store records
  why, a stream moves what); Dudycz distinguishes them by *message design* (internal facts vs external
  integration messages vs state sync) — the store/stream difference restated as a modelling decision
  rather than a product choice.
- **The BFF half is the article's**: the fuller treatment of composing per-screen backends is in
  [[dudycz-vertical-slices-ownership-and-external-dependencies]] ("It's still a slice; it's named after a
  screen because that's honestly what it is"). This note is the event-driven extension of that idea.
- Adjacent: [[event-storming]] (pivotal events) · [[coupling-taxonomy]] and
  [[khononov-coupling-should-be-weighed-not-counted]] (broadcasting internal events is Model- or
  Intrusive-strength coupling to everyone at once) · [[event-modeling]] · [[cqrs]].

## Limits

- **Short-form post (~450 words), no code, no worked example.** The internal/external split is asserted
  with definitions but no guidance on the hard part — *how* to derive an external event from internal
  ones, versioning at the public boundary, or who owns the published contract.
- **No measurement**; "the common motive I see" is an experience report.
- **Summary Events and pivotal events are referenced, not defined** ("previous chapters of
  #EventDrivenDiary" are not captured), so part of the argument points outside the KB.
- **Hohpe is cited second-hand** for the events/commands/state taxonomy; his primary is not captured.
- Day-accurate date only; part of a series whose other chapters are missing.

_Source: `raw/notes/dudycz-backend-for-frontends-for-event-driven-apis.md`._
