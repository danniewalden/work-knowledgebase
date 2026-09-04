---
title: Graph Engineering
type: concept
created: 2026-07-31
updated: 2026-07-31
sources: [prefect-loops-vs-graphs, addyosmani-software-factories-light-and-dark, nick-tune-graphs-memory-skills-agents]
tags: [graph-engineering, loop-engineering, multi-agent-orchestration, directed-agentic-graphs, orchestration, focus]
---

# Graph Engineering

**The macro-orchestration layer above the loop.** Where [[loop-engineering]] perfects *one agent's
internal, micro behaviour* (set it an objective, let it iterate to a goal), **graph engineering governs
the flow *across* agents** — modelling the whole workflow as an explicit graph of nodes and edges so it
is reproducible, governable, and auditable. The **authored primary** is [[jeremiah-lowin]] of
[[prefect]] ([[prefect-loops-vs-graphs]]), who coined **"directed agentic graph"** and named the
loops(micro)-vs-graphs(macro) distinction; the public spark was **Peter Steinberger's** viral tweet
asking whether we've moved from loops to graphs.

## The progression

Lowin places it as the newest rung of a ladder, each step "a way to take more control of your agents'
behaviour," each recognising that *more structure + keeping the agent longer on a prescribed path =
better outcome*:

**prompt engineering → multi-prompt → [[loop-engineering]] → graph engineering.**

Loop engineering is genuinely powerful (goal-seeking, from ML) but "got boiled down to the dumbest
version of itself" — the [[ralph-loop|Ralph loop]] — and the simple version became representative. The
warning Lowin repeats: graphs risk the same fate unless the agent world connects to the **decades of
orchestration/graph-theory literature** instead of "rediscovering graph theory from scratch" and
inviting "a new round of slop."

## What a directed agentic graph is

- **Node** = a unit of business logic/work, most likely an agent invocation in a harness; its
  **parameterization, skills, tools, access, instructions, and even the model** can all be set *per
  node*.
- **Edge** = the one-way path from a decision an agent makes to the next invocation.
- A deliberate **rebrand of DAG**: the old *directed **acyclic** graph* (the decades-old
  workflow-orchestration standard) becomes the *directed **agentic** graph* — drop "acyclic," keep
  "directed," and let it govern agent behaviour.

**Inside a node the agent has full autonomy (its own loop); crossing an edge returns control to the
orchestrator.** That interplay is the thing to build intuition for. The **degenerate case makes the
point**: a single-node graph *is* loop engineering reinvented, the structure doing nothing. The moment
you split it, each node can carry different tools/models/access, or be purely programmatic. Crucially,
graphs **permit regression to a loop without leaving the paradigm** — collapse to one node when you
don't care to observe anything; expand when you do. Nodes need not be agents: a node can be
**programmatic code, a human-in-the-loop approval, or sleeping/waiting on an external event.**

## Why it matters — control vs autonomy, reproducibility, security

- **Control vs autonomy** is, for Lowin, *the* central design question with agents; a graph gives you
  **boundaries to modulate it** — autonomy inside a node, control at each edge. How many nodes? A design
  question ("art more than science") — put a node boundary "wherever you want to reason about progress,
  intervene, or interject programmatic logic, and nowhere else."
- **Reproducibility + auditability** — a bare loop over an API gives no guarantee it takes the same path
  each run; a graph means "this run looks like the last hundred, so you can compare them." A business
  concern (products, customer-facing), not an individual one.
- **Security — "don't hand your agent a bazooka."** The strongest reason to reach for a graph:
  **scope capabilities per node.** Do the diligence in a node that *cannot* issue the refund; grant the
  refund tool only in a later node, past a programmatic control-return, **locked to one customer, usable
  once.** "Harness orchestration as much as agent orchestration" — a [[agent-governance|governance]]
  mechanism that rhymes with the KB's [[guardian-agents]] / DCB-guard worked models.

## Macro vs micro — the load-bearing line

**LangGraph and Pydantic AI model an *individual agent's internals* (tool choices, low-level
capabilities) as a graph — that's the micro level.** Directed agentic graphs are **macro orchestration
across potentially many agents**, each node a full agentic invocation whose internal agent *could itself*
be built in LangGraph/Pydantic AI. Keep the two levels distinct: graph-engineering-the-concept here is
the macro one.

## Relationship to neighbours

- **[[loop-engineering]]:** graph engineering is strictly *above* it — a single-node graph reduces to a
  loop, and the loop is what runs *inside* each node. The two are complementary rungs of the same "take
  more control" ladder, not rivals.
- **[[multi-agent-orchestration]]:** directed agentic graphs are a concrete, reproducible model *for*
  multi-agent orchestration — the "org chart made of loops" drawn as an explicit control-flow diagram.
- **[[software-factory]]:** [[addyosmani-software-factories-light-and-dark|Osmani's]] "loops vs graphs"
  aside says the same thing from the factory side — "a predefined directed graph is **back-pressure**
  drawn as a diagram" (trade agent freedom for mandatory checks and legible failure points).
- **[[nick-tune-graphs-memory-skills-agents|Nick Tune's Graph+Memory+Skills+Agent]]:** adjacent but a
  *different* graph — Tune models the **system/state graph** agents *reason over* (queryable, to bound a
  change's blast radius); Lowin models the **control-flow graph** agents *run inside*. Both argue an
  explicit graph beats agents making it up as they go.
- **vs. [[event-modeled-agent-design]]:** an open seam — an [[event-modeling|Event Model]]'s slices and
  swimlanes are a candidate authoring surface for such a graph (slice = node's unit of work,
  [[given-when-then|GWT]] = the edge's gate); not yet drawn by any source.

## Provenance / freshness

Coined and argued by [[jeremiah-lowin]] (Prefect PyData London keynote ~June 2026; FastMCP podcast ep. 3,
2026-07-22); Prefect is being rebuilt around it, and the **Dagster acquisition** (a graph-native
asset/lineage product) folds in. Early, vendor-authored, and pre-GA ("early access partners") — canonical
for the *framing*, not yet an independent worked deployment.

_Sources: [[prefect-loops-vs-graphs]] · [[addyosmani-software-factories-light-and-dark]] · [[nick-tune-graphs-memory-skills-agents]]._
