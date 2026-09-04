---
title: "Adaptech Group — Your Workflow Should Not Live Inside a Giant Process Manager"
type: source
created: 2026-07-29
updated: 2026-07-29
sources: [adaptech-workflow-not-inside-giant-process-manager]
raw_file: [raw/articles/adaptech-workflow-not-inside-giant-process-manager.md]
tags: [event-modeling, event-sourcing, cqrs, process-manager, saga, automation-pattern, focus-substrate]
---

# Adaptech Group — Your Workflow Should Not Live Inside a Giant Process Manager

A design primary from **[[adaptech-group]]** ([[adam-dymitruk]]'s consultancy; published on the
Adaptech Group LinkedIn page and reposted by Dymitruk, 2026-07-28) arguing that a long-running
business process should **not** be coordinated by one large **saga / process manager**. Instead,
model workflow progress as **visible information** — a **projected to-do list** — and let several
small, **single-responsibility processors** act on it. The concrete worked realization of Event
Modeling's **[[event-modeling|Automation pattern]]** ("a processor works a todo list") and the
recurring podcast theme **"sagas → to-do lists"**, previously captured only as show-notes.

## The problem — hidden workflow state

A process starts as a simple sequence (check inventory → confirm payment → arrange shipping →
notify). Real operating conditions (an external system times out, a payment succeeds but the
confirmation is late, a retry risks doing the work twice, a deploy restarts mid-process) make it
grow until one large coordinator holds every step, exception, retry and compensation rule. At that
point the problem is bigger than code complexity: **the organization can no longer see the current
state of the business process** without reading the coordinator's internal branches. Basic questions
become hard — what finished, which external result is still missing, did the payment fail or just
arrive late, can it continue after a restart, would another attempt repeat a completed action —
questions support, ops, developers and leaders all need answered. "The workflow exists, but the
business cannot easily inspect it." That invisibility **is** delivery risk.

## The design — a projected to-do list + focused processors

- **Represent progress as information.** For each active process, a **projection** records what the
  system knows, what's done, what's unfinished, and whether there's enough information to continue.
  Worked example (a stock purchase): a projected row shows the requested stock + quantity, whether a
  price has been received, when it arrived, whether the order was submitted, the submission result,
  and whether another attempt is allowed. The projection **does not replace the event history** —
  events remain the record of what happened; the projection turns that history into a view that
  **people and automated processors** can both use ([[cqrs]] read model).
- **Give each processor one responsibility.** Once progress is visible, no single coordinator is
  needed: one small processor fetches the market price, another submits the order once a valid price
  exists, another manages retries or verifies an uncertain result. Several processors **observe the
  same to-do list**, each reacting only to the fields/statuses relevant to its job — focused,
  testable, replaceable. The workflow still coordinates correctly because the projection shows which
  information is present and which step is ready.

## Three supporting claims

- **External calls are business states, not procedure lines.** "Call the provider, get the result,
  continue" hides several meaningful states: not-sent, awaiting-response, response-arrived-too-late,
  and done-remotely-but-unconfirmed-locally. These matter to the business — a stock price needs a
  **timestamp** (how stale is too stale?), a payment needs a **stable identifier** (don't charge
  twice), a shipment may need verification before re-requesting. As events + projected statuses they
  can be discussed, measured, improved; buried in a procedure they're invisible.
- **Recovery should be visible before failure occurs.** Test each step by asking what the system
  knows if it stops there. If the answer depends on an in-memory position or a hidden flag inside one
  process manager, recovery is hard. An event history + to-do list are **durable evidence**: the
  system can see the payment was requested and whether a confirmation arrived, and if uncertain a
  processor **verifies rather than recharges**. Recovery becomes normal design, not special cases
  bolted on after incidents — which is also what makes legacy **modernization** safer.
- **Visibility improves more than architecture.** The same projection powers operational tools —
  dashboards of what's waiting on payment/market-data/SLA breach, support seeing *why* a customer's
  process stopped, product measuring step durations. Business-language statuses
  (`PaymentAcceptedAwaitingShipment`) communicate more than "instance at step 7."

## Event Modeling exposes the structure before implementation

[[event-modeling|Event Modeling]] surfaces this early: instead of one box labeled "Saga," the model
shows the business process as a **timeline of commands, events, projections and automations** — a
purchase request produces an event; a projection shows purchases waiting for a price; a processor
obtains the price; an event records it; the projection updates; a different processor submits. That
lets business, architects, developers and testers examine the same process **before** it is
distributed across services. "At Adaptech Group, this is one reason Event Modeling is treated as a
**foundation for [[event-sourcing|Event Sourcing]] work**."

## Migration on-ramp

No full transformation required: pick one process manager / orchestration that causes operational
confusion or slows delivery; **list every piece of information it needs** (external results,
timestamps, attempt counts, approvals, failure reasons, completion states); then ask **which missing
item prevents the next decision** — that question reveals the processors the workflow actually needs.
Turn the requirements into a projected to-do list, use focused processors to complete each
unfinished responsibility, record results as events. The result should be **easier to inspect than
the code it replaces**.

## Connections

The dedicated primary for [[process-managers-and-todo-lists]] (the pattern). Fills out the
**Automation pattern** in [[event-modeling]] (processor + todo list) and the **projection-as-read-model**
angle of [[cqrs]]; sits on the [[event-sourcing]] substrate (events as durable evidence for recovery).
The one-processor-one-responsibility rule echoes [[vertical-slice-architecture]] (a processor as a
focused slice) and the capability-owns-its-processing line in [[autonomous-domain-capabilities]]
([[rico-fritzsche]]'s Reactors). Business-language statuses tie to [[domain-driven-design]] /
[[business-capabilities]]. Caveat: **vendor/self-authored** (Adaptech markets Event Modeling +
Event Sourcing delivery), a clear design essay with no external quality data — but the clearest
single statement yet of the saga→to-do-list pattern the KB had only in podcast show-notes.

_Source: [[adaptech-workflow-not-inside-giant-process-manager]] (raw/articles)._
