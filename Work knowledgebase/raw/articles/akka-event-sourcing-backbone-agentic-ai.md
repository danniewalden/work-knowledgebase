---
source_url: https://akka.io/blog/event-sourcing-the-backbone-of-agentic-ai
title: "Event Sourcing: The Backbone of Agentic AI"
author: Kevin Hoffman (Akka / Lightbend)
publication: Akka Blog (video + transcript)
published: 2025-08-08
retrieved: 2026-06-11
type: article
topic: event-modeling-and-agentic-ai
capture: full transcript verbatim (timestamps preserved; site nav/footer removed)
---

# Event Sourcing: The Backbone of Agentic AI

Video · 9 minute read · August 8, 2025 · Posted by Kevin Hoffman, Director of Product Management

Video: https://www.youtube-nocookie.com/embed/4qbVqlt-Pkk

### About the video

Agents can't exist in a vacuum. They need a supporting cast and there's no better foundation than Event Sourcing

**Transcript**

0:00: Hey everybody, my name is Kevin Hoffman, and in this video I'm gonna be talking about event sourcing and how this powerful pattern forms the backbone for building real world agentic AI applications.

0:13: Before I get started, let me cover just a little bit about me and my background.

0:18: I'm the author of Applied event Sourcing with ACA, Real World event sourcing.

0:24: And programming web assembly with rust.

0:27: I basically eat, sleep, and breathe event sourcing and distributed systems.

0:31: In this video, I'm gonna give a quick overview and background on what agentic AI actually means.

0:38: From there I'll talk about the pretty rigorous demands agentic AI puts on a system.

0:44: And then I'll finish up with a discussion of how event sourcing and specifically event sourcing with ACA has everything we need.

0:54: So let's talk about what agentic actually means.

0:57: Something that is agentic, as the name implies, can act with agency.

1:02: It can act independently to achieve outcomes or goals.

1:06: Agentic is stateful and capable of making decisions.

1:10: Agentic AI is a superset of agentic, and this means that AI is used in some way to achieve goals.

1:18: If you only take away one idea from this video, it should be that prompt engineering is the most important aspect of building agentic systems.

1:26: You may also have heard the term context engineering.

1:30: They both refer to the idea that the precision you use when talking to an LLM will determine success or failure.

1:38: The sections of this slide in yellow are what is called the system prompt.

1:42: When you ask your favorite LLM if it thinks you should eat a burrito, the application you're using is going to wrap that question with context, instructions, and guidelines.

1:52: Here you can see that we've supplied some context about how good burritos are.

1:56: The LLM will take that into account for its reply.

2:01: As easy as it is to believe that these large language models understand what we're saying.

2:06: That isn't the case.

2:08: Instead, when we supply a prompt to a model, the first thing we do is tokenize the text.

2:13: This means breaking it up into chunks.

2:15: These chunks are then converted into what's called a vocabulary.

2:20: this vocabulary is a mapping between the human readable tokens and their numeric counterparts.

2:26: It's important to remember that this vocabulary is specific to the algorithm or model that generated it.

2:33: This means that you can't take a set of token IDs from one model and expect it to work on a different one.

2:41: Finally, each of these token IDs is converted into a vector.

2:45: You can think of this vector as a really large set of floating point numbers.

2:51: They're kind of like instructions on a map, leading the model from a starting point to each of the tokens.

2:59: As I mentioned, LLMs communicate via tokens.

3:02: We stream tokens into them and we get streams of tokens out of them.

3:07: The reason this is important is because for most of the models that are hosted or managed by other providers, we have to pay for tokens.

3:15: When you're looking at the payment plans, it's easy to think it'll be cheap when you see buckets of millions of tokens.

3:21: This is a dangerous assumption as tokens can build up rapidly.

3:25: Remember that creating the vector embeddings uses up tokens, sending input uses tokens, and getting output uses tokens.

3:35: At some point in your agentic journey, you'll have to weigh the trade-offs between paying for tokens or paying for the infrastructure required to host a model that doesn't charge by the token.

3:48: So, let's get into a bit of detail on the components that make up the new buzzwords of agentic AI.

3:56: The thing that makes agents so powerful is context.

4:00: Agents receive context from the environment, things like users, sensors, events, data streams, and integrations.

4:08: Agents are goal oriented.

4:11: Usually you'll see agents with fairly narrow goals, and then some orchestrating supervisor is responsible for weaving multiple agents together to perform complex tasks.

4:22: Agents can be autonomous, which is a double-edged sword.

4:26: Sometimes this is powerful and helpful, but an agent given too much autonomy and privilege can wreak havoc.

4:32: Agentic AI also implies learning.

4:36: Whether the context for prompts gets more precise over time or whether models are being refined, we hope that our agentic systems get better the more they're used.

4:45: Last but not least, we have the concept of adaptability.

4:48: Agents, or more typically agent orchestrators can change their goals and strategies.

4:54: They can dynamically choose the best models for a given task, and agents can even be used to plan out how other agents are going to be used to solve problems.

5:05: Now that we've had a bit of background about what agentic AI is and how it works.

5:10: Let's start talking about how this all relates to event sourcing in ACA.

5:15: At their core, a agentic systems are distributed systems.

5:18: Communication with LLMs is event-based and streaming.

5:22: Agents have an event-driven architecture that can include human in the loop interaction, real-time data ingestion, resiliency tasks like failover and retry.

5:33: These distributed systems also separate the read and write models, which is a perfect match for event sourcing.

5:40: All right, now we get to talk about yet another buzzword, rag or retrieval augmented generation.

5:48: LLMs only know what they were taught as of the cut-off date for their training.

5:52: This means that anything that happened after this date will be a complete and total mystery to the model.

5:59: To compensate for this, we can supply the additional knowledge that the model needs as context within the prompt itself.

6:07: It's this context augmentation that gives the phrase its name.

6:11: In addition to filling in the gaps in the LLM's general knowledge, retrieval augmentation can also be used to provide access to internal or private data.

6:21: Such as a customer's purchase history or data that belongs only to one company and so on.

6:29: Agents are very needy, high maintenance things.

6:32: Agents need some way to store and retrieve memory or conversation history.

6:36: They need to be able to make additional queries to augment the prompt context.

6:40: They need to stream asynchronously both in and out of an LLM.

6:44: Some agents can utilize tool call backs and so that needs to be supported as well.

6:49: LLMs and by extension agents are nondeterministic.

6:54: We can't predict from one call to the next how they're going to react, so we need a way to evaluate and judge the performance of the model.

7:02: To measure our confidence or lack of it in the results.

7:08: OK, so now that we've covered what agents need, we can talk about how event sourcing makes perfect sense as the core foundation of any agentic system.

7:17: Event sourcing provides perfect recall.

7:19: Since everything that took place in an event sourced system is captured as an immutable event, we can reliably reproduce the state of any agent at any given point in time.

7:30: Not only do we know and have the ability to regenerate state, we also know why the state is that way.

7:37: This means we can audit everything in the system, which is crucial when parts of the system are nondeterministic.

7:45: By making the choice to embrace event sourcing, our agentic systems also get a ton of things included in the package.

7:52: We can do fearless experimentation and run what if scenarios, as well as use event logs to feed and inform fine tuning and context engineering.

8:03: Event sourcing means that autonomous agents can act in concert and communicate with each other through durable events.

8:10: We can even deal with agent and event versioning through replay and regeneration.

8:16: I want to finish up the main content of this video by showing this symbolic backbone.

8:22: Event sourcing is the central supporting column for all of the key features of agentic systems like memory, rag, multi-agent, and multi-modal operation, tool integration, and vector embeddings.

8:35: You might be wondering what you should do next to learn and keep up to date with all of these rapid AI innovations.

8:41: From an ACCA standpoint, you can go to our website and follow the Getting Started tutorials and the guided tours through the documentation.

8:49: There's no substitute for hands-on experience building, so go out there and tinker.

8:54: Build and break things and learn from it and see how those lessons can be applied to your work.

9:00: I mentioned earlier in the video that prompt and context engineering are absolutely critical to being successful building agentic systems.

9:09: As such, any time invested in learning about those subjects is well worth it.

9:15: Thanks for checking out this video and I hope you got inspired to go roll up your sleeves and start playing with all of this agentic AI stuff.

9:24: Check out our other videos and documentation for more guides, walkthroughs, and fun demos.

---

*Note: the transcript is auto-generated and contains transcription artifacts — "ACA"/"ACCA" refer to **Akka**.*
