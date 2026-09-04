---
source_url: "https://www.linkedin.com/in/martindilger/recent-activity/all/ (two-part series; exact permalinks not captured; Part 1 links Part 2 via https://lnkd.in/ezEhhbSY)"
title: "How I use Local-LLMs to build software systems (Part 1) + what's running under the hood (Part 2)"
author: Martin Dilger
publication: LinkedIn
published: 2026-07-02
retrieved: 2026-07-03
type: note
---

# Dilger — Local-LLM distributed agent setup for Event Modeling (two-part LinkedIn series)

*(Martin Dilger, LinkedIn. Part 1 posted ~1 day, Part 2 ~same-day as retrieval. Verbatim capture of both parts. On tight EM×agents focus — a concrete implementation report of his always-on, board-driven, distributed local-LLM build/modeling factory; enriches [[dilger-event-modeling-agent-harness]] and [[dilger-model-is-a-living-spec-always-on-agent]] with real hardware, models, and the claim/lock synchronization mechanism.)*

## Part 1 — "How I use Local-LLMs to build software systems"

How I use Local-LLMs to build software systems

I´ve been advocating the use of local models for quite some time already.
I´m having different agents running on different machines.. basically distributing the load.. more machines, more agents, more work gets done.

The Models I´m actively using right now:
- Gemma4
- Qwen3.6:27B

They run on 3 Asus GX10 in the office. These machines run independently - no clustering necessary.

Harness is Claude Code or Open Code backed by Ollama ( and one Hermes Agent )

With Gemma4 - performance is around 60 tok/sec
With Qwen3.6:27b - performance is around 30 tok / sec

This all is not superfast, but good enough.. as it all happens in the background, nobody typically cares.

Running Claude Code adds an overhead of ~ 1sec per loop-iteration, which is neglectible.

Here´s the workflow:
- Model the behavior with stakeholders
- Refine with Engineers
- Set the slice into status "Planned"
- One agent picks it up and sets the status "In Progress"

For this, it´s completetely irrelevant where this agent runs. Could be on my local machine, could be somewhere in the office.. at the Event Modeling in a session, someone asked whether an agent is connected to the Board we used. It was.. but I couldn´t tell from where and typically I don´t care.

Only one agent can set the status in progress. Any other agent will see that the slice is already in progress and will pick another one.

Agents run in ralph-loops 24/7 - I typically have 6-10 agents running in parallel looking for work. Most of them for building, 1-2 for modeling support.

The "Slice" is the perfect unit of work, as agents can work on them in parallel - that´s the power of "decoupling". They don´t have to know anything from each other.

When Slices change - just put them back from "Done" to "Planned" - an agent will compare the specified behavior to the actual code and make the necessary adjustment ( add Specs, change projections, add / remove fields.. )

The fascinating thing is - at some point in time you stop thinking about the code, well knowing it´ll be built in the background. Focus is completely on the Spec-Side of things - specifying "what" needs to be done, not "how"..

The combination of Event Modeling, Event Sourcing and Slice-Based Architectures - I call it the triplet of flexible architectures - enables this way of working.

Hope that gives some insights!

[Post closes with a promotion for an August teaching program — text truncated in capture.]

## Part 2 — "what's actually running under the hood"

Yesterday I showed my local Agent Setup for Event Modeling. Today I want to show you what's actually running under the hood.
I´ve been chasing this idea for so long..

Three Asus GX10s. Sitting in my office. Quietly turning models into running software.

Here's how it works:

Each machine runs projects in parallel. Every project has its own Build-Kit and Modeling-Kit, matched to the stack and architecture it needs.

The Kits connect live to the Eventmodelers-Platform through a real-time agent - always listening, always ready.

Every project is tied to one Board, and reacts instantly to what happens there:
→ A slice gets moved to "Planned" - one agent picks it up and starts working.
→ Someone leaves a comment for an agent → a new Modeling Task appears (Modeling Kit)
→ Someone starts talking → live voice-to-text transcription triggers a Modeling Task, no one touches a keyboard

Agents only wake up when there´s work. Otherwise they silently wait, no cost, no tokens..

Multiple build- and modeling agents can work the same board, the same project, at the same time - even across different machines. And they don't step on each other. The moment a slice hits "Planned," one agent claims it and moves it to "In Progress." Locked. No collisions. That's the whole synchronization trick - beautifully simple.

There are no merge conflicts, no coupling hell. Agents silently and tirelessly do their work.

You can spin up you own agents locally with Claude Code for example. It just joins the workforce like any other agent. I typically do this for discovery and modeling work - the interviews, the "wait, what did the business actually mean by that" moments - powered by the Modeling Skills.

Spin up a new project, and the Build- and Modeling-Agents provision themselves automatically. No setup ceremony. You go from model to running code in minutes.

And the Kits aren't empty shells - they come with batteries included: opinionated, production-ready skills built on our blueprint architecture for each stack.

Could I add more machines and run more agents? Sure. But honestly, these three on-prem boxes have so much headroom, they'll carry us a long way.
This investment was well worth it.

This is the closest I've ever come to what I'd call a real feature factory:
Idea → Model → Build → Deploy.

One of the happiest moments was the first time, when a non-technical person modeled something and it turned into code. Just amazing.

I´ve been chasing this idea, and now it just... runs. Quietly. In the background. While I sleep.

of course - the real worked happened long before - modeling and decomposing the software into slices is what enables this. That´s what we talk about next.

Part 1 - Local Model Setup: https://lnkd.in/ezEhhbSY
