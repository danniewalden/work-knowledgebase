---
title: Multi-Agent Orchestration
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [svitla-agentic-ai-market-trends-2026, anthropic-building-effective-agents, langchain-state-of-agent-engineering-2026, martinfowler-prince-building-reliable-agentic-ai-systems, devadoss-cead-capability-aligned-agent-design, graph-engineering-era-of-llm-agents-system-intelligence, ning-code-as-agent-harness, addyosmani-code-agent-orchestra, edwards-alexander-an-accidental-blackboard, wong-graph-engineering-wiring-agents-into-an-organization, breunig-who-taught-the-models-to-do-that, laycock-the-conductor-developer, tornhill-compressed-cognition-cost-of-faster-coding]
tags: [agentic-ai, multi-agent, architecture, protocols]
---

# Multi-Agent Orchestration

The 2026 shift from single, isolated agents toward **systems of specialized agents that
coordinate**, each contributing its specialization to a shared outcome
([[svitla-agentic-ai-market-trends-2026]]). Example chain: an inventory agent detects a
low-stock pattern → notifies a procurement agent → contacts supplier agents and orders →
triggers a logistics agent to schedule delivery, with no single agent owning the whole process.

Generalizes [[anthropic]]'s **orchestrator-workers** pattern ([[agentic-workflow-patterns]])
from one process to cross-system collaboration. Two protocols make it practical:

- **[[model-context-protocol]]** (MCP, Anthropic) — the *vertical* layer: agent → tools/systems.
- **[[agent2agent-protocol]]** (A2A, Google) — the *horizontal* layer: agent → agent
  delegation and communication.

Most new enterprise architectures plan to use both together. The trajectory points toward
agent-to-agent ecosystems and "agentic front ends" replacing some native applications — but
also toward distributed-systems problems (debugging, failure points, coordination overhead),
echoing [[akka]]'s thesis that [[agentic-ai]] is **inherently distributed**
([[akka-agentic-systems-are-distributed-systems]]). Caveat: most agent-to-agent interaction
in 2026 is still experimental. For why an event-sourced log is a natural substrate for this
coordination, see [[event-sourced-agentic-patterns]]; for the four substrates side by side, see
[[agent-coordination-substrates]].

## Multi-agent systems (MAS) and the EDA fabric (2026-06-12)

[[solace-multi-agent-systems-real-time-context-eda]] frames the same shift as **multi-agent
systems (MAS)** and adds the analyst case ([[gartner]], [[idc]]): single agents reliably pick from
only a handful of actions per step and compound errors over multi-step runs, so enterprises need
MAS — but MAS only works if agents have **real-time context** and coordinate over an
[[event-driven-architecture]] fabric, not direct calls. Gartner's "inner vs outer" agent
architecture (runtime/orchestrator/memory/tools/model vs IAM/gateways/observability/guardrails) and
the rule **agents coordinate via events, never direct calls** are spelled out in
[[confluent-agentic-event-driven-systems-architecture]]; see [[agentic-event-driven-systems]]. Adds a
governance dimension — **zero-trust identity** for non-human (agent) actors and least-privilege,
time-bounded entitlements ([[agent-governance]]).

## Production worked example (PRINCE, 2026-06)

[[martinfowler-prince-building-reliable-agentic-ai-systems|Bayer's PRINCE]] is a concrete, regulated
instance: a **LangGraph**-orchestrated workflow of specialized agents — Clarify-Intent → **Think & Plan**
→ **Researcher** (RAG + Text-to-SQL) → **Reflection** → **Writer** — with **three reflection loops**
(process / data / draft) and an evolution toward **domain-specific Researcher sub-agents** (toxicology vs
pharmacology) each owning their tools and schema. Notably it's orchestrated via an internal workflow
engine (not [[agent2agent-protocol|A2A]]), and its lesson is **context discipline** — route the right
context to each agent rather than one shared prompt (see [[context-engineering]]).

## Why one agent is not enough — the architectural-mismatch argument (Feng et al. 2026)

[[graph-engineering-era-of-llm-agents-system-intelligence|Feng et al. (arXiv:2608.21156)]] give the clearest
statement in the KB of why orchestration is architecture rather than plumbing — an **arXiv preprint survey,
not peer-reviewed**, and a position rather than a result. Some tasks "require heterogeneous expertise,
interdependent subtasks, parallel execution, **independent verification**, and **persistent state**, exceeding
any single agent's organizational capacity. Augmenting one agent's capabilities or context **cannot resolve
this architectural mismatch**." Note what two of those five drivers are: *maker≠checker*, and state that must
outlive a context window ([[long-running-agents]]). Their answer is [[graph-engineering]] — "explicit, dynamic,
evolving graph structures representing tasks, agents, and system states" — and the property they name is
**System Intelligence**.

The hard part is the shared state, and a second survey names it as an open problem from the code side:
[[ning-code-as-agent-harness|Ning et al.]] take an explicit position on a "Shared Code-Centric Harness
Substrate" with "harness-state convergence", and list "**Transactional Shared Program State and Semantic
Conflict Resolution**" among their open problems *(preprint)*. **That is ground the event-sourcing tradition
already claims to hold** — total ordering, an append-only log, conflicts detected before effects apply
([[esaa-event-sourcing-for-autonomous-agents]], [[agentic-event-driven-systems]],
[[event-sourced-agentic-patterns]]). The most direct research-gap-meets-existing-answer seam this batch
surfaces.

## Capability-aligned decomposition — CEAD (deVadoss, 2026-05)

[[john-devadoss|deVadoss's]] **CEAD** ([[devadoss-cead-capability-aligned-agent-design]]) is the KB's
most explicit prescription for *how to decompose* a multi-agent system: not by naming roles in a prompt
("role names are not architecture") but around **durable [[business-capabilities|business capabilities]]**
and their ownership/authority/state/evaluation boundaries — **"capability before agent, boundary before
topology."** Its runtime patterns are ordered smallest-first: start with a single **supervised
tool-using agent**, add **brokered specialists** only where a boundary is justified, use **verifier /
challenger** agents only with a distinct oracle, and reserve **peer-to-peer (A2A)** for
independently-owned agents. Each production agent needs an **Agent Capability Contract (ACC)**.

The paper is also the KB's clearest evidence on **proliferation cost**: over a 10,000-task simulation an
ungoverned 32-agent swarm scored 23.1% safe success vs 70.6% for CEAD, and even CEAD degrades past ~32
agents — coordination overhead, handoffs, and attack surface dominate. This mirrors [[akka]]'s
distributed-systems thesis and the [[confluent-agentic-event-driven-systems-architecture|events-not-direct-calls]]
rule from a *design-discipline* angle: **use the smallest number of agents that represent distinct
capability, risk, state, evaluation, and ownership boundaries.** Governance ([[agent-governance]]) alone
cannot rescue weak decomposition — a governance-first-but-design-poor grid still lost to CEAD.

## The repo as an accidental blackboard — and why it stopped working ([[edwards-alexander-an-accidental-blackboard|Edwards-Alexander, 2026-09-02]])

Ten Thoughtworks engineers, one room, four days, one monorepo, building a simulated airline **IROps**
system. Two independent decisions combined into a coordination substrate nobody designed:

1. Because many agents in one repo broke the build pipelines, agents were told to **continually commit and
   rebase from main** (initially: rebase after commit, then push, with all build checks in place).
2. Separately, agents were told to **plan, scope work to numbered sections of the shared spec, and store
   those plans in the repo**, updating them with progress.

*"These updates, alongside all others, were swept up with the new commit discipline. **Agents were able to
see other agents' progress.**"* What that produced: *"One agent would mark a line of the plan as in
progress, the other agent would see that and not work on that line. When the first agent finished, the
other agent would see not only that the work was complete… but would also be directly delivered **notes on
how the line had been implemented**."* Claim/release **plus** knowledge transfer, through commits. They
then used it deliberately — directing an agent to *"look at plans and source, monitor the repo, and when
the work for the cost model lands start to integrate it. **And it did.**"*

The pattern is the classic **blackboard system** (Hearsay-II, 1980; formalised as **tuple spaces** by
Gelernter et al., 1986): *"a shared memory that autonomous agents can read and write from independently…
tuples with a certain minimum structure, and then as many extra fields as you want: **no schema**…
They can each solve a decomposed part of the problem, drop their solution into the shared space, **label
it**, and other autonomous searchers will find it, pick it up, and use it."*

**Both caveats are the point:**

- **It is not established that this can be reproduced — by the author.** *"But it was an accident… It was
  missing some of the key parts of how blackboards operate. And because it was accidental, **I'm not
  convinced I would be able to reliably prompt our agents into doing it again.**"* They identified the
  single prompt that started the cascade (it is **not published**), but *"it was an emergent behaviour.
  It wasn't a directed behaviour."*
- **The mechanism was withdrawn and the effect died.** *"While we created it by directing a frequent push
  cycle, **we backed-off from that. The frequent commits were overloading our CI pipeline.** We switched
  to only push when a more coherent chunk of change was complete. **This deprived the agents of the
  continuous flow of updates on progress.**"* **The coordination substrate and the CI budget are in
  direct conflict, and CI won.** Any claim that "commit early and often solves multi-agent collision" now
  has a named capacity cost — which extends [[tornhill-merge-conflicts-agentic-bottleneck]].

His own conclusion is that **the channel should not be source control**: *"I believe you want this
communication channel to be sitting independently of source control."* He is building **Talwrn** (Welsh
for a threshing pit) as a purpose-built agent blackboard — **no evidence yet**.

**Read it as designed capability showing through, not spontaneous invention.**
[[breunig-who-taught-the-models-to-do-that|Breunig]] documents that labs deliberately trained models to
persist, to write plans down, and to decompose and coordinate — so a repo full of in-progress plans is the
obvious surface for those trained behaviours to land on. On that reading the *capability* was engineered
by the labs and only the **affordance** was accidental, which makes the reproducibility problem a
**harness** problem — the author's own conclusion.

*(n=1, four days, a **practice exercise with a simulated airline**, not a client system. **No measurement
of any kind** — no throughput, no defect count, no non-blackboard arm, no count of how often
claim/release actually fired versus collided. Ten engineers in one room means the human coordination
channel was also wide open and no attempt is made to separate the two. **NOT INDEPENDENT** — Thoughtworks
on a Thoughtworks exercise, in Thoughtworks' own martinfowler.com series.)*

## Three coordination substrates, and nobody has compared them

This page's coding-agent coordination primitives come from
[[addyosmani-code-agent-orchestra|Osmani, 2026-03-26]], which names the **single-agent ceiling** as three
walls — **context overload**, **no specialization**, **no coordination** (*"even if you spawn helpers,
they can't communicate, share a task list, or resolve dependencies"*) — and the shift they force:
**conductor → orchestrator**, *"from one musician, real-time guidance"* to *"an entire ensemble,
asynchronous coordination,"* where *"the codebase becomes your canvas, not a conversation thread."*

**Osmani's substrate — a shared task list plus peer messaging.** Three layers: a **Team Lead**
(decomposes, synthesizes), a **shared task list** (statuses pending/in_progress/completed/blocked,
**explicit dependencies**, **file locking**), and independent **teammates** with their own context
windows. Two mechanisms carry the weight: **automatic dependency resolution** (a completed task flips its
blocked dependents to pending and a teammate picks them up) and **peer-to-peer messaging** — *"The backend
agent tells the frontend agent the API contract directly: 'GET /search?q= returns [{id,title,url}].' This
doesn't go through the lead… **This peer-to-peer approach prevents the lead from becoming a coordination
bottleneck**."* Also: **hierarchical subagents** (*"spawn two feature leads. Each feature lead then spawns
its own two or three specialists… The parent never sees those details"*) and a **dedicated `@reviewer`
teammate** — read-only, tools limited to lint/test/security-scan, **auto-triggered on every
TaskCompleted** — so *"the lead only sees green-reviewed code. It's like having a permanent CI quality
gate built into the team itself."*

**So the KB now holds three structurally different substrates:**

| Substrate | Coordination happens via | Source |
| --- | --- | --- |
| **Shared task list** — statuses, explicit dependencies, file locking, peer messages | a *structured, mutable* work registry | [[addyosmani-code-agent-orchestra]] |
| **Blackboard** — schema-less shared memory, labelled deposits, no routing at all | *everyone reading the same space* | [[edwards-alexander-an-accidental-blackboard]] |
| **Directed agentic graph** — nodes, permitted edges, authoritative shared state | *explicit control flow* | [[prefect-loops-vs-graphs]], [[wong-graph-engineering-wiring-agents-into-an-organization]] |

**No captured source compares them, and there is a real conflict between two of them.** Osmani's rule is
partition-by-ownership: **"One file, one owner"** — *"Never let two agents edit the same file. Conflicts
kill velocity."* The blackboard effect required the opposite: everybody reading and writing a shared
surface, continuously — and it **died when push frequency was reduced to protect CI**. Partition avoids
the integration load; sharing buys coordination *and* knowledge transfer. Neither source acknowledges the
trade-off. **Open question for this page** — and the full treatment, including the fourth (designed,
append-only-log) substrate the event-sourcing thread proposes, is on [[agent-coordination-substrates]].

**One more finding worth keeping, because it is about infrastructure rather than agents:** *"flaky
environments, which a single developer encounters as an annoying edge case, **become systemic blockers
when forty agents hit the same flaky test simultaneously**."* At agent scale the contended resource is
**shared infrastructure**, not the codebase — the same lesson the CI-overload finding above teaches, and
the reason [[addyosmani-agentic-code-quality|Osmani]] lists *"brittle environments that don't hold up
under script-driven stress"* alongside weak tests as a first-order cause of agent failure.

*(**IMPRESSION NOT MEASUREMENT** for every quantity in the orchestra piece — *"Parallelism (3x
throughput)"*, *"3-5 teammates is the sweet spot"*, *"three focused agents consistently outperform one
generalist working three times as long"*, *"substantially cuts stuck agents"*, the 180k/280k token budgets
and *"roughly 220k tokens total"* — practitioner judgement plus four demo videos on a toy bookmarks app.
Agent Teams is an **experimental** flag. **NOT INDEPENDENT**: the author is a Director at Google Cloud AI,
the piece promotes his own book and cites his own prior posts as support. Its **`AGENTS.md` percentages
are UNCITABLE** — presented as research with no study named or linked.)*

## The human-side ceiling on fan-out (2026-07/08) — disputed

CEAD's ~32-agent degradation above is a **machine-side** limit. There is a human-side one, and the KB's
two sources disagree about where it sits.

[[rachel-laycock]] ([[laycock-the-conductor-developer]]) puts it at eight to twelve: *"an engineer…
regularly have eight AI agents running in parallel. I've heard similar numbers from others. Ten. Twelve.
**Beyond that, they become the bottleneck**"* — and frames orchestration at that width as the emerging
shape of the job (the developer as conductor, *"someone has to hold the whole system in their head"*).
[[adam-tornhill]] ([[tornhill-compressed-cognition-cost-of-faster-coding]]) puts it at two:
*"I typically have one long-running agentic maintenance task that I just babysit, and then one focus
task. **Never more**"* — because *"it is the **parallelisation of human attention** that does not
scale."* He explicitly exempts machine parallelism ("yes, I understand sub-agents and machine
parallelisation. That is not what I'm objecting to"), so this is a claim about the *supervisor*, not the
topology.

**Both are anecdote-grade** — her 8/10/12 is hearsay from one unnamed engineer plus "others," his
ceiling of two is a personal rule — and the mechanism he offers (decision density, "3-4 things" in
working memory, self-interruption) is the only one on the table. Held open on
[[attention-bottleneck]]; the consequence for orchestration design is that fan-out has **two**
independent ceilings, and the human one may bind first.

_Source pages: [[svitla-agentic-ai-market-trends-2026]] · [[anthropic-building-effective-agents]] · [[solace-multi-agent-systems-real-time-context-eda]] · [[confluent-agentic-event-driven-systems-architecture]] · [[martinfowler-prince-building-reliable-agentic-ai-systems]] · [[devadoss-cead-capability-aligned-agent-design]] · [[graph-engineering-era-of-llm-agents-system-intelligence]] · [[ning-code-as-agent-harness]] · [[addyosmani-code-agent-orchestra]] · [[edwards-alexander-an-accidental-blackboard]] · [[wong-graph-engineering-wiring-agents-into-an-organization]] · [[breunig-who-taught-the-models-to-do-that]] · [[laycock-the-conductor-developer]] · [[tornhill-compressed-cognition-cost-of-faster-coding]]._
