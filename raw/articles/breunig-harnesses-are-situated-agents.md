---
source_url: https://www.dbreunig.com/2026/08/14/harnesses-are-situated-agents.html
title: Harnesses are Situated Agents
author: Drew Breunig
publication: dbreunig.com
published: 2026-08-14
retrieved: 2026-08-24
type: article
---

# Harnesses are Situated Agents

### The best way to define a harness is as a "situated agent"

Tags on the original post: AI · HARNESSES · AGENTS · SYSTEMS

[Harrison Chase](https://x.com/hwchase17) once excitedly shared an insight that agents are comprised of 4 things: a system prompt, a planning tool, a file system, and subagents. In the year-plus since he said that, I think this remains largely true. (Though you might tweak it to have general tools, etc.)

Lately, we've been experiencing a wave of *harnesses*. It seems like everyday a new coding harness lands. I'm sure we'll see another few dozen before the month is out.

Recently, there's been:

- [Omnigent](https://databricks.com/blog/introducing-omnigent-meta-harness-combine-control-and-share-your-agents) from Databricks, which is a "meta-harness" that calls out to Claude Code, Codex, Pi, and others.
- [DeepSeek Harness](https://deepseek.com/harness/en) landed with the new DeepSeek V4-Pro, and is totally modular. Models, tools, skills, sessions, sandboxes, storage, loops, scheduling, and the UI are all swappable
- [Buzz](https://block.xyz/inside/introducing-buzz-where-humans-and-agents-work-together) is Block's new thing, and because it's Jack Dorsey it's a Nostr social network for agents and humans.
- [QM](https://qm.ycombinator.com) from YCombinator gives us org-shaped scoping: each employee, Slack room, and project gets its own memory, files, credentials, permissions, schedules, and sandboxed execution.
- [Flue](https://blog.cloudflare.com/agents-platform-flue-sdk) from CloudFlare uses a declarative pattern, which is pretty unique becaause it hides the loop from users.
- [Muse Code](https://developer.meta.com/ai/products/muse-code/) from Meta, whose model, Muse Spark 1.2, was co-trained with the harness itself.

And then there's [OpenClaw](https://github.com/openclaw/openclaw), [NanoClaw](https://github.com/nanocoai/nanoclaw), [Hermes](https://github.com/NousResearch/hermes-agent), [Conductor](https://conductor.build/), [Prime Agent](https://github.com/PrimeIntellect-ai/prime-agent), and more.

We've seen enough at this point that the common patterns are starting to emerge. Each brings something unique, but *they're more alike than different*. And that's great, because that lets us find the metapattern here. Which brings us back to "situated agents."

I like this framing. Harrison's 4 elements of an agent remain – the system prompt, planning tool, file system, and subgents – describing the core loop. This is the core loop the developer controls with the keyboard. The *harness* manages everything beyond this, the world the developer sits within.

Imagine the simplest coding agent, and you at the keys. Let's slowly zoom out and consider all the elements *the harness* can manage:

1. **The Session:** The current task and context, as both a trajectory and a durable, branchable log. You can zoom backwards, fork, and replay it.
2. **The Environment:** The instance, defined as a sandbox, terminal, worktree, computer, and/or container.
3. **The Repo:** The project. Versioned with Git, it contains your code, history, current work, `AGENTS.md`, guides, and hooks.
4. **Memory:** The person's predilections, accrued over time, managing progress and past decisions.
5. **Skills:** The domain, artifacts describing reusable workflows or domain knowledge worth wielding in this situation.
6. **The Team:** Your colleagues and counterparts. Shared rooms, shared traces, project tracking tools, issues, and bug reports.
7. **The Organization:** The policies and audits, defined by legal, leadership, and procurement.
8. **The Model:** The LLMs themselves, the common artifact shared by all. Stochastic blobs we all poke trying to evoke positive outcomes. Log or train on their quirks and adjust.

*As we move outward, each layer is used by more people and changed less often.*

Harnesses account for the above layers, fanning out from the agent, to determine what ends up in the context, how the loop runs, and what gets saved.

With this wave of new harenesses, we're seeing innovation around each layer. Buzz's channels, Claude Tag, and others are experimenting with multiplayer agent environments. Omnigent's policies manage what *can* happen in a given session, pushing down an organization's requirements. And Meta trained Muse Spark to know it's harness ([much like others](https://www.dbreunig.com/2026/05/10/overfitting-the-harness.html), they just don't write about it…)

The burst of harness innovation, I believe, isn't going to slow because managing these layers is *much stickier* than less-situated agents. It's trivial to jump from Claude Code to Codex when one tires of Opus's writing, but if the entire org and team have already *set up* a system that manages *all of the above*, it's really hard to shift.

People at Cursor and Copilot are nodding right now, welcoming us all, wondering what took so long.

It's going to be funny if the network effects the AI labs have been searching for *end up looking just like the network effects of the SaaS era*. Coding harnesses, managing the environments *around* the agent, look a whole lot like the SaaS platforms of old.

---

*Capture note (2026-08-24 watch run): filed under the loop-engineering topic (scope: anything-substantive). Breunig is not on the config's `people` list — this is a topic-axis hit, surfaced via Simon Willison's 2026-08-23 quotation of Breunig's companion piece. The 8-layer "situated agent" model (Session → Environment → Repo → Memory → Skills → Team → Organization → Model, ordered by how many people use a layer and how often it changes) is a candidate definitional primary for the harness-engineering concept page, alongside Böckeler's guides/sensors framing. Also names a concrete Aug-2026 harness census (Omnigent, DeepSeek Harness, Buzz, QM, Flue, Muse Code, OpenClaw, NanoClaw, Hermes, Conductor, Prime Agent) worth dating. Unreferenced-but-cited companion: "Overfitting the Harness" (2026-05-10), not yet captured.*
