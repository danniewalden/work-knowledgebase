---
source_url: https://www.prefect.io/blog/loops-vs-graphs
title: Loops vs. graphs
author: Jeremiah Lowin; Radhika Gulati
publication: Prefect (FastMCP podcast, episode 3)
published: 2026-07-22
retrieved: 2026-07-31
type: article
---

# Loops vs. graphs

*(Edited transcript of episode three of the FastMCP podcast: Radhika Gulati (Product Marketing) in conversation with Jeremiah Lowin (CEO).)*

Peter Steinberger sent everyone into a frenzy with an almost throwaway tweet asking whether we're still talking about loops or whether we've moved on to graphs. Overnight, our feeds filled up with graph engineering, the death of loops, and a lot of people rediscovering their college algorithms class in public. Jeremiah introduced directed agentic graphs at a keynote over a month ago, and they've been a product imperative at Prefect since our all hands back in April. If the world is ready to talk about graphs, we have a lot to say. So for episode three of the FastMCP podcast, Radhika Gulati (Product Marketing) sat down with Jeremiah Lowin (CEO) to work through what graphs have to do with your agents, from the perspective of a company that has spent years building orchestration software on top of them.

What follows is an edited version of that conversation.

## First, what even is a graph?

This is where the topic gets boring in a constructive way, which is exactly why we like it. A graph is a data structure that represents information as nodes, which you can think of as boxes, and edges, which are the lines that connect those boxes to each other. Two nodes and an edge between them is a graph. Add a third node, connect it however you like, even loop the last one back to the first, and you still have a graph. That's the whole idea: a way of representing information in a connected, weblike form.

It turns out to be one of the most useful ideas in computing. The internet is a graph of how web pages link to each other, which was Google's big insight. Social networks are graphs of how people connect, which was Facebook's. And at Prefect we've built our whole product around them: we build, discover, and execute graphs for orchestration and workflow automation, representing the work to be done as a graph of functions to call. Dagster, which just joined the Prefect family, uses a graph to represent the assets your data pipelines build and the lineage between them. So when graph talk took over the agent world, it landed in very familiar territory for us. What surprised us was seeing this nuanced, very explicit way of mapping work show up among agents, where it has historically felt contrary to what people actually want to do.

## From prompts to loops to graphs

Graph engineering is the latest entry in a progression. We went from prompt engineering, where you ask the agent to do something and it comes back with a response, to multi-prompt approaches with several requests and responses, to loop engineering, where you set the agent off on an objective and it iterates over and over until it meets a goal. All of these are ways people try to take more control of their agents' behavior, and they all recognize the same thing: the more structure you give a workflow, the more powerful it can be, and the longer you can keep an agent on a prescribed path, the better the outcome.

In our opinion there's also a goal missing from most AI engineering today, which is reproducibility. Keeping the agent on rails means this run looks like the last hundred, and you can actually compare them.

## The Ralph loop problem

What's a little sad about all of this is that powerful ideas tend to get boiled down to the dumbest version of themselves that can be broadly understood. Loop engineering is a genuinely powerful way of creating goal-seeking behavior, something we know well from machine learning, where loops are paramount in both training and goal seeking. When it translated into agents, it showed up as the Ralph loop, the most swallowable possible version. That's not entirely bad. Plenty of people who started there moved past it and did real loop engineering. But the simple version became the representative one.

With graphs, we honestly don't know what the dumb version looks like, because the entry fee is high. Graphs are hard. Maybe the simple version is already here in features like dynamic workflows in Claude, which do automatic sub-agent delegation. People are already using graphs without knowing it, too. When you fan out sub-agents in Claude, you're not sitting there thinking about graph traversal, but a graph is exactly what you've built. Most people will probably never encounter one as an explicit thing in their world, even as graphs quietly shape more and more of what their agents do under the hood.

## What a directed agentic graph actually is

Go back to nodes and edges, and make them concrete. In our definition, a node is a unit of business logic or work, most likely carried out by an agent. An edge is the path you follow from a decision that agent makes to the next invocation in the graph.

Take a simple example. One node asks an agent to look up a customer's information, with two edges fanning out to two new nodes. If the agent finds the customer, we follow the first edge to a node where the agent takes some action on that customer's information. If the customer can't be found, we follow a different edge to a node that handles that case instead.

This is a directed graph, which means edges are only followed in a specific direction. Once you've moved from the first node to the second, you don't get to reverse down that edge; it's a one-way street. If you've spent time in the orchestration world, this is ringing bells, because a DAG, a directed acyclic graph, has been the standard way of describing a workflow for decades. Acyclic means no loops back: once you've left a node, no path is allowed to return to it. In this new world we see no reason for that constraint to survive, so we want to rebrand DAG as a directed agentic graph: a directed graph that governs agent behavior, where each node represents the invocation of an agent in a harness, and where the parameterization, the skills, the tools, the access, the instructions, even the model itself can all be set at the level of that node.

To see why the node-level settings matter, imagine the degenerate case: a graph with a single node, where the agent gets every tool and every instruction it could possibly need and churns until it's done. That's loop engineering reinvented, and the graph structure is doing nothing at all. The moment you split it into two nodes with an edge between them, you can supply different tools in each, use a more powerful model for the hard first step and a cheaper one for the second, or make the second node purely programmatic, ordinary code that runs conditional on the agentic decision made in the first. Inside each node, the agent goes off on its loop and does its thing. Across the nodes, you can observe, configure, and govern the whole behavior.

## Why businesses care about this more than individuals

Frankly, we're surprised to see this conversation happening at the individual level at all. As an individual, you fire up Claude or ChatGPT, ask it to do something, and maybe it uses a graph invisibly, maybe it loops, maybe it just responds. You don't really care about the structure of that interaction, and most of the time you shouldn't have to.

When agents show up inside a business, as part of a product, or in front of customers, you inherit concerns that never applied to your personal chat sessions: reproducibility, auditability, and the ability to understand what happened. Invoke an agent the current state-of-the-art way, over an API with some harness or loop engineering around it, and you have no real way of knowing whether it takes the same path to the goal every time. You also get very few chances to evaluate it, other than waiting for the whole thing to finish and inspecting whatever side effects it left behind. For something simple, like translating one data structure into another, that can be fine. For a ten-step workflow that decides whether to issue a customer a refund and then actually issues it, it's where the customers we talk to start to get very nervous. Model that workflow as a graph instead and you can observe progress programmatically, and you know it will move through the same series of steps every single time.

## Control versus autonomy, the central question

Fundamentally, what graphs let you do is modulate between control and autonomy, which in our opinion is the central design question when you work with agents. The magic of agents is that you set them off and they figure it out, making decisions in ways that would be genuinely difficult or impossible to code deterministically. The downside is that if they make it up as they go every time, it's very hard to reason about their behavior, put constraints around it, or answer questions like "over the last hundred times the agent did this, where did it tend to mess up?" Without a data structure that maps what the workflow even is, you end up with handwavy observability and agents self-reporting their own progress, which breaks down at any reasonable scale.

A graph gives you boundaries to modulate with. Inside a node, the agent has full autonomy. When it finishes and follows an edge, control comes back to you. That interplay is the thing we think the ecosystem needs to build an intuition for very quickly.

So how many nodes should your graph have? This is a design question, right now much more art than science, and it's the same question Prefect users have asked us for years about tasks. Our answer hasn't changed. Think about the units of work. Where do you want checkpoints? Where do you want to say "retry this three times" or "escalate immediately if this fails"? A ten-step workflow doesn't need to be ten nodes. It should have a node boundary wherever you want to reason about progress, intervene, or interject programmatic logic, and nowhere else. If you don't actually care about observing any of it, collapse the whole thing into one node and you've regressed to loop engineering, maybe all the way to prompt engineering. What's nice about graphs is that they permit that regression without requiring you to leave the paradigm, so the door stays open to more sophisticated approaches later.

## Don't hand your agent a bazooka

Come back to the refund agent, because security might be the strongest reason to reach for a graph at all. The state-of-the-art way to build one today is to write a skill listing the ten things to check before issuing a refund: the transaction is in the eligible window, the customer has a valid payment method, the order is real. Then you give the agent a tool that can send refunds and ask it to run the workflow.

What you've actually done is hand the agent the capability to issue refunds, along with a polite note explaining how you'd like it done. Anyone who has worked with agents for more than ten minutes knows they don't even always read their skills. So if it reads the skill, and follows the steps in order, and decides responsibly, and targets the right customer ID, and the customer didn't inject any confusing instructions into its worldview, then everything works. If any one of those fails, including the agent just getting lazy and skipping a step, you have a problem that's incredibly difficult to diagnose, because the agent will come back and cheerfully report that it did a good job and sent a refund. As far as we know, nobody is brave enough to put this in production, and they're right not to be. On past episodes we've described this as asking an agent to make a sandwich and handing it a bazooka in case it runs into any zombies.

Now split it into even a simple graph. The first node does all the diligence on the customer. It's the part that genuinely needs an agent, because it isn't programmatic, and that agent cannot issue refunds. Its only job in life is to decide whether a refund should happen. Only after that decision, past a programmatic moment where control returns to the orchestrator, does a new node get the refund tool: locked to the one customer it's supposed to affect, usable exactly once. The non-destructive work gets done where the dangerous tool doesn't even exist, and the destructive, one-way work gets done in a fresh harness where it does. You could call this harness orchestration as much as agent orchestration, and it's why we think people will actually adopt graphs. Reproducibility and easier reasoning are real benefits, but the number one reason is the ability to change an agent's capabilities depending on the path it took to get there.

## Humans in the loop, as nodes

The same structure fixes another awkward pattern: human approval. Today you either bake approval into every tool call, hope the skill says "don't do this unless a human signs off," or wait for an MCP elicitation after the tool has already been invoked. With a graph, a human-in-the-loop moment is just a node. The agent achieves its objective in one node, the workflow moves to an approval node where a person decides, and the next agentic node runs conditional on that decision.

Stepping all the way back, that's really what an agentic graph is: nodes that represent outcomes, and edges that represent what happens next once a decision comes out of that outcome. Most of the time an agent produces the outcome, but nothing stops a node from being a human approval, programmatic code execution, or simply sleeping and waiting for an external event. All of these are valid things to drop into the graph.

## Where LangGraph and Pydantic AI fit

If you've seen graphs in the agent world before, it was probably at a lower level. Frameworks like LangGraph or Pydantic AI's graph model an individual agent's internals, its tool choices and lower-level capabilities, as a graph, and that's effective. It's also not what we're talking about. Directed agentic graphs are macro orchestration across potentially many agents, where each node is a full agentic invocation. The agent inside a node could itself be built in LangGraph, Pydantic AI, or any other framework that models its micro behavior. We're modeling the overall workflow around those agents so it's reproducible, governable, and auditable.

## About that tweet

So what was Peter Steinberger actually saying? Honestly, we're not sure. The least charitable reading is that the AI world is thick with signaling that you've thought of something before everyone else. What we'd hope from people with that kind of influence is that they use it to drive good outcomes rather than sending a crowd off to rediscover graph theory from scratch, because there are decades of experience and literature here, and without that connection being drawn, people are going to make every mistake the orchestration world already made and invite a new round of slop while they're at it.

We don't love being the people who show up and say "calm down, here's the boring way that works." But somebody has to say that there is a sane way to do this, one that borrows from best practices developed over decades, and the window for the ecosystem to adopt it, rather than watching the worst version become the representative one the way the Ralph loop did, is open right now.

## What this means for Prefect

Every ten years or so, the same fundamental question of how to automate work gets trotted out in new dress for the technology of the day. Today it's agents: how do I automate them, how do I trust the outcomes they deliver, how do I triage them when something goes wrong. We're updating Prefect for exactly this, with the directed agentic graph as the front-and-center representation of agent behavior. You'll be able to look at a workflow and see what the conditional paths are and what happens when it fails at any point, then watch the agent make its way through that structure as an observable, reproducible, understandable workflow, with different capabilities at different times.

This is where the Dagster acquisition fits too. Dagster's product is fundamentally graph-based, built around asset graphs and lineage, and that experience is joining Prefect's durable runtime for executing the agent loop. It feels like an Avengers-assemble moment for the product lineup. And to be honest about the proportions: it's 95% things we've been doing for decades, and 5% new magic sparkles because it's AI and needs some special handling. With people, we never get the option of putting them in a data structure and having it forcibly executed, but we absolutely map out our processes and we absolutely follow them. This is the equivalent for agents, and it's about as close as we can get to a deterministic framework, which is where the confidence that work gets done a specific way actually comes from.

## Wrapping up

Jeremiah gave a keynote on directed agentic graphs at PyData London about a month and a half before everyone's feed filled up with graph talk, so the honest summary is that this has been coming for a while, and it's arriving sooner than we all thought. If you're one of our early access partners, you're probably already playing with some of the technologies described here. If you'd like to be, reach out to our team, and there will be a much bigger push in the coming months when this is production ready.

Same deal as every episode: if something about graphs, agents, or MCP is confusing you, leave a comment. We read them, we respond to them, and we'll turn the good ones into the next conversation.
