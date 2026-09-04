---
source_url: https://docs.eventsourcingdb.io/blog/2026/06/29/too-many-islands-too-few-bridges-notes-from-the-event-modeling-conference-2026/
title: "Too Many Islands, Too Few Bridges: Notes from the Event Modeling Conference 2026"
author: Golo Roden
publication: the native web / EventSourcingDB blog
published: 2026-06-29
retrieved: 2026-07-31
type: article
---

_Verbatim capture (via live logged-in Chrome — the piece was unreachable headless for
weeks). Two in-line photos noted in brackets; site chrome and the closing email CTA kept
minimal. Author's words otherwise unchanged._

# Too Many Islands, Too Few Bridges: Notes from the Event Modeling Conference 2026

Every once in a while, you walk into a room and feel a particular kind of energy: the sense that a community is standing at the edge of something larger than itself. The first time I experienced this was in September 2011, in Brescia, at the first Node.js Conference Italy: around 250 people from across Europe, convinced they were looking at the next big thing in server-side software. I wrote an article about it back then, every bit as caught up in it as the people around me. As it turned out, we were right.

The second time was last week, in a converted industrial space in Munich, at the two-day Event Modeling Conference 2026, with around forty other people. The same restlessness, the same sense of momentum. And one question that kept resurfacing all day, in talks and in hallway conversations alike. By the end of the second day, that question had a name, scribbled across a flip chart and signed by nearly everyone in the room.

[Photo: Golo Roden at the Event Modeling Conference 2026]

## Forty People in a Room in Munich

The conference took place at the Impact Hub Munich, a former industrial site with exposed concrete and a comfortably improvised feel. It was sold out, yet still small enough that you could realistically meet everyone over the course of two days. Nebulit organized it, and Martin Dilger held the whole thing together as host, something he did remarkably well.

The format was deliberately varied: keynotes, talks, hands-on workshops, open-space sessions, and a marketplace of short pitches, all woven together across the two days. What I appreciated most was how much breathing room there was around the sessions. Between talks, there was more than enough time to network and, just as importantly, to disappear into a side room with a handful of people and dig into a single topic in a small circle. People used that opportunity eagerly, and some of the best moments of the conference happened in exactly those side rooms.

The conference revolves around Event Modeling, the method Adam Dymitruk has done so much to shape: a way of describing how information flows through a system over time, blueprint-style, before a line of code is written. If you want a gentler introduction to the idea, we explored it in an interview on Event Modeling a while ago. Adam opened the conference with a keynote. Unfortunately, he couldn't be there in person and had to join by video. We spend a fair amount of time at gatherings like this; not long ago we wrote about our first KanDDDinsky. But this one had a different texture, and most of it came down to a single, nagging question.

## Too Many Islands, Too Few Bridges

That question, in one form or another, was this: why is it still so hard to find your way into this field?

Because the field that calls itself Event Sourcing, CQRS, and Domain-Driven Design isn't really one field. It is an archipelago. There are many schools and many flavors of how to do this work. Do you model with aggregates or with dynamic consistency boundaries? Do you do Event Storming, model using Event Modeling, or tell stories with Domain Storytelling? And even the words differ: is it an event or a domain event, a command or an intent, a read model or a projection? Each camp has its own vocabulary, its own preferred tools, and its own conventions, and each is internally coherent and externally hard to reconcile with the others.

The fragmentation reaches further than methodology. It runs all the way down to the examples we teach with. For example, WPS reaches for a cinema box office to explain Domain Storytelling. Bastian Waidelich and Sara Pellegrini, in contrast, use a student enrolling in courses. We at the native web, for our part, usually tell the story of a city library. Three teachers, three canonical "hello world" examples, and a newcomer left to work out, entirely on their own, that all of these are really describing the same handful of underlying ideas.

It shows up in tooling, too. One team builds on Axon, another on a framework it built in-house and never published; we build on EventSourcingDB, with OpenCQRS and Nimbus. Each choice is reasonable on its own island, and each comes with assumptions that quietly leak into how people think the whole field works. The result is that what you learn in one camp is only ever a slice of the whole, and it takes a very long time to figure out who belongs where and how the pieces actually fit together.

That cost lands squarely on the people we should most want to welcome. There is remarkably little that we, as a community, have actually agreed on. We all do something we call Domain-Driven Design, with something event-shaped around it, but there are almost no shared standards and almost no shared examples to point a beginner toward. This is exactly the spirit behind something we have argued before: that great minds should not think alike, they should think together.

None of this is a complaint about diversity. The variety is a sign of a living, curious, genuinely creative field, and I would not trade it away. But diversity without shared reference points isn't richness. It is fragmentation. We have plenty of islands. What we are short on are bridges.

## What If We Built a Foundation?

On the afternoon of the second day, that diffuse frustration finally crystallized into a concrete proposal. What if this community had a foundation of its own, something in the spirit of the Linux Foundation or the CNCF, to give it a shared backbone?

The discussion that followed was lively, and it produced far more ideas and open questions than a single afternoon could ever resolve. Who would steward it? What would it own first? How do you create something neutral enough that every island trusts it, yet opinionated enough to be useful? No one walked away holding a charter or a set of bylaws. But everyone in the room did agree on one thing: this is worth pursuing. That shared commitment, written out and signed by the room on a flip chart, became "The Munich Event."

The aims, as they took shape in the conversation, started exactly where the pain is sharpest: standardization. A shared terminology, shared file formats, shared examples, all the connective tissue that lets one island's work mean something on the next. And beyond that, a second goal: spreading the word, so that Event Sourcing and Event Modeling reach the wider audience they deserve, rather than staying the quiet specialty of a few.

It is a modest artifact, that flip chart. A few sentences and a column of signatures on a sheet of paper. But the most consequential things often start out looking modest, and what mattered was never the paper. It was that a roomful of people who usually inhabit different islands had, for one afternoon, agreed to start building toward each other.

## Your Domain Model Belongs in the Repository

And then it was my turn, with timing I couldn't have arranged if I had tried. My talk was titled "Your Domain Model Belongs in the Repository," and its argument ran straight through the fault line the room had spent the afternoon circling.

It rested on two claims. The first: we need far more standardization than we have, from the words we use to the file formats we exchange, because meaningful exchange is impossible without it. The second is the uncomfortable one. Nearly every modeling effort, no matter which method it uses, ends the same way. The whiteboard fills up, someone takes a photo, the photo gets pasted into a wiki, and then no one ever looks at it again, let alone keeps it up to date. The model dies the moment the workshop ends.

The word "repository" in the title is meant literally: a Git repository. The domain model belongs right next to the code, so that the two can be changed together, in a single coherent pull request, and reviewed as one unit. When the model is a versioned, plain-text artifact, it gains everything the code already has: diffs, history, review, blame, and a single source of truth that can't quietly drift out of date. A model that lives beside the code is a model that stays alive.

This is where ESDM (Event-Sourced Domain Model) entered the talk, not as the point of it, but as one concrete attempt to build a bridge. ESDM is a YAML-based language for describing event-driven systems. It captures the building blocks of Domain-Driven Design, CQRS, and Event Sourcing (aggregates, events, commands) in a single shared format. Because it is plain text, it lives in your repository. Because it is structured, tools can read and write it. And because it is structured, so can an AI.

That last point was the heart of the live demo. While I talked through the concept, I had an AI assistant working in the background. First it ran backward: it took an existing application, analyzed it, and reverse-engineered an ESDM model out of the code. Then it ran forward: from that single model, it generated two working implementations, one in Kotlin and one in Python. One model, two languages, derived live on stage, the closest thing to a bridge you can show in five minutes. It is the same conviction that drives our work on Event Sourcing and AI: structured, machine-readable history and models are exactly what these tools need to be useful.

The reaction is the part I keep coming back to. People were glad it simply worked, which is never a given with a live demo. But what they responded to most was the direction of it: here was a tool aimed squarely at the gap we had been circling all day. If you would like to see what a model that lives beside your code looks like, ESDM is free and open for commercial use, a good place to start.

[Photo: Martin Dilger and Golo Roden at the Event Modeling Conference 2026]

## Where I've Felt This Before

The thing about Brescia in 2011 is that the bet paid off. Node.js did not take over the world because the technology was flawless; it took over because a community held on to its enthusiasm long enough for adoption to catch up. The energy came first, and the ubiquity followed years later.

Munich felt like that earlier moment: not the part where everyone already agrees you were right, but the part before it, when a small group can sense the shape of what is coming and quietly decides to build toward it. The bridges aren't built yet. The Munich Event is still a sheet of paper rather than a foundation, and ESDM is young. But for the first time, the will to build those bridges felt shared rather than scattered.

That, more than any single talk, is what I carried home. And it comes with an invitation. If you care about giving this community shared standards, shared examples, and shared tools, if the idea of a foundation resonates with you, or if you simply want to tell us where ESDM gets it wrong, we would genuinely like to hear from you at hello@thenativeweb.io.

The islands aren't going anywhere. Let's start building the bridges.
