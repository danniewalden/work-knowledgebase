---
title: "Prefect — Loops vs. graphs (directed agentic graphs)"
type: source
created: 2026-07-31
updated: 2026-07-31
sources: [prefect-loops-vs-graphs]
raw_file: [raw/articles/prefect-loops-vs-graphs.md]
tags: [graph-engineering, loop-engineering, multi-agent-orchestration, agentic-ai, directed-agentic-graphs, orchestration, focus]
---

# Prefect — Loops vs. graphs

Edited transcript of **FastMCP podcast episode 3** — Radhika Gulati (Product Marketing) with
**[[jeremiah-lowin]]** (CEO, [[prefect]]) — published 2026-07-22. The **authored primary** for the
**loops-vs-graphs** framing and the coinage **"directed agentic graph."** Source file:
`raw/articles/prefect-loops-vs-graphs.md`. Companion concept: [[graph-engineering]].

## The framing

**Loops are one agent's internal, micro behaviour; directed agentic graphs are macro orchestration
across (potentially many) agents.** Graph engineering is the newest entry in a progression Lowin lays
out: **prompt engineering → multi-prompt → [[loop-engineering]] → graph engineering** — each a way to
"take more control of your agents' behaviour," each recognising that *the more structure you give a
workflow and the longer you keep an agent on a prescribed path, the better the outcome.* Loop
engineering is genuinely powerful (goal-seeking, from ML), but it "got boiled down to the dumbest
version of itself that can be broadly understood" — the [[ralph-loop|Ralph loop]] — and the simple
version became the representative one. The spark for the public frenzy was **Peter Steinberger's**
near-throwaway tweet asking whether we're still on loops or have moved to graphs; Lowin had already
given a **PyData London keynote** on directed agentic graphs ~6 weeks earlier, and it's been a Prefect
product imperative since April.

## What a directed agentic graph actually is

Nodes and edges, made concrete: a **node is a unit of business logic/work, most likely carried out by
an agent**; an **edge is the path from a decision that agent makes to the next invocation.** It's
**directed** (edges go one way — no reversing). Lowin **rebrands DAG**: the old *directed acyclic
graph* (the decades-old workflow-orchestration standard) becomes the *directed **agentic** graph* — he
drops the acyclic constraint, keeps "directed," and makes each node "the invocation of an agent in a
harness" where **parameterization, skills, tools, access, instructions, even the model itself can be
set at the node level.**

The degenerate case is the whole point: a **single-node graph = [[loop-engineering]] reinvented**, the
structure doing nothing. Split it into two nodes and you can give each different tools, use an expensive
model for the hard step and a cheap one for the next, or make a node purely programmatic. **Inside a
node the agent has full autonomy (its loop); crossing an edge returns control to you.** So graphs
**permit regression to a loop without leaving the paradigm** — collapse to one node if you don't care to
observe anything, expand when you do.

## Why businesses care (and individuals don't)

For an individual firing up Claude/ChatGPT, whether it loops or uses a graph invisibly doesn't matter.
Inside a **business / product / customer-facing** setting you inherit **reproducibility, auditability,
and the ability to understand what happened** — none of which a bare loop over an API gives you (you
can't know it takes the same path each time; you can only inspect side effects after the fact). Graphs
give **boundaries to modulate control vs autonomy** — Lowin's stated *central design question* for
agents — and **reproducibility** ("this run looks like the last hundred, so you can compare them"),
a goal he says is missing from most AI engineering today.

## The security argument — "don't hand your agent a bazooka"

The strongest reason to reach for a graph. State-of-the-art today: write a skill listing the ten checks
before issuing a refund, then hand the agent a refund tool and hope. That's **handing the agent the
capability plus a polite note** — and agents "don't even always read their skills." Split into a graph:
node 1 does the (non-programmatic, genuinely-needs-an-agent) diligence and **cannot issue refunds**;
only past a **programmatic control-return** does node 2 get the refund tool — **scoped to one customer,
usable once**, in a fresh harness. "You could call this **harness orchestration** as much as agent
orchestration," and it's why Lowin thinks people will actually adopt graphs: the number-one benefit is
**changing an agent's capabilities depending on the path it took.** (Prior-episode image: asking an
agent to make a sandwich and handing it a bazooka in case of zombies.)

## Humans and non-agents as nodes

A **human-in-the-loop approval is just a node**: agent produces an outcome → approval node where a
person decides → next agentic node runs conditional on the decision. More generally a node can be an
agent, **programmatic code, a human approval, or sleeping/waiting on an external event** — all valid
graph citizens. Stepped back: "nodes represent outcomes, edges represent what happens next once a
decision comes out of that outcome."

## The macro/micro line — vs LangGraph and Pydantic AI

Explicit and load-bearing for the KB: **LangGraph / Pydantic AI model an *individual agent's internals*
(its tool choices, low-level capabilities) as a graph** — that's the **micro** level and it's fine.
**Directed agentic graphs are *macro* orchestration across many agents, each node a full agentic
invocation** — the agent *inside* a node could itself be built in LangGraph or Pydantic AI. Prefect
models the workflow *around* those agents so it's reproducible, governable, auditable.

## Positioning + Prefect / Dagster

Lowin is deliberately the "calm down, here's the boring way that works" voice — graph theory and
orchestration have decades of literature, and skipping that connection means "making every mistake the
orchestration world already made" and inviting "a new round of slop" the way the Ralph loop did. He
frames it as "**95% things we've been doing for decades, 5% new magic sparkles because it's AI**."
Prefect is being updated with the directed agentic graph as the front-and-center representation of agent
behaviour; the **Dagster acquisition** fits because Dagster's product is fundamentally graph-based
(asset graphs + lineage), joining Prefect's durable runtime for executing the agent loop.

## Why it matters here

- The **authored primary** behind [[graph-engineering]] and the source of the loops(micro) vs
  graphs(macro) distinction the KB now files there.
- A **macro-orchestration counterpart** to [[loop-engineering]]: loop engineering perfects one agent's
  inner behaviour; directed agentic graphs govern the flow *across* agents — squarely a
  [[multi-agent-orchestration]] and [[software-factory]] concern ("an org chart made of loops" gets an
  explicit control-flow diagram).
- Adjacent to [[nick-tune-graphs-memory-skills-agents|Nick Tune's Graph+Memory+Skills+Agent substrate]] —
  both argue an explicit, queryable/traversable graph beats agents making it up as they go; and to
  [[addyosmani-software-factories-light-and-dark|Osmani's "loops vs graphs"]] aside ("a predefined
  directed graph is back-pressure drawn as a diagram").
- Node-level capability scoping is a control-vs-autonomy and [[agent-governance|governance]] mechanism;
  the refund example rhymes with the KB's [[guardian-agents]] / DCB-guard worked models.

## Links

Entities: [[jeremiah-lowin]], [[prefect]], [[nick-tune]]. Concepts: [[graph-engineering]],
[[loop-engineering]], [[multi-agent-orchestration]], [[ralph-loop]], [[software-factory]],
[[agent-governance]], [[model-context-protocol]].
Related sources: [[addyosmani-software-factories-light-and-dark]], [[nick-tune-graphs-memory-skills-agents]],
[[swyx-loopcraft-art-of-stacking-loops]], [[anthropic-getting-started-with-loops]].

_Raw source: `raw/articles/prefect-loops-vs-graphs.md`._
