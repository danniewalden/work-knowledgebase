---
source_url: https://www.eventmodelers.ai/docs/blog/event-modeling-conference-munich/
title: "40 Practitioners, 2 Days, and the Future of Software Design: What Happened at the First Event Modeling Conference in Munich?"
author: Martin Dilger
publication: eventmodelers.ai / Nebulit (blog)
published: 2025-11-28
retrieved: 2026-06-30
type: article
---

(Verbatim capture of Martin Dilger's recap of the FIRST Event Modeling
Conference. NOTE: this is the inaugural conference, held in October 2025 in
Munich, recap published 2025-11-28 — NOT the 2nd Event Modeling Conference of
25–26 June 2026, whose recap/recordings were still unpublished as of the
2026-06-30 watch. Nav/footer chrome and image markup stripped; images noted
inline; author's words kept intact. Closing workshop-sales pitch trimmed to a
note at the end.)

# 40 Practitioners, 2 Days, and the Future of Software Design: What Happened at the First Event Modeling Conference in Munich?

November 28, 2025 · ~20 min read · Event Modeling & Conference · Martin Dilger

Wednesday morning. I'm standing in front of a room, looking out at 40 practitioners who flew in from across Europe and from even further away to be here. Event modelers. Event sourcing experts. People who've been doing this work in the trenches, building real systems, facing real problems.

This wasn't a typical conference with keynote speakers talking at passive attendees. This was something different. This was practitioners coming together to help each other solve the hardest problems in our field. And honestly? I was super nervous.

## The Bold Move

Organizing a conference is always a risk. What if people didn't show up? What if the discussions fall flat? But I had a conviction: nothing beats face-to-face discussions when you're wrestling with complex modeling challenges. I've been evangelizing Event Modeling for years. I've modeled hundreds of systems. But this was about creating a space for the community to collide, debate, and discover together in a safe place.

## Day 1: Adam's Keynote Sets the Tone

After my welcome, we kicked off with Adam Dymitruk. No slides. No deck. Just Adam talking. His keynote was inspirational — not motivational-poster, but "this is why we do this work". He talked about the fundamental principles of Event Modeling, where it came from, the philosophy behind it, and why it matters.

Some announcements were also made during the Keynote: a planned **Certification program** for Event Modeling, and a **Joint-Venture between Adam and me — a new company that will focus on Tooling and Standardization for Event Modeling**, driving forward the "engineering" part of Event Modeling.

## The Unusual Experiment: 5 Rooms of Practitioners

Normally an Event Modeling workshop has one expert facilitating and everyone else learning. Not this time. We split into five teams, each working on a different problem, but every room was packed with experienced practitioners with strong opinions, battle-tested patterns, and real-world scars. People discussed different approaches, challenged each other's assumptions, asked "what about this edge case?" The energy was intense — not combative, but deeply engaged. This was pattern recognition happening at high speed.

## The Marketplace: Letting the Community Drive

After lunch, a marketplace session: anyone could pitch a topic in two minutes, then we dot-voted. One topic rose to the top immediately: **DCB (Dynamic Consistency Boundary) vs. Aggregates** — the most prominent debate in the event sourcing world right now.

## The Big Debate: Are Aggregates Really That Bad?

We had **Allard Buijze from AxonIQ** and **Adam Dymitruk** in the room, practitioners who'd done DCB for years, others defending aggregates ("they work fine for us"), and newcomers. These are real architecture decisions with real consequences. People shared war stories — systems that scaled beautifully with aggregates, and systems that collapsed under their weight; teams that tried DCB and never looked back, and teams that couldn't figure out if it was a thing at all. After modeling hundreds of systems, I've learned the answer is almost always "it depends." Do you keep aggregates and risk the typical issues later, or invest in DCB upfront? It depends.

## Day 1 Close: OpenCQRS 1.0

We closed the first day with **Frank Scheffler introducing the 1.0 release of OpenCQRS** — a lightweight Java-based framework for building event-sourced systems. OpenCQRS is production-ready, another sign the ecosystem is maturing. The frameworks are enablers; the point is the community of practitioners helping each other. Followed by a closing dinner.

## Day 2: The Future Arrives

I opened Day 2, then handed over to **Allard Buijze for the keynote**. And what Allard showed us… was the future arriving in real time. **The new AxonIQ platform. AI-powered code generation. Event Models turning into working code, automatically.**

I'm not exaggerating: this is exactly what I predicted. In January 2024 I gave a webinar and said publicly, "Our industry will change completely within two years." We're moving away from writing code and towards designing systems; AI will handle the rest — and we are within the predicted 2-year timeframe. Event Modeling is the key that unlocks this transformation.

## Why I Was So Certain

Event Models are structured, precise, complete. They define the events, the commands, the read models, the flows. Everything you need to build a system is in the model. Of course AI would eventually turn that into code. For years we've had the design (the Event Model) and then had to manually translate it into code — that's always felt like redundant work. Why model the system and then code the system? Why not model the system and generate the code? Watching Allard's keynote, I was seeing it happen.

## Live Event Modeling with 40 Practitioners

After Allard's keynote we did live Event Modeling with the entire conference. Forty practitioners, one problem, modeling together. The question that kept surfacing: **"How do I model automations? Where does the logic go?"**

## The Breakthrough: Where Do You Put the Logic?

Someone presented a real-world use case with complex automation rules. Do you model that logic as part of your domain, or treat it as a separate automation layer? The room dove in. Then I said something that caused a visible shift:

**"Just because the event is in the Event Model doesn't mean it has to be in the code later."**

## The Model Is Not the Implementation

The Event Model is a design tool and a communication tool — it aligns stakeholders, helps you understand the domain, and visualizes how the system should behave. But when you move to implementation, you make pragmatic engineering decisions. Maybe an event in your model doesn't need to be persisted. Maybe it's just a workflow step handled internally. Maybe you combine three events into one for performance, or split one into two because of team boundaries. **The model gives you clarity and alignment; the code gives you working software. They're related, but not the same thing.** Use the model as a guide, not a blueprint. Teams get stuck trying to force their code to match the model perfectly, which creates rigidity; the freedom to diverge in code — when it makes sense — leads to better, more maintainable systems.

## Another insight: The Zoom-In Approach

If you have a complex algorithm or detailed automation, do you put all of it in the Event Model (cluttering it and losing the high-level view) or leave it out (losing the detail)? My **two-model approach**: keep the main Event Model high-level, focused on information flow; when you have a complex slice — an automation, an algorithm, a detailed workflow — create a second "zoom-in" model. Zoom in on one part to see the details while the main model stays clean and readable.

## The Closing: Cratis and the .NET Ecosystem

We closed with a talk on **Cratis by Einar Ingebrigtsen**, a .NET-based CQRS platform (chosen by the community in the marketplace). OpenCQRS for Java, Cratis for .NET, AxonIQ evolving rapidly — the tools are maturing across ecosystems.

## Pattern Recognition Over Hundreds of Systems

I didn't learn Event Modeling from a dramatic "aha moment." I learned it from repetition — modeling hundreds of systems until patterns emerged. But learning accelerates exponentially in a room full of other practitioners: you can compress years of learning into two days with the right conversations.

## You're Not Alone With Your Problem

The core insight: whatever question you have, someone in that room has already solved it. Event Modeling and event sourcing are still relatively niche; most teams are isolated, figuring it out alone. This conference showed there's a community with answers.

## After the Conference Is Before the Conference

We're doing this again. It will be much bigger, maybe a different format. We're going to keep bringing practitioners together to solve hard problems.

## The Future Is Already Here

In January 2024 I said our industry would change completely within two years. In October 2025, at this conference, I watched it happen in real time. **AI + Event Modeling = the future of software design.** We're moving from writing code to designing systems; from implementation to intention; from manually translating models into software to letting AI handle that work. Event Modeling is the key that unlocks this transformation. — Martin Dilger

(Closing section was a sales pitch for Dilger's "Event Modeling Mastery" 2-day workshop + bundled online course, lifetime tooling license, and "Understanding Eventsourcing" book — trimmed. Related posts linked: "The Event Modeling Workshop That Went Until 2 AM"; "Event Modeling Anti-Patterns"; "State-Based Systems Are Doomed to Fail". © 2026 Nebulit GmbH.)
