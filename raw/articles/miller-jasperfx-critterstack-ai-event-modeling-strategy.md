---
source_url: https://jeremydmiller.com/2026/08/21/the-jasperfx-critterstack-ai-and-event-modeling-strategy/
title: The JasperFx / CritterStack AI and Event Modeling Strategy
author: Jeremy D. Miller
publication: The Shade Tree Developer
published: 2026-08-21
retrieved: 2026-08-26
type: article
---

# The JasperFx / CritterStack AI and Event Modeling Strategy

jeremydmiller — Uncategorized — August 21, 2026 — 7 Minutes

Assuming you haven't been living under a rock, you've probably noticed that topics related to Artificial Intelligence (AI) are pretty well dominating most conversations about software development right now.

I'd like to lay out the Critter Stack community and JasperFx's strategy is for AI assisted software development at this moment and talk about all the different spaghetti we're trying to throw up against the wall so that the Critter Stack and JasperFx can continue to thrive in our new world order.

## Vertical Slice Architecture

Switching to the Critter Stack's impact on application code, Wolverine has been built with what we now call "Vertical Slice Architecture" (VSA) in mind from the very beginning. That emphasis on VSA code organization has turned out to have been accidentally prescient as Wolverine's very terse approach to VSA is already very optimized for AI agentic development — especially when contrasted with more traditional server side .NET code organization that leans into layered architectures that force AI agents to burn more tokens traversing the code.

Here's a tutorial on Vertical Slice Architecture with Wolverine.

The takeaway here is that the intended idiomatic usage of Wolverine in our recommendations is already well suited for AI assisted development. The available command line tools that we bake right into your application using the Critter Stack tools can help a lot too. However, there is the very real issue of helping users utilize the AI-friendly, terse, VSA style of code when folks are coming from Clean Architecture approaches or other styles that call for more projects, layers, and abstractions that we the Critter Stack community or your AI agent ideally wants to deal with. Likewise, the usage of all those small diagnostic tools aren't terribly obvious for troubleshooting if you don't know they're there or aren't a Linux guru who's used to banging out obscure command line calls from memory.

Wolverine and the rest of the Critter Stack is very highly optimized for simple and terse code using the Vertical Slice Architecture approach, and that's great for AI assisted development!

And it's incumbent upon people like me to prove that out over time of course.

## Event Sourcing is Great for AI!

Or at least that's something that all of the folks like me that are heavily invested in Event Sourcing tooling are telling you!

Now that CritterWatch 1.0 is live, JasperFx Software has a commercial offering that gives you comprehensive MCP or command line integration with all the common APIs and capabilities of our Marten/Polecat/Fisher event stores.

## Command Line Tooling

We've long invested in command line diagnostics up and down through the whole Critter Stack just because it's a mechanically cheap way to do that, but now the AI agent usage has made those tools more valuable than ever.

Our "classic" `dotnet run describe` is the human friendly tool we've long used to dump system descriptions out for our human users and one of the first things I ask users to try to unwind many common issues with Marten or Wolverine usage, and that's not going anywhere. We've also invested quite a bit recently in additional CLI tools in Wolverine 9.0 especially that have textual output optimized for AI agents to explain message routing, preview the generated source code around a message handler, troubleshoot why a message handler isn't being found, and other common user questions. I expect we will continue to expand this support based on any trends we see with user confusion.

We're also doubling down even farther on the CLI path with the shortly forthcoming CritterWatch tooling that will provide CLI access to every bit of of an application's "Critter Stack" configuration, the dead letter queue storage, domain centric queries against Open Telemetry tracking tools you might be using such as Jaeger, and queries against any Marten or Polecat event storage including a new "projection step through" function to trouble shoot projections.

I recently wrote about how we improved and expanded our CLI tooling in the "Critter Stack 2026" wave or releases.

## CritterWatch

CritterWatch and its exposed MCP server will give you access to messaging and event workflow both from a static configuration standpoint and runtime discovered view as well. Every single bit of information exposed through CritterWatch and every single action is also completely exposed through its MCP endpoints, including access to the event stores of your Critter Stack application.

CritterWatch also comes with command line tooling as well that gives AI agents access to cross-application information about systems, workflows, messaging, and event stores.

## AI Skills

We've built, and will continue to curate and evolve a set of AI Skills files for the Critter Stack tools including Marten, Polecat, Wolverine, and even Alba to help users use our tools more effectively. For Wolverine, the AI Skills will help you write code with Wolverine idioms that lead to much tighter code — or they'll let you write the code in the conceptual way you're used to, then suggest how to adjust that code to a tighter or more performance Wolverine idiom. All of which should help you be more effective over time with AI assisted development.

The AI Skills also teach your AI agent how to utilize the built in CLI

You can purchase access to these AI Skills here on the JasperFx website. All of our support plans also include access to these AI Skills as well as the forthcoming CritterWatch packages that are hopefully available by the time you read this.

## Spec Driven Development and Event Modeling with Bobcat

We're working a little bit on our solution for "Spec Driven Development" with a tool (so far) called Bobcat. I'm not sure what exactly will land in Bobcat or be spun out, but so far it's the spiritual successor to my old Storyteller project for effective automated integration testing.

As part of that, Bobcat has a Gherkin capability for expressing executable specifications (we're not taking a direct dependency on Reqnroll yet, but I'm personally undecided about whether we do that in the long run). We're mostly going down the Gherkin path just because of the existing support inside of VS Code and JetBrains Rider for editing Gherkin documents. We'll definitely look at other models for expressing tests too (simply marking up C#/F# test code for visualization? A markdown input? Something completely different?).

Bobcat also has a "Supervisor" capability that uses the new Microsoft Testing Platform (MTP) to drive xUnit.Net (or any testing tool that supports MTP and `dotnet test`) test suites with a bit more supervised parallelism and selective test retries. The "Supervisor" is also built to "know" when and how to recycle docker containers or restart test processes based on observed test failures. That's been a god send for me doing my own CritterWatch development where the automated test suites are huge and test health can degrade as docker containers or processes have been up too long. We're also building out a little we application you can use to see ongoing test results inside of the very long running test suites — again, for my own sanity when an AI agent is running tests and you can't always tell if it's active.

This is still pretty mushy as far as details, but we're making the test output of Bobcat specifications write out quite a bit of detail about what Wolverine messages occurred, events that were appended, and HTTP calls received during the test — including the timings to help optimize test runs over time. I'm hopeful that this will be beneficial as well for AI assisted development by trying to make the tests themselves help diagnose test failures for quicker correction.

Lastly — and for the moment — we're landing an Event Modeling capability into the core of the Critter Stack, but making the future Bobcat user interface be the visualization of the models. The concept that I'm proposing so far is:

- A new model and fluent interface API in our low level JasperFx.Events library that you can use to declare event types, read model types, and any other common elements of Event Storming or Event Modeling
- A new user interface in Bobcat that can visualize the Event Modeling slices defined by that model
- Integrate `dotnet watch` with that so you can interactively doodle with slice definitions and see the model change
- Have the specified model overridden when real code is built in the system, which is making us introducing "Event Modeling" concepts directly into Wolverine and our Marten/Polecat/Fisher event stores
- Integrate the Bobcat specifications directly into the Event Modeling visualization. Rather than have people waste time writing intermediate models for policies, constraints, or validation rules in a diagram, go straight to Behavior Driven Development specifications that become actionable specs
- Add more command line options to export the event slice definitions for AI agent usage
- Expand out AI Skills so an AI agent knows how to use Bobcat specifications and our models to build systems
- Probably invest in extending our existing code generation support to build out the shell of a "slice" from the model as a first step

Philosophically, I'm coming from a background in code-and-TDD/BDD-centric Extreme Programming and I've long been very dubious about the efficacy of "low code" visual modeling approaches or application generators like JHipster. I'm also not enthusiastic about any of the intermediate DSL approaches I'm seeing for modeling event driven architectures using YAML, XML, or custom built textual DSLs. Because of the Critter Stack's relentless focus on low ceremony code, I think that we're better off just adding the visualization capabilities on top of the code rather than trying for a hugely time consuming user interface effort.

Obviously

## LLM Callouts?

I don't have any details yet, but JasperFx is going to work with at least one client to build in integrations to LLMs from Wolverine and Marten/Polecat/Fisher projections using the Microsoft.Extensions.AI abstractions.

I think that we will 100% add LLM integrations into CritterWatch in the near future.

## Agent Orchestration

This might end up being no more than a "build your own lightsaber" project for me, but JasperFx is building out its own take on an agent orchestrator and durable agent memory on top of the Critter Stack. And conveniently enough, we now have Fisher for Sqlite backed event sourcing that will be very convenient for this effort.

To be honest, I've been impressed with KurrentDb's Capacitor tool, and that's low hanging fruit for a Critter Stack-backed option.

It's somewhat likely that this tooling would either end up landing in CritterWatch or at least share the same license model as CritterWatch, but it's going to be a commercial tool all the way.

## Summary

As the imagery at the top was trying to suggest, in terms of our AI strategy, we're trying to throw all the spaghetti up against the wall right now and see what ends up sticking. And that's the best that I've got for now.
