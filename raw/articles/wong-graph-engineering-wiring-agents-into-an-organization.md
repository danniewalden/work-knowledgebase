---
source_url: https://www.awongcm.io/blog/2026/09/01/graph-engineering-wiring-agents-into-an-organization/
title: "Graph Engineering: Wiring Agents Into an Organization"
author: Andy Wong
publication: Power of Eloquence (awongcm.io)
published: 2026-09-01
retrieved: 2026-09-02
type: article
---

# Graph Engineering: Wiring Agents Into an Organization

Tue Sep 01 2026 8:30 AM

> **TL;DR**: *Loop engineering taught one agent how to keep going without you in the room. Graph engineering is what happens once there's more than one agent — and someone has to decide who talks to whom, in what order, and who's allowed to see what.*

*[Image: AI-generated header illustration — "Generated AI image by Google Gemini Nano Banana"]*

## Introduction

In my last [article](https://www.awongcm.io/blog/2026/08/23/loop-engineering-teaching-ai-agents-how-to-think/), I wrote about loop engineering — the outer cycle that lets an agent run to completion without you steering it turn by turn. Wrap a task in a trigger, a verifiable goal, a real verifier, and stop rules, and you have something that can run unattended for hours instead of minutes.

That post assumed one agent. One loop, one harness underneath it, one job.

But if I were to actually ship the same loop into production, the next probable problem that would show up almost immediately is: the loop that fixes bugs isn't the loop that should review the fix, and the loop that reviews the fix definitely isn't the loop that should decide whether to deploy it. One instruction from a person was quietly spawning half a dozen agents, each with a different job, and nothing in "loop engineering" told me how those agents should be connected to each other.

That's the layer this post is about: **graph engineering** — designing the topology that connects multiple agents into something closer to an organization than a single worker.

---

## What Is Graph Engineering?

Graph engineering is the discipline of designing the structure that multiple agents run inside: which specialized nodes exist, which edges are allowed to route work between them, and what shared state travels along those edges as the graph executes.

The term itself has a messier origin story than "loop engineering" did, and it's worth being upfront about that rather than pretending it arrived fully formed. The earliest serious use I could find is a July 4, 2026 post by Josh Simmons, "We Are Entering the Graph Engineering Phase," which named the shift before almost anyone else was talking about it. It stayed a niche observation for two weeks. Then, on July 18, Peter Steinberger — one of the same voices who helped popularize loop engineering — tweeted something close to "are we still talking loops or did we shift to graphs yet?" and it took off, racking up millions of views within days.

I want to flag something most of the recap posts skip: by several accounts, that tweet was at least partly a joke — a dig at an industry that mints a new "X engineering" term every few weeks, not a considered technical claim. Hamel Husain's reply to the whole thing was, reportedly, a single "Stop it" GIF. That's worth remembering before you put "graph engineering" on a slide with a straight face.

Here's the thing, though: the joke pointed at something real. Two things happened after it that turned "graph engineering" from a tweet into an actual discipline.

First, LangChain — who arguably has the strongest claim to prior art here, given LangGraph has existed since 2023 — published a response on July 22 arguing the term isn't new, it's just the latest label for what LangGraph has done from the start: build the explicit graph structures that route work between agents, tools, and humans. Their point is fair. It's also the same thing people said about loop engineering when it showed up ("isn't this just a while-loop with extra steps?"), and it didn't stop that term from becoming useful shorthand.

Second, an arXiv survey — "Graph Engineering in the Era of LLM Agents: From Individual Intelligence to System Intelligence," submitted August 21 and revised August 26 — gave the term an actual definition with some rigor behind it. Their framing is the cleanest I've seen: prompt, context, harness, and loop engineering all optimize *individual* agent behavior. Graph engineering is the first layer that optimizes the *system* — explicit, dynamic structures representing tasks, agents, and state, evolving as the graph runs.

So: born as a half-joke on July 4, viral as a real joke on July 18, contested as marketing on July 22, formalized as a research topic by August 26. Less than two months, start to finish. I'm writing about it anyway, because underneath the naming churn is a genuine engineering problem I ran into myself the week after my loop engineering post went out.

---

## Where This Sits Next to Loop Engineering

Extending the ladder from the last few posts:

- **Context engineering** answers: *what do I put in front of the model right now?*
- **Harness engineering** answers: *how does the model act on that — which tools, how is one step validated and executed?*
- **Loop engineering** answers: *what happens after that step — do we go again, and for how long?*
- **Graph engineering** answers: *which agent does this next, what are they allowed to see, and who do they hand off to?*

A loop governs one agent's campaign toward one goal. A graph governs the org chart those campaigns live inside. You can have four excellent loops — each with a tight verifier and sane stop rules — wired together so badly that the fix-it loop and the review-it loop are the same underlying agent talking to itself, which is exactly the "model grading its own homework" failure I warned about last time, just moved up a level.

---

## The Three Things Every Graph Needs

Strip away the framework-specific vocabulary (nodes, edges, state — LangGraph's terms, but the shape is universal) and every working multi-agent graph decomposes into three parts.

### 1. Nodes — the specialized workers

Not every node has to be an LLM call. A node can be an agent (with its own loop, its own harness), a deterministic function (a linter, a test runner, a formatter), a router that decides where to send work next, or a human checkpoint. Treating "call a person for approval" as just another node type, rather than a special case bolted on afterward, is what makes a graph actually safe to run unattended for the parts that should run unattended.

### 2. Edges — who's allowed to talk to whom

An edge is a permitted transition, not a suggestion. If your bug-fixing agent can silently hand its own output straight to a "mark as resolved" node with no review edge in between, you don't have a review process — you have a rubber stamp with extra latency. Edges are where you encode the org chart: who reports to whom, what needs a second opinion, what's allowed to happen without one.

### 3. Shared state — what travels along the graph

This is the part that's easy to get wrong in a way that doesn't show up until week three. If every node keeps its own private context and only passes along a one-line summary, the graph slowly develops the multi-agent version of a game of telephone — the reviewer agent approving something the writer agent never actually did, because the summary it received didn't say what really happened. Shared state needs to be explicit about what's authoritative (the actual diff, the actual test output) versus what's a convenience summary for a node that doesn't need the full detail.

```
from dataclasses import dataclass, field
from enum import Enum
from typing import Callable

class NodeType(Enum):
    AGENT = "agent"          # LLM-backed, has its own loop
    FUNCTION = "function"    # deterministic — linter, test runner, formatter
    ROUTER = "router"        # decides which edge to take next
    HUMAN = "human"          # a checkpoint that pauses for a person

@dataclass
class GraphNode:
    name: str
    node_type: NodeType
    handler: Callable         # what actually runs
    allowed_next: list[str]   # the edges — who this node is permitted to hand off to

@dataclass
class GraphState:
    task_id: str
    authoritative: dict = field(default_factory=dict)  # the real artifacts: diffs, test results
    summaries: dict = field(default_factory=dict)       # convenience context for nodes that don't need it all
    history: list[str] = field(default_factory=list)    # which nodes have run, in order

class AgentGraph:
    def __init__(self, nodes: dict[str, GraphNode], entry: str):
        self.nodes = nodes
        self.entry = entry

    def run(self, state: GraphState) -> GraphState:
        current = self.entry
        while current is not None:
            node = self.nodes[current]
            state = node.handler(state)          # each handler owns its own loop internally
            state.history.append(current)

            next_node = self._route(node, state)
            if next_node and next_node not in node.allowed_next:
                # the edge doesn't exist — fail loud, don't silently reroute
                raise ValueError(f"{current} tried to hand off to {next_node}, but that edge isn't defined")
            current = next_node
        return state

    def _route(self, node: GraphNode, state: GraphState) -> str | None:
        # a router node decides dynamically; other nodes usually have one fixed next step
        if node.node_type == NodeType.ROUTER:
            return node.handler.decide(state)
        return node.allowed_next[0] if node.allowed_next else None
```

Notice what this doesn't do: it doesn't decide *how* the fix-it agent fixes the bug, or when it's allowed to stop retrying. That's still loop engineering's job, running inside the `AGENT` node's handler. The graph only decides where the output of that loop is allowed to go next. Same relationship as last post's harness-inside-loop diagram, one level up.

---

## Where Graph Engineering Goes Wrong

| Symptom                                                | Usually caused by                                                                                                        |
| ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| The reviewer always approves                           | The "review" node is the same agent that wrote the code, just called again — no independent edge, no independent context |
| Work silently vanishes                                 | A node fails and there's no edge defined for the failure case, so the graph just stops with no record of why             |
| Everyone re-derives the same context                   | Shared state has no authoritative source, so every node reconstructs its own version from scratch, and they drift apart  |
| A human checkpoint gets skipped under load             | The human node is treated as optional latency to route around instead of a real edge in the graph                        |
| The graph works in the demo, falls apart in production | It was designed top-down as an org chart before a single node's loop was proven reliable on its own                      |

That last row is the one I'd flag hardest, because it's the same lesson from the loop engineering post, just recurring one layer up: don't reach for a five-node graph with routers and sub-routers before you've proven that two nodes handing off to each other actually works. A graph amplifies whatever's inside its nodes — a node with a weak loop doesn't get more reliable by being connected to three other nodes, it just gets more expensive to route around when it fails.

---

## They Nest, They Don't Compete

A loop without a graph is a single agent that can run itself to completion, alone — useful, but everything has to go through that one agent, including work it isn't actually well-suited for. A graph without solid loops inside its nodes is just an org chart connecting agents that individually don't know when to stop — you've structured the chaos without reducing it.

The boundary is the same shape as the loop-and-harness boundary from last time: a loop's stop rules govern one agent's campaign; a graph's edges govern which campaign runs next and who's allowed to see the result. Neither replaces context or harness engineering underneath it — a node with bad context or a leaky harness is still a bad node, no matter how well-designed the graph around it is.

---

## What to Build Next

If you've got more than one agent in production, or you're about to:

**Short term (this sprint):**

- [ ] Draw your current setup as an actual graph — nodes and edges — even if it's informal today; you'll usually find an edge you didn't know existed
- [ ] Check whether any "review" node is secretly the same agent as the node it's reviewing
- [ ] Decide what's authoritative state versus convenience summary, and stop letting nodes silently drift on the latter

**Medium term (next month):**

- [ ] Make failure an explicit edge, not an undefined case that just halts the graph
- [ ] Turn human approval steps into real graph nodes with defined edges in and out, not a side-channel Slack message
- [ ] Log the path each run actually took through the graph, not just the final output — you'll need it the first time someone asks "why did it do that"

**Longer term:**

- [ ] Build reusable node types for your team's recurring roles (a review node, a deploy-gate node) the way you'd build a shared loop library
- [ ] Track which edges get used versus which ones exist for a case that's never happened, and prune accordingly
- [ ] Revisit this in a few months — "graph engineering" may not be the name that sticks, but the underlying problem of governing multi-agent topology isn't going away

---

## Closing Thought

Loop engineering was about deciding, without you in the room, whether one agent's next step actually moved the task forward. Graph engineering is about deciding, without you in the room, which agent gets the next step at all — and who's allowed to check its work.

I'll be honest about where this term stands: it hasn't "won" the way loop engineering did. It was arguably half a joke to start with, and serious people I respect think it's mostly a new label on ideas LangGraph has shipped for three years. I think both things can be true at once — the name is contested, and the problem it's pointing at is real. The engineering teams that build genuinely trustworthy multi-agent systems won't be the ones with the cleverest single loop. They'll be the ones who can draw their agents' org chart on a whiteboard and explain, edge by edge, why each connection exists.

Till next time, Happy Coding!

---

## References

1. Josh Simmons, "We Are Entering the Graph Engineering Phase," July 4, 2026.
2. Peter Steinberger, viral post on the shift from loops to graphs, July 18, 2026 (widely reported as at least partly satirical).
3. LangChain (Harrison Chase, Sydney Runkle), ["3 Years of Graph Engineering with LangGraph,"](https://www.langchain.com/blog/3-years-of-graph-engineering-with-langgraph) July 22, 2026.
4. "Graph Engineering in the Era of LLM Agents: From Individual Intelligence to System Intelligence," [arXiv:2608.21156](https://arxiv.org/abs/2608.21156), submitted August 21, 2026, revised August 26, 2026.
5. Boris Cherny, "Steps of AI Adoption," July 17, 2026.

Posted by Andy Wong Tue Sep 01 2026 — tags: ai-engineering, large-language-models, loop-engineering, harness-engineering, ai-agents, agentic-ai, claude, developer-tools, graph-engineering, multi-agent-systems
