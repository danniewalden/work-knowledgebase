---
title: "Event Modeling — A Getting-Started Guide for Beginners"
type: deliverable
created: 2026-06-13
sources: [eventmodeling-what-is-event-modeling, semaphore-dymitruk-event-modeling]
tags: [event-modeling, getting-started, beginner]
---

# Event Modeling: Getting Started

A one-page guide for someone brand new. Event Modeling is a way of designing a
software system by describing it as a **timeline of events** — the story of what
happens, in order — instead of as a snapshot of its current state. That single
shift in perspective is the most important thing to absorb first.

The method was created by Adam Dymitruk. It's deliberately small: **3 building
blocks, 4 patterns, 2 ideas**, run as a **7-step workshop**.

---

## Step 1 — Read the canonical introduction

Start with Dymitruk's own write-up, "What is Event Modeling?":
**https://eventmodeling.org/posts/what-is-event-modeling/**

It's short and readable, and it's the source everything else builds on. Don't
worry about mastering it — just get the core idea: *model what happened over
time, not the current state.*

## Step 2 — Learn the tiny vocabulary

Almost everything runs on three building blocks. Learn these and you can read any
event model:

- **Event** — a fact that something happened and state changed. Past tense:
  *"Order Placed," "Guest Checked In."* If nothing was stored, it isn't an event
  (e.g. "user looked at the calendar" doesn't count).
- **Command** — a user's *intention* to change something. *"Place Order,"
  "Check In Guest."* A command, if accepted, produces an event.
- **View (read model)** — what the screen shows the user. Views update as events
  accumulate. They're *passive*: a view can't reject an event that already happened.

The flow is always the same, laid out left-to-right on a timeline:

> **Command → Event → View**

Wireframes (rough sketches of the screens) sit across the top, grouped into
**swimlanes** — one lane per user or system involved.

## Step 3 — Model something you already understand

Event Modeling is a hands-on workshop method, so the fastest way to learn is to
do it. Pick a familiar process — a hotel check-in, placing an online order, a
library checkout — and lay it out on a whiteboard (sticky notes or a virtual
board) following the seven steps:

1. **Brainstorm events** — every fact that gets stored.
2. **Plot the timeline** — put those events in the order they happen.
3. **Storyboard** — sketch the screen for each moment.
4. **Identify inputs** — mark the commands (what the user does).
5. **Identify outputs** — mark the views (what the user sees).
6. **Apply swimlanes** — group events by the team or system that owns them.
7. **Elaborate scenarios** — flesh out the edge cases.

Finish with the **completeness check**: every piece of data on a screen should
trace back to an event that put it there, and every event should have somewhere
it ends up. No orphans.

## Step 4 — Write a couple of Given-When-Then specs

For one command, write a small specification in this shape:

> **Given** [events that already happened]
> **When** [this command is issued]
> **Then** [this new event is stored]

It's the same Arrange-Act-Assert pattern as a unit test, and writing one or two
makes the abstract model feel concrete. Each spec ties to *exactly one* command
or view.

---

## A few things worth knowing up front

- **Event Modeling is not Event Storming.** Event Storming (by Alberto
  Brandolini) is the messier, exploratory sticky-note brainstorm that Event
  Modeling grew out of. Event Modeling is the calmer cousin that produces a clean
  blueprint. They're related but different.
- **You don't need the heavy theory to start.** Event sourcing, CQRS, and
  Domain-Driven Design all pair nicely with Event Modeling, but none of them are
  prerequisites. Learn the three building blocks first; reach for the rest later.
- **Why people like it:** because each step is isolated by explicit contracts,
  the cost of adding a feature stays roughly flat as the system grows — you can
  build features in any order and estimate them reliably.

## If you prefer learning by clicking

Two online tools are built specifically for drawing event models:

- **prooph board** — modeling tool with a code-generation engine.
- **Qlerify** — AI-assisted modeling that generates models from descriptions.

## Recap

Model the **timeline of events**. Learn **Command → Event → View**. Sketch a
familiar process across **swimlanes**, run the **7 steps**, and finish with the
**completeness check**. That's enough to start thinking in events.
