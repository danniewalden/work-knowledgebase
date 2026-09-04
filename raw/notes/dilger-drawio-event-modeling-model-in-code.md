---
source_url: https://www.linkedin.com/in/martindilger/recent-activity/all/
title: "Are you using Draw.io for Event Modeling? (model-in-code, AI manipulation, MCP guardrails)"
author: Martin Dilger
publication: LinkedIn
published: 2026-06-30
retrieved: 2026-06-30
type: note
---

(LinkedIn post, ~7h before retrieval. Apostrophes reconstructed from a live-Chrome
text scrape; promotional/product URLs elided as [link].)

Are you using Draw.io for Event Modeling?

Nothing wrong with that, really. In discussions, I see that clients use the draw.io
xml and use AI to directly manipulate it.

"We need the model in the code" - and I fully agree.

Draw.io does a decent job, it's free, allows to serialize diagrams to XML and allows
you to keep your model in your repo - to be honest, where it belongs most of the
time.

But working like this also has drawbacks:
- it's hard to contribute directly as a non-technician typically
- AI has no framework to follow, no rules - so it's easy to make mistakes
- the xml is not readable directly, you have to use the web- or desktop viewer -
  this creates friction.
- collaboration is harder - what's not committed doesn't exist

The [Eventmodelers Plattform] fully supports that model, actually I'm using it
myself like this for many use-cases.

Make your changes, export to the standardized JSON Format. Version it in git. Use
your local agent to manipulate the json ( we provide skills for this )..

But also leverage the MCP to validate changes before commit.. this gives the agent
guardrails and feedback and prevents costly mistakes.. the agent will just
self-correct mistakes.

Visualize the JSON in the plattform Model-Viewer and make it accessible to anyone.
This is also the recommended way to clear [link] - stays yours fully.

This model also fully supports Code-Generation and AI-assisted development using our
Build-Kits with Node, Java, Kotlin..

I know what it is like to get started with this.. it's overwhelming because I was
overwhelmed.

that's why..
I wrote the book I wish I had, when I started..
I provide the training I wish I had when I started..
I host the conference I wish I could attend when I started..
now I'm building the enterprise-grade tooling I wish I had when I started..

Making Event Modeling, Event Sourcing and AI-assisted development accessible one
step at a [time].
