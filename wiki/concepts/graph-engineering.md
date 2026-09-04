---
title: Graph Engineering
type: concept
created: 2026-07-31
updated: 2026-09-04
sources: [prefect-loops-vs-graphs, addyosmani-software-factories-light-and-dark, nick-tune-graphs-memory-skills-agents, wong-graph-engineering-wiring-agents-into-an-organization, macmanus-schott-react-for-agents-flue-meta-harness, edwards-alexander-an-accidental-blackboard, graph-engineering-era-of-llm-agents-system-intelligence, guo-survey-question-answering-to-task-completion-harness-design, mcateer-evolution-of-the-agent-harness]
tags: [graph-engineering, loop-engineering, multi-agent-orchestration, directed-agentic-graphs, orchestration, focus]
---

# Graph Engineering

**The macro-orchestration layer above the loop.** Where [[loop-engineering]] perfects *one agent's
internal, micro behaviour* (set it an objective, let it iterate to a goal), **graph engineering governs
the flow *across* agents** — modelling the whole workflow as an explicit graph of nodes and edges so it
is reproducible, governable, and auditable. The **authored primary** is [[jeremiah-lowin]] of
[[prefect]] ([[prefect-loops-vs-graphs]]), who coined **"directed agentic graph"** and named the
loops(micro)-vs-graphs(macro) distinction; the public spark was **Peter Steinberger's** viral tweet
asking whether we've moved from loops to graphs — **which was, by several accounts, at least partly a
joke, and was not the term's first serious use. This page previously credited it flatly as the spark; see
*Provenance / freshness — and the joke at the origin* below before repeating that.**

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
  mechanism that rhymes with the KB's [[guardian-agents]] / DCB-guard worked models. The same principle
  reached from inside a single agent: [[macmanus-schott-react-for-agents-flue-meta-harness|Schott's]] Flue
  hooks attach a capability at runtime *"after first verifying a user"* — **capability follows lifecycle
  stage, not identity**, whether that stage is a graph node or a hook.

## Macro vs micro — the load-bearing line

**LangGraph and Pydantic AI model an *individual agent's internals* (tool choices, low-level
capabilities) as a graph — that's the micro level.** Directed agentic graphs are **macro orchestration
across potentially many agents**, each node a full agentic invocation whose internal agent *could itself*
be built in LangGraph/Pydantic AI. Keep the two levels distinct: graph-engineering-the-concept here is
the macro one.

## Nodes, edges, shared state — and how graphs fail ([[wong-graph-engineering-wiring-agents-into-an-organization|Wong, 2026-09-01]])

A second, non-Prefect decomposition, framework-agnostic: *"which specialized nodes exist, which edges are
allowed to route work between them, and what shared state travels along those edges."*

- **Nodes need not be LLM calls** — an agent (with its own loop and harness), a **deterministic function**
  (linter, test runner, formatter), a **router**, or a **human checkpoint**. *"Treating 'call a person for
  approval' as just another node type, rather than a special case bolted on afterward, is what makes a
  graph actually safe to run unattended for the parts that should run unattended."* (Agrees with
  [[prefect-loops-vs-graphs|Lowin]].)
- **An edge is a permitted transition, not a suggestion.** *"If your bug-fixing agent can silently hand
  its own output straight to a 'mark as resolved' node with no review edge in between, you don't have a
  review process — **you have a rubber stamp with extra latency**. Edges are where you encode the org
  chart."* His reference implementation **fails loud** on an undeclared handoff rather than silently
  rerouting.
- **Shared state: authoritative vs convenience — the dimension Lowin's account lacks.** The week-three
  failure: every node keeps private context and passes a one-line summary, producing *"the multi-agent
  version of a game of telephone — **the reviewer agent approving something the writer agent never
  actually did**, because the summary it received didn't say what really happened."* Be explicit about
  what is **authoritative** (the actual diff, the actual test output) versus what is a convenience
  summary. Note that [[edwards-alexander-an-accidental-blackboard|the accidental blackboard]] solved
  exactly this by accident — make the repo itself the authoritative shared space and there is nothing to
  drift from. The four substrates side by side are on [[agent-coordination-substrates]].

**The failure table, worth carrying whole:** the reviewer always approves → *"the 'review' node is the
same agent that wrote the code, just called again"* (**"the model grading its own homework failure, just
moved up a level"**); work silently vanishes → **no edge defined for the failure case**; everyone
re-derives context → no authoritative source, nodes drift; a human checkpoint gets skipped under load →
*"the human node is treated as optional latency to route around instead of a real edge"*; **works in the
demo, falls apart in production → "it was designed top-down as an org chart before a single node's loop
was proven reliable on its own."**

That last row generalises the same warning one layer up from [[loop-engineering]]: *"**a graph amplifies
whatever's inside its nodes** — a node with a weak loop doesn't get more reliable by being connected to
three other nodes, it just gets more expensive to route around when it fails."* His three practices:
**make failure an explicit edge**, make human approval a **real node with defined edges in and out** ("not
a side-channel Slack message"), and **log the path each run actually took through the graph, not just the
final output — "you'll need it the first time someone asks 'why did it do that'"** (an
[[agent-legibility]]/[[decision-trace]] requirement, not a performance one).

*(No measurement, no deployment — and the author states the framing is **prospective**: the motivating
problem is *"if I were to actually ship the same loop into production, the next probable problem that
would show up almost immediately is…"* So the failure table is reasoned from a hypothetical, not
harvested from incidents.)*

## Independent academic support — and a rival ladder (Feng et al. 2026)

This page's primary is a vendor one ([[prefect-loops-vs-graphs|Lowin/Prefect]], who sell orchestration).
[[graph-engineering-era-of-llm-agents-system-intelligence|Feng et al. (arXiv:2608.21156, 35 authors)]] reach
the same boundary independently — an **arXiv preprint survey, not peer-reviewed**, and a *position* rather
than a measurement, so it corroborates the argument and no result. Their version: individual intelligence hits
"a fundamental limit: many tasks require heterogeneous expertise, interdependent subtasks, parallel execution,
**independent verification**, and **persistent state**, exceeding any single agent's organizational capacity.
**Augmenting one agent's capabilities or context cannot resolve this architectural mismatch**; intelligence
must instead be distributed across specialized agents and organized at the system level." They name that
property **System Intelligence**, and Graph Engineering as its substrate: "explicit, dynamic, evolving graph
structures representing tasks, agents, and system states." Note the two named drivers of the mismatch are this
KB's own rules — *maker≠checker* (independent verification) and state outliving a context window
([[long-running-agents]]).

They also state the paradigm ladder outright: "**Prompt Engineering** to elicit model capabilities, **Context
Engineering** to manage information access, **Harness Engineering** to organize external tools and resources,
and **Loop Engineering** to support continual reflection and self-improvement" — this KB's sequence, from a
source unconnected to the practitioners who coined it, with graph engineering proposed as the fifth rung.
**But the ladder is contested:** [[guo-survey-question-answering-to-task-completion-harness-design|Guo et al.
(arXiv:2606.20683)]], two months earlier, agree on the first three rungs and make the fourth **"agent-native
training and co-evolution"**, with no loop or graph rung at all. Two independent surveys agree on
prompt → context → harness and diverge on what follows: one goes *up* into orchestration structure, one
*inward* into the model. They may not be rivals — coordination and internalisation can both be true — but the
wiki records both proposals and merges neither. Also worth holding against
[[mcateer-evolution-of-the-agent-harness|McAteer]], who expects **multi-agent orchestration to be absorbed
into model weights** next ([[harness-absorption]]): two 2026-08 claims about the same near future pointing
opposite ways.

**One capture note, since two ingest batches disagreed about it:** the graph-engineering survey reached the KB
first only as a summary inside Wong's piece (with the paper itself not in `raw/`); it has since been captured
directly as [[graph-engineering-era-of-llm-agents-system-intelligence]]. Cite the primary, not the summary.

## Relationship to neighbours

- **[[loop-engineering]]:** graph engineering is strictly *above* it — a single-node graph reduces to a
  loop, and the loop is what runs *inside* each node. The two are complementary rungs of the same "take
  more control" ladder, not rivals. (Note that the *loop* page's own layering — loop above harness — is
  itself disputed, and that the two surveys above disagree about whether loop or graph is the higher
  rung.)
- **[[multi-agent-orchestration]]:** directed agentic graphs are a concrete, reproducible model *for*
  multi-agent orchestration — the "org chart made of loops" drawn as an explicit control-flow diagram.
  For graphs as one of four coordination substrates, see [[agent-coordination-substrates]].
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

## Provenance / freshness — and the joke at the origin

Coined and argued as *directed agentic graph* by [[jeremiah-lowin]] ([[prefect]] PyData London keynote
~June 2026; FastMCP podcast ep. 3, 2026-07-22); Prefect is being rebuilt around it, and the **Dagster
acquisition** (a graph-native asset/lineage product) folds in. **Early, vendor-authored and pre-GA**
("early access partners") — canonical for the *framing*, not yet an independent worked deployment.

**The term's public history is messier than this page previously implied**, and
[[wong-graph-engineering-wiring-agents-into-an-organization|Andy Wong]] lays it out against his own
interest (he is writing about the term anyway): *"Born as a half-joke on July 4, viral as a real joke on
July 18, contested as marketing on July 22, formalized as a research topic by August 26. **Less than two
months, start to finish.**"* Specifically:

- **2026-07-04** — Josh Simmons, *"We Are Entering the Graph Engineering Phase"*: the earliest serious
  use Wong could find. Stayed niche for two weeks.
- **2026-07-18** — **Peter Steinberger's** post ("are we still talking loops or did we shift to graphs
  yet?") goes viral at millions of views. *"By several accounts, that tweet was at least partly a joke —
  **a dig at an industry that mints a new 'X engineering' term every few weeks**, not a considered
  technical claim."* **Hamel Husain's reply was reportedly a single "Stop it" GIF.** *"That's worth
  remembering before you put 'graph engineering' on a slide with a straight face."*
- **2026-07-22** — **LangChain** (Harrison Chase, Sydney Runkle), *"3 Years of Graph Engineering with
  LangGraph"*: the term isn't new, it's the latest label for what LangGraph has done since 2023. Wong:
  *"Their point is fair."* **NOT INDEPENDENT** — LangChain has a product in the category, so their
  prior-art rebuttal is not external corroboration for anything about LangGraph.
- **2026-08-21, revised 08-26** — *"Graph Engineering in the Era of LLM Agents: From Individual
  Intelligence to System Intelligence,"* **arXiv:2608.21156** — **PREPRINT, not peer-reviewed**. Reached
  the KB first only through Wong's summary; the primary is now captured as
  [[graph-engineering-era-of-llm-agents-system-intelligence]]. Its framing is the first in the KB
  that is neither Prefect's nor LangChain's: **prompt, context, harness and loop engineering all optimize
  *individual* agent behaviour; graph engineering is the first layer that optimizes the *system*** —
  explicit, dynamic structures representing tasks, agents and state, evolving as the graph runs.

Wong's own verdict, worth quoting on this page: *"it hasn't 'won' the way loop engineering did. It was
arguably half a joke to start with, and serious people I respect think it's mostly a new label on ideas
LangGraph has shipped for three years. I think both things can be true at once — **the name is contested,
and the problem it's pointing at is real.**"* And his standing caveat: *"'graph engineering' may not be
the name that sticks, but the underlying problem of governing multi-agent topology isn't going away."*

_Sources: [[prefect-loops-vs-graphs]] · [[addyosmani-software-factories-light-and-dark]] · [[nick-tune-graphs-memory-skills-agents]] · [[wong-graph-engineering-wiring-agents-into-an-organization]] · [[graph-engineering-era-of-llm-agents-system-intelligence]] · [[guo-survey-question-answering-to-task-completion-harness-design]] · [[mcateer-evolution-of-the-agent-harness]] · [[macmanus-schott-react-for-agents-flue-meta-harness]] · [[edwards-alexander-an-accidental-blackboard]]._
