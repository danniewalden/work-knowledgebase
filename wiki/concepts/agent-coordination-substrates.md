---
title: Agent Coordination Substrates
type: concept
created: 2026-09-04
updated: 2026-09-04
sources: [edwards-alexander-an-accidental-blackboard, addyosmani-code-agent-orchestra, wong-graph-engineering-wiring-agents-into-an-organization, prefect-loops-vs-graphs, esaa-event-sourcing-for-autonomous-agents, akka-event-sourcing-backbone-agentic-ai, ning-code-as-agent-harness, graph-engineering-era-of-llm-agents-system-intelligence, breunig-who-taught-the-models-to-do-that, tornhill-merge-conflicts-agentic-bottleneck]
tags: [multi-agent, coordination, multi-agent-orchestration, event-sourcing, open-question, focus]
---

# Agent Coordination Substrates

**What many agents actually coordinate *through*** — as distinct from how they are decomposed
([[multi-agent-orchestration]]) or which protocol they speak ([[model-context-protocol]],
[[agent2agent-protocol]]). The KB now holds **four structurally different substrates**, one of them with a
1980s literature behind it, and **nobody has compared them.** This page exists to keep the comparison in
one place and to state the trade-off nobody in the sources acknowledges.

Why it matters more than it looks: two independent 2026 surveys name **shared state across agents** as
*the* open problem — [[ning-code-as-agent-harness|Ning et al.]] list "**Transactional Shared Program State
and Semantic Conflict Resolution**" among their open problems, and
[[graph-engineering-era-of-llm-agents-system-intelligence|Feng et al.]] argue multi-agent systems need
explicit structures "to maintain **evolving execution states**" *(both **arXiv preprints**, not
peer-reviewed)*. Whatever the substrate is, it is the thing the field says it does not yet have.

## The four substrates

| Substrate | Coordination happens via | Conflict handling | Evidence | Source |
| --- | --- | --- | --- | --- |
| **Shared task list** — statuses, explicit dependencies, file locking, peer-to-peer messages | a *structured, mutable* work registry | **partition**: "one file, one owner" | practitioner impressions + demo videos on a toy app | [[addyosmani-code-agent-orchestra]] |
| **Blackboard / tuple space** — schema-less shared memory, labelled deposits, no routing at all | *everyone reading and writing the same space* | none by design; claim/release emerges from what is written | n=1, four days, a **simulated** system; **no measurement of any kind** | [[edwards-alexander-an-accidental-blackboard]] |
| **Directed agentic graph** — nodes, permitted edges, authoritative vs convenience state | *explicit control flow* | fail loud on an undeclared handoff | vendor framing, pre-GA; the failure table is reasoned from a hypothetical | [[prefect-loops-vs-graphs]], [[wong-graph-engineering-wiring-agents-into-an-organization]] |
| **Append-only event log** — total order, one durable history, conflicts detected before effects apply | *a designed, ordered shared history* | optimistic concurrency / boundary contracts | design literature; **no multi-coding-agent deployment captured** | [[esaa-event-sourcing-for-autonomous-agents]], [[akka-event-sourcing-backbone-agentic-ai]] |

The fourth row is the important one for this KB: **it is the designed version of the second.** A blackboard
with a total order, a schema at the boundary, and conflict detection *is* an event log. The blackboard case
arrived by accident and died when its enabling mechanism was withdrawn; the log version was designed for
exactly this and has never been pointed at a fleet of coding agents.

## The trade-off nobody acknowledges: partition vs share

This is the substantive finding, and it is a genuine conflict between two sources that do not cite each
other:

- **[[addyosmani-code-agent-orchestra|Osmani's]] rule is partition by ownership** — *"One file, one owner.
  Never let two agents edit the same file. Conflicts kill velocity."* Coordination cost is avoided by
  making the shared surface small.
- **[[edwards-alexander-an-accidental-blackboard|The accidental blackboard]] required the opposite** —
  everybody reading and writing one surface, continuously, which is what produced not just claim/release
  but **knowledge transfer** (*"notes on how the line had been implemented"* delivered to the next agent
  for free).

Partition avoids the integration load and forfeits the knowledge transfer. Sharing buys coordination *and*
transfer, and has a **named capacity cost on one side only**: the frequent-push discipline that made the
blackboard work *"were overloading our CI pipeline"*, so it was backed off, *"which deprived the agents of
the continuous flow of updates on progress."* **The coordination substrate and the CI budget were in direct
conflict, and CI won** — which extends [[tornhill-merge-conflicts-agentic-bottleneck]] and generalises to
the observation that at agent scale the contended resource is **shared infrastructure**, not the codebase.

No source prices the other side. Nobody has measured what partitioning costs in re-derived context.

## What each substrate's own failure mode is

- **Shared task list:** the lead becomes a coordination bottleneck unless agents can message peers
  directly (Osmani's fix: the backend agent tells the frontend agent the API contract without going
  through the lead). *(**IMPRESSION NOT MEASUREMENT** for every quantity in that piece — see
  [[multi-agent-orchestration]].)*
- **Blackboard:** **not established to be reproducible, by the author** — *"I'm not convinced I would be
  able to reliably prompt our agents into doing it again"*, and the single prompt that started the cascade
  is **not published**. *(**NOT INDEPENDENT** — Thoughtworks on a Thoughtworks exercise, in Thoughtworks'
  own martinfowler.com series.)*
- **Graph:** *"the multi-agent version of a game of telephone — the reviewer agent approving something the
  writer agent never actually did"*, when each node keeps private context and passes a one-line summary.
  [[wong-graph-engineering-wiring-agents-into-an-organization|Wong's]] fix is the dimension the other
  accounts lack: be explicit about what is **authoritative** (the actual diff, the actual test output)
  versus what is a **convenience summary**.
- **Event log:** unproven here. The KB has the design argument and no instance of it coordinating a fleet
  of coding agents, which is precisely the gap to be honest about.

## Open questions — stated, not resolved

- **Nobody has compared them.** No captured source evaluates two substrates against each other on one
  workload. Every claim above is single-substrate.
- **Is the partition/share trade-off real or an artifact of tooling?** The blackboard died to a CI budget,
  not to a coordination failure. A cheaper propagation channel (which is what
  [[edwards-alexander-an-accidental-blackboard|the author concluded]] — *"I believe you want this
  communication channel to be sitting independently of source control"*, hence his purpose-built
  **Talwrn**, **no evidence yet**) might dissolve the trade-off entirely.
- **Does an event-sourced substrate solve harness-state convergence?** The harness field's open problem is
  this KB's substrate thread's claimed answer — and **no paper in the harness literature cites event
  sourcing at all**, so this is an *unexploited* seam and a research question, not a settled advantage.
  See [[event-sourced-agentic-patterns]].
- **Is the blackboard effect designed capability showing through?** [[breunig-who-taught-the-models-to-do-that|Breunig]]
  documents that labs deliberately trained models to persist, write plans down, and coordinate — so a repo
  full of in-progress plans is the obvious surface for trained behaviour to land on. On that reading the
  *capability* was engineered and only the **affordance** was accidental, which makes reproducibility a
  **harness** problem.

## Related

[[multi-agent-orchestration]] · [[graph-engineering]] · [[event-sourced-agentic-patterns]] ·
[[agentic-event-driven-systems]] · [[esaa-event-sourcing-for-autonomous-agents]] ·
[[context-engineering]] · [[decision-trace]] · [[software-factory]]

_Sources: [[edwards-alexander-an-accidental-blackboard]] · [[addyosmani-code-agent-orchestra]] · [[wong-graph-engineering-wiring-agents-into-an-organization]] · [[prefect-loops-vs-graphs]] · [[esaa-event-sourcing-for-autonomous-agents]] · [[akka-event-sourcing-backbone-agentic-ai]] · [[ning-code-as-agent-harness]] · [[graph-engineering-era-of-llm-agents-system-intelligence]]._
