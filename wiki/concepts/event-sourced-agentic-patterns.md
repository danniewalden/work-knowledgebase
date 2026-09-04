---
title: Event-Sourced Agentic Patterns
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [anthropic-building-effective-agents, akka-event-sourcing-backbone-agentic-ai, akka-agentic-systems-are-distributed-systems, langchain-state-of-agent-engineering-2026, deloitte-ai-agents-scaling-faster-than-guardrails, ning-code-as-agent-harness, graph-engineering-era-of-llm-agents-system-intelligence, dilger-podcast-episode-47-agentic-modeling-audit-trails, dilger-git-as-primary-persistence-for-event-models, nick-tune-event-sourced-claude-code-workflows]
tags: [agentic-ai, event-sourcing, patterns, synthesis, architecture]
---

# Event-Sourced Agentic Patterns

**The bridge between the KB's two technical threads.** Thread 3 ([[anthropic]]) describes
*what shape* agentic systems take — the [[agentic-workflow-patterns]] and
[[multi-agent-orchestration]]. Thread 2 ([[akka]], [[kevin-hoffman]]) describes *what
substrate* they should run on — an [[event-sourcing]] backbone. This page argues they are
two halves of one design: the patterns describe the control flow; event sourcing is the
state and communication layer that makes that control flow reliable.

## Why the patterns need a backbone

Every source agrees agents are **nondeterministic**, and that this is the core engineering
problem ([[agentic-ai]]). The same property shows up three ways across the threads:

- Anthropic prescribes **transparency** (show planning steps) and **iteration** (measure,
  evaluate) — see [[agent-observability-and-evals]].
- [[langchain-state-of-agent-engineering-2026]]: observability/tracing is *table stakes*;
  quality is the #1 production blocker.
- [[deloitte-ai-agents-scaling-faster-than-guardrails]]: mature [[agent-governance]] needs
  **audit trails capturing the full chain of agent actions**.

An **append-only log of immutable events** answers all three at once — perfect recall, audit,
durable inter-agent communication, and versioning via replay ([[akka-event-sourcing-backbone-agentic-ai]]).
So the reliability practices Thread 3 demands are exactly what Thread 2's substrate provides.

## Mapping the patterns onto events

Each of Anthropic's patterns has a natural event-sourced expression:

- **Prompt chaining** → each step's output is an event; the "gate" check reads prior events.
  Replaying the log reproduces a run exactly — the reproducibility Anthropic asks for.
- **Routing** → the classification decision is a recorded event, making "why did it go
  there?" auditable after the fact.
- **Parallelization (sectioning/voting)** → independent worker outputs are events;
  aggregation is a projection ([[cqrs]]-style view) over them.
- **Orchestrator-workers** → the orchestrator's delegations and the workers' results are a
  conversation of events; this *is* [[multi-agent-orchestration]] when workers are separate
  agents, with [[agent2agent-protocol]] as the wire format and the event log as durable memory.
- **Evaluator-optimizer** → generate/critique/revise cycles become an event history; the loop
  is a fold over that history, and stopping conditions are predicates on it.

## The gap the harness literature names, from the other side (2026-05/08)

Two large surveys of agent harnesses independently arrive at this page's problem statement as an **unsolved
research problem** — both **arXiv preprints, not peer-reviewed**. [[ning-code-as-agent-harness|Ning et al.
(arXiv:2605.18747, 42 authors)]] list "**Transactional Shared Program State and Semantic Conflict
Resolution**" and "**Human-in-the-Loop Safety and Accountability as Harness State**" among their open
problems, and take an explicit position on a shared harness substrate with "harness-state convergence";
[[graph-engineering-era-of-llm-agents-system-intelligence|Feng et al. (arXiv:2608.21156)]] argue multi-agent
systems demand explicit structures "to maintain **evolving execution states**". Ning et al. also list
"**verification through deterministic sensors**" and "**planning as contract formation**" as harness
mechanisms — which is [[esaa-event-sourcing-for-autonomous-agents|ESAA]]'s boundary-contract design in
different vocabulary.

That is worth stating plainly and with its limits: **the harness field's open problem is this thread's claimed
answer.** Total ordering, an append-only log, conflict detection before effects apply, and accountability as
*stored state* rather than asserted process are exactly what event sourcing supplies. What the KB does **not**
have is any evidence that the harness community has tried it and found it wanting, or tried it at all — no
paper in the harness batch cites event sourcing. So this is an *unexploited* seam and a research question
("does an event-sourced substrate solve harness-state convergence?"), not a settled advantage.

## The unifying claim

The same idea underpins [[adam-dymitruk]]'s [[event-modeling]] (information systems as a
timeline of events) and Akka's agent infrastructure: **current state is a replay of an
append-only ledger.** Apply it to agents and the control-flow patterns become *event
schemas*, [[guardian-agents]] become *subscribers that veto or flag events before they
commit*, and governance audit trails are *the log itself*. [[anthropic]]'s "simplicity +
transparency + good ACI" principles and Akka's "event-sourced, distributed by default" thesis
point at the same well-instrumented, replayable agent.

## "Agents need an audit trail, not a snapshot" — and three layers of answer

[[adam-dymitruk]] states this page's thesis as a *requirement for agents*, in
[[dilger-podcast-episode-47-agentic-modeling-audit-trails]]:

> "Agents need an audit trail, not a snapshot. Events are the truth, the full story, not just the
> current state. Read models are derived and disposable. If an agent goes sideways, follow the event
> trail, find the divergence, fix it, replay. No mystery, no data surgery."

*(Provenance: the hosts are relaying a LinkedIn post by **Svet Angelov**, which is **not captured in
`raw/`** — so Dymitruk's endorsement is the citable part, not the origin. The episode's **date is
unresolved**: no date in HTML, metadata or body; absent from the RSS feed and from
podcast.eventmodeling.org, both still ending at Ep 46 (2026-04-26/27), so it post-dates 2026-04-27 and
may be a previously unpolled channel rather than a new item. **Show-notes level, not verified against
audio. VENDOR SELF-REPORT** for the tooling.)*

The claim is a *should*. What is new as of 2026-09 is that it has been answered at three distinct layers,
by three parties, **none of whom cite each other**:

| Layer | Answer | Source |
| --- | --- | --- |
| The **domain** the agents build | the event log itself — the KB's existing synthesis | this page; [[esaa-event-sourcing-for-autonomous-agents]] |
| The **specification** the agents work from | **git as primary persistence** for the event model: one repo per board, branching, BYODS, and *"you can store your models in a Worm-Drive for auditability"* | [[dilger-git-as-primary-persistence-for-event-models]] |
| The **agent loop** itself | persist **only events** from the workflow state machine, derive state by replay; the log yields per-state timings, rejection counts, hook-denial counts and a journal | [[nick-tune-event-sourced-claude-code-workflows]] |

**Why the middle row is the interesting one.** Every audit-trail argument in this KB so far has been
about the agent's *actions*. Making the **model's own history** the audit trail means you can prove what
the agent was *told* to build, not only what it did — a feedforward control on the spec rather than a
feedback control on the output ([[feedforward-and-feedback-controls]], [[agent-governance]]). *(**VENDOR
SELF-REPORT**; the git backend is **announced as being added, not reported in use**, and no auditability
requirement, regulation or auditor is named for the WORM claim.)*

**Why the bottom row is not the same claim as this page's.** Tune's consumers are harness-optimisation
questions — where did time go, which instructions are being violated — not domain queries, and his
purpose is *efficiency* where Dymitruk's is *correctness* (*"follow the event trail, find the
divergence, fix it, replay"*). Same substrate, different use. *(**IMPRESSION NOT MEASUREMENT · NOT
INDEPENDENT** — one session of his own personal-project harness, which he states.)*

## Open edge — now largely closed (2026-06-12)

This synthesis was originally the KB's own: [[anthropic]] doesn't mention event sourcing, and Akka
doesn't mention the five patterns. **That edge is now externally corroborated.** Three independent
2026 sources connect agent control flow to an event-sourced/[[event-driven-architecture]] substrate:
[[confluent-agentic-event-driven-systems-architecture]] (closed-loop control; immutability, replay,
projections, sagas as production design principles — see [[agentic-event-driven-systems]]),
[[atlan-event-driven-architecture-for-ai-agents]] (names **event sourcing** as one of four agent
patterns, alongside chaining, fan-out, saga), and [[solace-multi-agent-systems-real-time-context-eda]]
(analyst-grounded: EDA as the fabric for multi-agent systems). Caveat: all three are EDA-tooling
vendors, so the framing is motivated; and they describe event *streaming/sourcing*, not
[[event-modeling]] the design method.

The strongest corroboration is **non-vendor and academic**:
[[esaa-event-sourcing-for-autonomous-agents]] (arXiv, Feb 2026) applies [[event-sourcing]] + [[cqrs]]
to multi-agent LLM software engineering — agents emit validated JSON *intentions*, a deterministic
orchestrator appends them to an immutable log and projects a hash-verified read-model with replay
verification — and reaches the same conclusion as this page's synthesis without selling a product.
*Still genuinely open:* an external source connecting the five patterns specifically to
[[event-modeling]] (the method), and a **worked** model — see [[event-modeled-agent-design]]. The
nearest arrival since is [[nick-tune-event-sourced-claude-code-workflows]] (2026-03-04), which
event-sources the **agent loop** rather than the domain: a real running system whose source of truth is
the loop's own event history. It is **not** the method — no swimlanes, commands, read models or
timeline — so the gap stands, but it is the first published instance where an agent harness's state
*is* a projection of its events. *(**NOT INDEPENDENT · IMPRESSION NOT MEASUREMENT** — his own harness,
personal projects.)*

**Update (2026-06-11):** the related, higher-level question — does the [[event-modeling]] *method*
describe agent systems? — now has a primary source. [[adam-dymitruk]] states agents map onto Event
Modeling's existing **user** and **Automation/processor** roles
([[dymitruk-event-modeling-future-proof-agents]]). That's worked out in
[[event-modeled-agent-design]]. Still missing: a *worked* event model of a multi-agent/harness
system (assertion exists; example doesn't).

_Source pages: [[anthropic-building-effective-agents]] · [[akka-event-sourcing-backbone-agentic-ai]] · [[akka-agentic-systems-are-distributed-systems]] · [[langchain-state-of-agent-engineering-2026]] · [[deloitte-ai-agents-scaling-faster-than-guardrails]] · [[ning-code-as-agent-harness]] · [[graph-engineering-era-of-llm-agents-system-intelligence]] · [[dilger-podcast-episode-47-agentic-modeling-audit-trails]] · [[dilger-git-as-primary-persistence-for-event-models]] · [[nick-tune-event-sourced-claude-code-workflows]]._
