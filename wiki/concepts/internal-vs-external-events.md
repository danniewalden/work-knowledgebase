---
title: Internal vs External Events (and messages that aren't events)
type: concept
created: 2026-09-04
updated: 2026-09-04
sources: [dudycz-backend-for-frontends-for-event-driven-apis, fritzsche-thinking-in-events, axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]
tags: [event-driven-architecture, event-sourcing, integration, coupling, substrate, focus]
---

# Internal vs External Events (and messages that aren't events)

The events a module **records** and the messages it **publishes** are different populations with
different design rules. Stated by **[[oskar-dudycz]]**
([[dudycz-backend-for-frontends-for-event-driven-apis]], 2026-08-29, #EventDrivenDiary) as an extension
of **backend-for-frontends**: we already accept that different API consumers need different surfaces —
"why don't we do the same for other types of APIs? For instance, an event-driven API?"

## Poor Man's replication through the queue

The failure mode he names, and the phrase worth keeping: teams satisfy "totally different customer needs
by publishing uniform events. What's worse, those events aren't actually events; most of the time,
**they're just state notifications: `SthSthCreated`, `SthSthUpdated`, `SthSthDeleted`.** I'm calling
them: **Poor Man's replication through the queue.**"

That is database replication wearing an event's clothes — and the messaging twin of
[[fritzsche-thinking-in-events|Fritzsche's]] "storing vague events only preserves the vagueness
permanently." Both authors, in the same fortnight, identify `SomethingUpdated` as the tell that the
domain's reasons have been discarded and only its mutations kept. See [[entity-centric-thinking]].

## The two splits

**1. Internal vs external events.**

- **Internal** (also *private*, *domain*) — "meaningful inside the module context… typically smaller and
  more focused, as internally we know our domain."
- **External** (also *public*, *integration*) — "meaningful in the whole system context," close to
  **pivotal events** from [[event-storming]] or to **summary events** (which do double duty as the
  archiving hinge — see [[event-sourcing]]).

**2. Messages are not only events** (Dudycz credits **Gregor Hohpe**, not captured in the KB):

- **State change** "just tells us what has changed; consumers won't know why this state changed or what
  has happened. This is useful for the data sync between modules" — a legitimate message type *provided
  you call it what it is*.
- **Commands** "represent the intention to perform a certain business operation; they're **directed, not
  broadcast** as events. They can also be **rejected**. If we mistake them for events, we end up with
  **passive-aggressive communication**, which can lead to dropped communication if we accidentally throw
  an error."

## The two failure modes

- "If we broadcast **all internal** events, we create a **leaking abstraction and a spider web of
  dependencies.**" (In [[khononov-coupling-should-be-weighed-not-counted|Integration Strength]] terms:
  Model- or Intrusive-strength coupling, to everyone at once.)
- "If we broadcast events while **ignoring other message types**, our communication looks like
  parliament: a room filled with shouting people. **This is a first step to a distributed monolith.**"

His framing principle: "We shouldn't lie to ourselves about our intentions, as that ends badly."

## Why this constrains the agent-EDA thread

[[agentic-event-driven-systems]] and its vendor sources ([[atlan-event-driven-architecture-for-ai-agents]],
[[confluent-agentic-event-driven-systems-architecture]],
[[solace-multi-agent-systems-real-time-context-eda]]) argue that agents should coordinate over events.
This page says **what those events must not be**: if inter-agent traffic is `AgentStateUpdated`
broadcasts, the architecture has bought a distributed monolith with extra latency and no explanation of
*why* anything happened. The commands-vs-events distinction — directed, rejectable — is precisely what
agent-to-agent protocols must get right ([[agent2agent-protocol]], [[multi-agent-orchestration]],
[[process-managers-and-todo-lists]]).

It also restates the [[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember|event store
vs. event stream]] line as a **modelling** decision rather than a product choice: AxonIQ separates them
by capability (a store records *why*, a stream moves *what*) — an **interested claim**, since AxonIQ
sells an event store — while Dudycz separates internal facts, external integration messages and state
sync by *intent*.

## Limits

A ~450-word LinkedIn post: definitions with no code and no worked example. **Nothing measured** — "the
common motive I see (in my past projects, in my client work)" is an experience report. It gives no
guidance on the hard part: how to *derive* an external event from internal ones, how to version the
public contract, or who owns it. Summary/pivotal events are referenced from uncaptured chapters of his
series, and Hohpe is cited second-hand.

## Related

[[event-driven-architecture]] · [[event-sourcing]] · [[cqrs]] · [[event-storming]] ·
[[coupling-taxonomy]] · [[balanced-coupling]] · [[vertical-slice-architecture]] ·
[[entity-centric-thinking]] · [[agentic-event-driven-systems]]

_Sources: [[dudycz-backend-for-frontends-for-event-driven-apis]] · [[fritzsche-thinking-in-events]]._
