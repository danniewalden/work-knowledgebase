---
title: Denoting an Agent in an Event Model (worked example)
type: deliverable
created: 2026-06-13
sources: [dymitruk-event-modeling-future-proof-agents, event-modeled-agent-design, qlerify-event-modeling-tool-ai]
tags: [event-modeling, agentic-ai, worked-example, notation]
---

# Denoting an Agent in an Event Model

The key insight from Adam Dymitruk (creator of Event Modeling): **you don't need any new notation for an agent.** Because automation was baked into the method from the start, an agent slots into one of two roles that already exist.

---

## Role 1 — Agent as *user*

An actor in a swimlane that issues **commands**, exactly like a human. Use this when the agent fronts a workflow (e.g. a chat-invoked agent kicking off a task).

On the timeline it's indistinguishable from a person clicking a button:

```
  actor          command              event
┌─────────┐    ┌───────────┐    ┌──────────────────┐
│ 🤖 Agent │───▶│ Start Task │───▶│ Task Started     │
│ (user)  │    │ (command)  │    │ (event)          │
└─────────┘    └───────────┘    └──────────────────┘
```

---

## Role 2 — Agent as *processor*  (the Automation pattern)

A processor watches a read model / "todo list," issues commands to other systems, and writes their replies back as **events**. This is the home for autonomous or background agents, and maps cleanly onto an initializer-executor / ralph-loop harness.

```
   view / read model        processor          command            event
┌────────────────────┐   ┌────────────┐   ┌──────────────┐   ┌────────────────┐
│ 📋 Pending Work     │──▶│ 🤖 Agent    │──▶│ Run Step      │──▶│ Step Completed │
│ (todo list)        │   │ (Automation)│   │ (command)    │   │ (event)        │
└────────────────────┘   └────────────┘   └──────────────┘   └───────┬────────┘
        ▲                                                             │
        └─────────────────── updates ────────────────────────────────┘
```

The processor loops: read the todo view → issue a command → store the reply as an event → the event updates the view → repeat.

---

## Multi-agent system

Just several users/processors composed on **one timeline**, coordinating through the shared event ledger — no redesign of your existing model required.

```
 Swimlane: User Agent     │  Start Task ─▶ ● Task Started
                          │
 Swimlane: Worker Agent   │              ● Task Started ─▶ Run Step ─▶ ● Step Completed
                          │
 Swimlane: Guardian Agent │                              ● Step Completed ─▶ (veto / approve)
─────────────────────────────────────────────────────────────────────────────────────▶ time
```

Each agent gets its own swimlane (Conway's-Law / DDD style) and is wired with the same **command → event → view** vocabulary as everything else.

---

## Pinning down behavior

Attach a **Given-When-Then** per command/view to specify what each agent does — the same way AI-assisted EM tools (e.g. Qlerify) express each step:

> **Given** there is pending work on the todo list
> **When** the agent issues `Run Step`
> **Then** a `Step Completed` event is appended to the ledger

---

## Notation cheat-sheet

| Event Modeling construct | How the agent uses it |
| --- | --- |
| **Actor / swimlane** | the agent's identity on the timeline |
| **Command** (blue) | the agent's *intention* — issued as user or processor |
| **Event** (orange) | the *fact* recorded after a command succeeds |
| **View / read model** (green) | the "todo list" the processor reads from |
| **Automation pattern** | the agent-as-processor loop |
| **Given-When-Then** | the spec pinning down each agent step |

---

*Caveat: Dymitruk asserts the user/processor mapping in a single 2025 post; no captured source yet gives a fully worked event model of a multi-agent system using the method itself. The closest is an event-sourcing/CQRS treatment one substrate-level remove from the method (see [[esaa-event-sourcing-for-autonomous-agents]]).*

*Sources: [[dymitruk-event-modeling-future-proof-agents]] · [[event-modeled-agent-design]] · [[qlerify-event-modeling-tool-ai]].*
