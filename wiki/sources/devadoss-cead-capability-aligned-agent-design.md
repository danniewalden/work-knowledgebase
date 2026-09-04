---
title: "deVadoss — CEAD: A Capability-Aligned Enterprise Agent Design"
type: source
created: 2026-07-31
updated: 2026-07-31
sources: [devadoss-cead-capability-aligned-agent-design]
raw_file: [raw/papers/devadoss-cead-capability-aligned-enterprise-agent-design.md]
tags: [agentic-ai, multi-agent, business-capabilities, enterprise-architecture, soa, microservices, agent-governance, focus]
---

# deVadoss — CEAD: A Capability-Aligned Enterprise Agent Design

Paper by **[[john-devadoss]]** (InterWork Alliance; `johnd@ieee.org`), *"Designing Intelligent
Enterprise Agents: A Capability-Aligned Multi-Agent Architecture"*, arXiv:2605.08258 (cs.MA),
2026-05-07. Raw capture:
`raw/papers/devadoss-cead-capability-aligned-enterprise-agent-design.md`. The KB's most direct source
tying **[[business-capabilities]]** to multi-agent architecture — the agent-era descendant of Homann's
capability black box and the SOA service contract. Flagged-important focus material.

## What it argues

The thesis is **design-first, not governance-first**: governance is necessary but "cannot be the
primary organizing abstraction." The primary abstraction must be **agent design** — capability
boundaries, autonomy allocation, interaction protocols, tool/data authority, state and memory design,
verification design, and human-interaction design. **CEAD (Capability-Aligned Enterprise Agent Design)**
is a reference architecture that decomposes multi-agent systems around **durable business capabilities**
plus authority, state, evaluation, and ownership boundaries. Governance becomes a *supporting control
and assurance plane* that enforces the design, detects drift, and provides accountability — it does not
replace design.

SOA is used as an **exemplar** (contracts, registries, loose coupling, policy-aware integration) while
"explicitly rejecting the idea that services are agents": a service is a *passive capability invoked
through a contract*; an agent is an *active, goal-directed actor* that chooses actions, selects tools,
maintains context, and may talk to other agents. Microservices are used as a **cautionary precedent** —
decomposition without design discipline produced distributed monoliths and service sprawl, and agents
can repeat this at higher risk as **micro-agent proliferation**.

## Key points

- **"Capability before agent."** Design Principle #1: define the business capability and owner *before*
  naming the agent role or prompt. "Boundary before topology" (#2): decide ownership/data/action/state/
  evaluation boundaries before deciding one agent vs many. Decompose *only* where there is a durable
  reason — separate business ownership, materially different tool authority, distinct data
  classification, specialized evaluation, or independent release cadence.
- **The Agent Capability Contract (ACC)** — the core *design* artifact (not a governance form),
  analogous to the **SOA service contract/SLA** but extended for autonomy, model behavior, tools,
  memory, verification, escalation, and evaluation. Its 13 fields: business capability + owner;
  purpose/non-purpose; autonomy level; interaction topology; I/O schemas; tool inventory + scopes; data
  classification; state/memory design; model-behavior policy; verification design; human interaction
  triggers; evaluation evidence; observability/audit; versioning/deprecation. "The record of the design
  decision that justifies an agent's existence."
- **Five autonomy levels (L0–L4):** Observe → Draft → Prepare → Bounded-execute → High-autonomy-execute.
  Autonomy is "a design variable" assigned by action risk/reversibility/confidence/evidence, not by
  model capability. Avoid a binary "agent allowed/not" model.
- **Intelligent enterprise agent — 7-condition definition:** goal-directed intent handling;
  LLM-mediated cognition; tool-mediated action; bounded autonomy; state/memory; observable
  accountability (owner, identity, trace, eval record, cost record, escalation path); uncertainty
  handling. Explicitly excludes bare prompts, REST microservices, stateless chatbots, and unrestricted
  autonomous systems.
- **Four planes:** Intent & Outcome Layer → **Agent Design Plane** (the architectural center: capability
  map, ACCs, autonomy allocation, interaction topology, verifier strategy, eval oracles, retirement
  rules) → Agent Runtime Plane (supervisors, planners, specialists, memory/RAG, verifiers, tool routers,
  human approval) → Enterprise Capability Plane (SOA services, microservices, data products,
  [[model-context-protocol|MCP]] servers, [[agent2agent-protocol|A2A]] peers) → Supporting Control &
  Assurance Plane (identity, policy, evals, audit, change control).
- **Runtime patterns, smallest-first:** *supervised tool-using agent* is the default; add *brokered
  specialists* only for justified boundaries; *verifier/challenger* only with a distinct oracle;
  *peer-to-peer (A2A)* for independently-owned agents; *human-in-the-loop* is part of interaction
  design, not an exception path.
- **Evaluation over 10,000 enterprise tasks (Finance/HR/Procurement/IT/Legal/Sales/CustOps).** Safe
  success (functional success ∧ ¬policy-violation ∧ ¬memory-poisoning): **CEAD 70.6%** vs mono-agent
  45.2%, ungoverned micro-agent swarm 23.1%, SOA-brokered 58.8%, governance-first-but-design-poor grid
  50.8%. The governance-first grid had strong controls and high audit coverage yet still lost to CEAD —
  **governance cannot compensate for weak decomposition.** Ablations: removing the capability map + ACCs
  drops functional success and auditability the most.
- **Proliferation is real.** Ungoverned systems degrade sharply past 16–32 agents; even CEAD degrades at
  64. Rule: use the *smallest* number of agents that represent distinct capability/risk/state/eval/
  ownership boundaries. **"Role names are not architecture."**

## Why it matters here

CEAD is the **agent-era extension of the capability-boundary thesis** the KB has been building. Homann's
**black box with a contracted service-level expectation** ([[business-capabilities]]) becomes the ACC —
"a contracted black box now carrying autonomy, memory, and verification." It corroborates
[[yves-goeleven|Goeleven's]] "decisions are owned by the capability, not the individual" and the
"contract between capabilities" rule, and it independently arrives at [[rico-fritzsche|Fritzsche's]]
capability-as-home argument ([[autonomous-domain-capabilities]]) — the durable business capability, not
a role or a prompt, is where an agent lives. Its **"agent sprawl = distributed monolith"** warning is
the [[coupling-taxonomy]] lesson applied to agents. And "capability before agent / boundary before
topology" is the direct multi-agent restatement of Conway/Team-Topologies value-flow alignment
([[skelton-team-topologies-foundation-ai-roi]]).

Caveat: the evaluation is a **simulation** (a parameterized success/violation model over synthetic
tasks, Eqs. 1–3), not a field study — read the numbers as evidence for the *architectural claim*, not as
production benchmarks.

## Links

Entities: [[john-devadoss]], [[ulrich-homann]] (capability black box the ACC descends from),
[[anthropic]] (MCP), [[matthew-skelton]] (value-flow boundaries). Concepts:
[[business-capabilities]], [[autonomous-domain-capabilities]], [[multi-agent-orchestration]],
[[agent-governance]], [[coupling-taxonomy]], [[model-context-protocol]], [[agent2agent-protocol]],
[[autonomy-ladder]], [[agent-observability-and-evals]], [[domain-driven-design]], [[conways-law]].
Related: [[confluent-agentic-event-driven-systems-architecture]], [[event-modeled-agent-design]],
[[rico-fritzsche-autonomous-domain-capabilities-ccc]], [[homann-business-capabilities]].
