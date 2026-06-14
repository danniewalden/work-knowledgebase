---
source_url: https://akka.io/blog/agentic-systems-are-distributed-systems
title: "Agentic Systems Are Distributed Systems"
author: Kevin Hoffman (Akka / Lightbend)
publication: Akka Blog
published: 2025-08-19
retrieved: 2026-06-11
type: article
topic: event-modeling-and-agentic-ai
capture: faithful full text (site nav/footer removed)
---

# Agentic Systems Are Distributed Systems

5 minute read · August 19, 2025 · Posted by Kevin Hoffman, Director of Product Management

## *All enterprise agentic systems at scale need to be distributed systems*

In our blog posts, videos, and conference talks, we've been spreading the word that [event sourcing is the key foundational technology](https://akka.io/blog/event-sourcing-the-backbone-of-agentic-ai) on which agentic systems should be built. This is because the built-in features you get with event sourcing are the same elements of the core foundation your agentic applications need.

In this post, I want to take a step back from event sourcing and talk more broadly about distributed systems and the notion that you can't build and deploy agentic systems to production without them also being distributed systems. As a result, your agentic platform needs to inherently be a distributed systems platform.

Let's start with the features your agents are going to need and from there discuss how those components relate to distributed systems.

### Distributed memory

If you've used AI assistants and agents, then you've encountered memory in one form or another. The simplest form might be where an agent maintains the conversation history for a specific session (short-term) or possibly all conversations with a certain user (long-term).

In a monolithic application, you might maintain some of this conversation history (especially short-term) in memory within a process. At some point you'll run into performance issues when conversation history isn't readily available in the same location as the agent. While it's easy to assume everything is in the same place (and possibly even in the same memory space) with a monolith, we have to assume data is not only out of process, but likely off-node in a distributed system.

A first attempt at shared memory might be to store the conversation history in a central database. Depending on needs and scale, even that might not be enough. Moving toward a distributed system pattern where agents and their memory are colocated is ideal for performance reasons but can also be used to help with compliance and data locality rules.

Conversation history is what provides the bulk of context for prompts, so we can't afford to lose this data under any circumstances. From an event sourcing perspective, storing agentic memory as a sequence of immutable events makes perfect sense.

If each memory interaction for an agent (or a group of collaborating agents) is an event that can be replicated close to wherever it is needed, then we get a free, built-in distributed backbone for our agentic system.

### Streaming I/O with LLMs

Most interactions with LLMs are streaming interactions. Agents submit token streams as input to the model and they receive token streams as output. This doesn't present much of a problem when we're working with "hello world" demo applications running on laptops.

But in production, it's a much different story. In real deployments, it is possible for the LLM to become unavailable or unresponsive. This can be due to load–something that's happening more and more lately–or network partitioning events that constantly plague cloud infrastructure.

Agents need to be able to deal with this data cutting off mid-stream and potentially resuming at a different point. We need to expect that the network locations of agents and models can change radically between any two calls.

If your agents can't deal with intermittent connectivity and data loss, backpressure and inconsistent streaming speeds, or any of the hundreds of other stream-related edge conditions then they will be a critical point of failure for your agentic application.

### Stateful orchestration

We need to be able to do per-agent orchestration (sometimes called "micro orchestration") where we manage single-agent failures, network connectivity loss, retries, and exponential backoffs during failures. These are all basic features of reliable, distributed systems.

In addition to the per-agent orchestration, we need to be able to orchestrate the collaboration between agents in the system. Just the presence of words like orchestrate and collaborate tell us that we're dealing with intrinsically distributed systems.

Let's take a simple planner example. You're building a fitness application that uses historical customer data to make multiple recommendations for both indoor and outdoor activities, as well as adding hydration breaks to a schedule.

Triggered by some stimulus (maybe customer input), you've got a planner agent that uses an LLM with RAG/contextual prompts to plan the work that needs to be done by multiple agents. Assume you've got the top-level planner agent, a weather agent, an indoor activity planner that has multiple tools for querying facility availability and hours, an outdoor activity planner that has tools for querying weather forecasts, UV indexes, and more.

When everything is local and predictable, this kind of orchestration doesn't sound too difficult. But now assume that none of the agents are on the same node in a multi-region cluster. Further, the source of event replicas is also somewhere else.

Something needs to keep track of the single source of truth for the state of the orchestration flow (which is derived from immutable, replicated events). Logic needs to be written to deal with failures and timeouts at multiple steps. You'll also want to be able to run multiple agents concurrently when there are no linear dependencies.

Gathering results from multiple concurrently running agents across different regions and clusters is no small feat, let alone being able to do so with guaranteed SLAs while handling streams and entities and workflows in different locations.

When you're evaluating an agentic framework, you want to consider more than just how easy it is to write an agentic "hello world." You need to consider what it looks like to build and operate a globally available, resilient, high-performance solution.

### Semantic search and context generation

Semantic search is a crucial part of agentic workflows for tasks like Retrieval Augmented Generation (RAG) and context generation and enrichment. Most agents don't just have a stateless interaction with an LLM, they have enriched conversations.

When your users ask your agents to perform work, they will often query vector databases and other data sources before sending a prompt. Not only does this automatically classify your application as a distributed system, but now you've got to deal with intermittent failures, timeouts, and disconnects when talking to multiple data sources.

Any part of your agentic application that assumes success and only supports the "happy path" is not ready for production and will cause real problems when deployed. In addition to the basic resilience patterns you need around communicating with context sources, you probably want to control the location of agents and their data sources.

A common pattern is to optimize the location of an agent (and/or the agent's session) to be as close to the customer accessing it as possible. Applications built in the monolithic style of demos and proofs of concept aren't going to be flexible enough to handle these kinds of optimizations.

### Running resilient components in clusters and regions

There are many important reasons to want to control where services are running. In addition to wanting to shorten the distance between the customer and their services and data, there are also resilience and scale concerns.

In the world of monoliths, one bad thing can take down the entire application. Running one instance of a service creates a single point of failure (SPoF); a liability in distributed systems.

What most of us want is to have components that are free to move around our infrastructure to optimize for performance and reliability. We want to have a backup version of a component take over immediately if the primary fails. If we lose an entire set of infrastructure in a region due to a cloud provider outage, we want another region or cluster to be able to take over and carry the load.

All of these things are usually a nightmare to build and maintain, but the Akka platform (especially Akka Automated Operations) makes it easy and declaratively maintained.

### Summary

It's very easy (and tempting) to look at all of the shiny agentic AI demos and assume that you can take those demos to production. Any application with agentic AI components needs to be supported by a robust set of frameworks and tools for distributed systems. Before you start deploying AI demos to production, ask yourself if that demo is going to work in real-world scenarios with network failure, unpredictable load, and demanding requirements for fault tolerance and resiliency.

Don't be fooled by the time to release an unreliable, unscalable demo. Plan for the time to release a reliable, scalable, production-ready application.
