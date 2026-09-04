---
title: "Source: Wong — Graph Engineering: Wiring Agents Into an Organization"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [wong-graph-engineering-wiring-agents-into-an-organization]
raw_file: [raw/articles/wong-graph-engineering-wiring-agents-into-an-organization.md]
tags: [graph-engineering, loop-engineering, multi-agent-orchestration, provenance, agentwashing, focus]
---

# Source: Wong — Graph Engineering: Wiring Agents Into an Organization

Source: **Andy Wong**, *"Graph Engineering: Wiring Agents Into an Organization"*, Power of Eloquence
(awongcm.io), **2026-09-01**. Raw capture:
`raw/articles/wong-graph-engineering-wiring-agents-into-an-organization.md`. Sequel to
[[wong-loop-engineering-teaching-ai-agents-how-to-think]] and the fourth rung of the same ladder.

## Summary

Two things here matter to the KB. First, a **decomposition of a multi-agent graph into nodes, edges and
shared state** with a failure table — the practical content. Second, and more valuable, an **honest
provenance history of the term "graph engineering"** which materially corrects the KB's existing
[[graph-engineering]] page: the viral tweet the KB credits as "the public spark" was, **by several
accounts, at least partly a joke** — a dig at an industry that mints a new "X engineering" term every
few weeks. Wong publishes this against his own interest, since he is writing the post anyway.

## Key points

- **The four-rung ladder, extended.** [[context-engineering]] = what goes in front of the model;
  [[harness-engineering]] = how it acts, one step; [[loop-engineering]] = do we go again, and for how
  long; **graph engineering = which agent does this next, what are they allowed to see, and who do they
  hand off to.** "A loop governs one agent's campaign toward one goal. A graph governs the org chart
  those campaigns live inside."
- **The provenance timeline, dated.** *"Born as a half-joke on July 4, viral as a real joke on July 18,
  contested as marketing on July 22, formalized as a research topic by August 26. Less than two months,
  start to finish."* Specifically: **Josh Simmons, "We Are Entering the Graph Engineering Phase"
  (2026-07-04)** is the earliest serious use Wong could find; **Peter Steinberger's 2026-07-18 post**
  ("are we still talking loops or did we shift to graphs yet?") took it viral at millions of views and
  **was at least partly satirical**; **Hamel Husain's reply was reportedly a single "Stop it" GIF**;
  LangChain (Harrison Chase, Sydney Runkle) published **"3 Years of Graph Engineering with LangGraph"
  (2026-07-22)** arguing the term is just a new label for what LangGraph has done since 2023 —
  *"Their point is fair."*
- **The one piece of formal grounding is a preprint.** *"Graph Engineering in the Era of LLM Agents:
  From Individual Intelligence to System Intelligence,"* **arXiv:2608.21156**, submitted 2026-08-21,
  revised 2026-08-26 — **PREPRINT, not peer-reviewed**, and captured here only through Wong's summary
  of it (the paper itself is not in `raw/`). Its framing, which Wong calls the cleanest he has seen:
  **prompt, context, harness and loop engineering all optimize *individual* agent behaviour; graph
  engineering is the first layer that optimizes the *system*** — explicit, dynamic structures
  representing tasks, agents and state, evolving as the graph runs.
- **Nodes — not every node is an LLM call.** A node can be an agent (with its own loop and harness), a
  **deterministic function** (linter, test runner, formatter), a **router**, or a **human checkpoint**.
  "Treating 'call a person for approval' as just another node type, rather than a special case bolted on
  afterward, is what makes a graph actually safe to run unattended for the parts that should run
  unattended."
- **Edges — "a permitted transition, not a suggestion."** "If your bug-fixing agent can silently hand
  its own output straight to a 'mark as resolved' node with no review edge in between, you don't have a
  review process — you have a rubber stamp with extra latency. **Edges are where you encode the org
  chart.**" His sample implementation **fails loud** on an undeclared handoff rather than silently
  rerouting.
- **Shared state — authoritative vs convenience.** The week-three failure: every node keeps private
  context and passes a one-line summary, producing "the multi-agent version of a game of telephone — the
  reviewer agent approving something the writer agent never actually did, because the summary it
  received didn't say what really happened." Fix: be **explicit about what is authoritative** (the actual
  diff, the actual test output) versus what is a convenience summary.
- **The failure table.** Reviewer always approves → the review node is the same agent, just called again
  (**"the model grading its own homework failure, just moved up a level"**). Work silently vanishes →
  no edge defined for the failure case. Everyone re-derives context → no authoritative source, nodes
  drift. Human checkpoint skipped under load → "the human node is treated as optional latency to route
  around instead of a real edge." **Works in the demo, falls apart in production → "it was designed
  top-down as an org chart before a single node's loop was proven reliable on its own."**
- **Make failure an explicit edge**, turn human approval into real nodes with defined edges in and out
  ("not a side-channel Slack message"), and **log the path each run actually took through the graph, not
  just the final output — "you'll need it the first time someone asks 'why did it do that.'"** That last
  is a legibility/audit requirement, not a performance one.
- **He does not claim the term won.** *"I'll be honest about where this term stands: it hasn't 'won' the
  way loop engineering did. It was arguably half a joke to start with, and serious people I respect
  think it's mostly a new label on ideas LangGraph has shipped for three years."* His own longer-term
  checklist item: *"'graph engineering' may not be the name that sticks, but the underlying problem of
  governing multi-agent topology isn't going away."*
- **Limits.** No measurement, no deployment, and — unusually — the author states the work is
  **prospective**: the motivating problem is framed as *"if I were to actually ship the same loop into
  production, the next probable problem that would show up almost immediately is…"* So the failure table
  is reasoned from a hypothetical, not harvested from incidents. The arXiv survey is a **preprint** and
  is second-hand here. The Steinberger-was-joking and Husain-GIF claims are hedged by the author himself
  ("by several accounts," "reportedly") and should be carried with those hedges.

## Connections / contrast

**This source corrects the KB's [[graph-engineering]] page on provenance.** That page had credited the
spark flatly to *"Peter Steinberger's viral tweet asking whether we've moved from loops to graphs"*, as
though a considered technical claim. Wong reports it as at least partly satire, adds the earlier Simmons
post (2026-07-04) as the first serious use, and adds LangChain's prior-art rebuttal. All three belong on
that page; see the deltas file.

**It also supplies the missing non-vendor definition.** The [[graph-engineering]] page's own freshness
note concedes it is "early, vendor-authored, and pre-GA" — built on [[jeremiah-lowin]]/[[prefect]], who
are rebuilding a product around the term. The arXiv survey's individual-vs-system cut (**prompt /
context / harness / loop optimize the agent; graph optimizes the system**) is the first framing in the
KB that is neither Prefect's nor LangChain's — though it is a **preprint**, and LangChain's
prior-art claim means their rebuttal is **NOT INDEPENDENT** corroboration for anything about LangGraph.

**Where Wong and [[prefect-loops-vs-graphs|Lowin]] agree, the KB can lean harder.** Both make the node
the unit at which capability is scoped (Lowin: "don't hand your agent a bazooka" — grant the refund tool
only in a later node; Wong: edges as permitted transitions, human checkpoints as first-class nodes).
Both say a graph is worth it for **auditability**, and both warn against premature graph-building
(Lowin: the degenerate single-node graph does nothing; Wong: don't build five nodes before two work).
Wong adds the *shared-state* dimension Lowin's account lacks — authoritative artifact vs convenience
summary — which is directly the failure mode [[edwards-alexander-an-accidental-blackboard|the accidental
blackboard]] solved by accident, by making the *repo* the authoritative shared space.

**Against [[breunig-harnesses-are-situated-agents|Breunig]]:** Breunig looks at the same August-2026
harness census and concludes the metapattern is the **situated agent** — eight layers of world around a
small core loop — not a ladder of successive "X engineerings." Wong's ladder and Breunig's onion are
two different shapes for the same material, and only Wong claims his rungs are disciplines.

## Links

[[graph-engineering]] · [[loop-engineering]] · [[harness-engineering]] · [[context-engineering]] ·
[[multi-agent-orchestration]] · [[agent-governance]] · [[agent-legibility]] · [[agent-explainability]] ·
[[decision-trace]] · [[agentwashing]] · [[langchain]] · [[prefect]] · [[jeremiah-lowin]] ·
[[prefect-loops-vs-graphs]] · [[wong-loop-engineering-teaching-ai-agents-how-to-think]] ·
[[voss-what-the-hell-is-a-loop-anyway]] · [[breunig-harnesses-are-situated-agents]] ·
[[edwards-alexander-an-accidental-blackboard]] · [[nick-tune-graphs-memory-skills-agents]]

_Source: [[wong-graph-engineering-wiring-agents-into-an-organization]] (raw: `raw/articles/wong-graph-engineering-wiring-agents-into-an-organization.md`)._
