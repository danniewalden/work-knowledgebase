---
title: Overview
type: overview
created: 2026-06-11
updated: 2026-06-14
sources: [karpathy-llm-wiki, eventmodeling-what-is-event-modeling, semaphore-dymitruk-event-modeling, akka-event-sourcing-backbone-agentic-ai, akka-agentic-systems-are-distributed-systems, anthropic-building-effective-agents, deloitte-ai-agents-scaling-faster-than-guardrails, langchain-state-of-agent-engineering-2026, svitla-agentic-ai-market-trends-2026, mcp-specification-2025-11-25, a2a-protocol-overview, gartner-40-percent-enterprise-apps-task-specific-agents-2026, fowler-bockeler-harness-engineering, fowler-bockeler-maintainability-sensors, openai-harness-engineering-codex, anthropic-effective-harnesses-long-running-agents, langchain-anatomy-of-an-agent-harness, firecrawl-what-is-an-agent-harness, hashimoto-my-ai-adoption-journey, stripe-minions-one-shot-coding-agents, dymitruk-event-modeling-future-proof-agents, qlerify-event-modeling-tool-ai, confluent-agentic-event-driven-systems-architecture, solace-multi-agent-systems-real-time-context-eda, atlan-event-driven-architecture-for-ai-agents, proophboard-skills-ai-agent-event-modeling, esaa-event-sourcing-for-autonomous-agents, jwilger-agent-skills-event-modeling, dilger-spec-driven-development-applied, dilger-faros-ai-report-amplifies-unclear-requirements, dilger-keep-command-handlers-pure, dilger-automatic-domain-discovery-claude-code, dilger-model-is-a-living-spec-always-on-agent, dilger-hold-my-beer-engineer, fraktalio-event-modeler-connect-ai-agents-mcp, dilger-craft-conf-idea-to-event-model-to-code, nick-tune-graphs-memory-skills-agents]
tags: [meta, event-modeling, event-sourcing, event-driven-architecture, agentic-ai, agent-patterns, governance, market, harness-engineering]
---

# Overview

The running synthesis of this knowledge base — the current, best summary of what
is known across all ingested sources. The LLM keeps this current as sources are
added: it's the page you read to get the big picture without drilling into
individual pages.

## Current state

Five content threads now, plus the meta-layer this KB runs on. Threads 1–2 cover Event Modeling and
the event-sourcing backbone; 3 the agentic-AI landscape; 4 harness engineering (how to make agents
reliable); 5 the external bridge — agentic event-driven systems. An active focus connects Event
Modeling to agent design (see [[event-modeled-agent-design]]).

**Meta: how this KB works.** It's built on the [[llm-wiki]] pattern from [[andrej-karpathy]]
([[karpathy-llm-wiki]]): immutable raw sources are compiled into a persistent, interlinked
wiki that **compounds** rather than being re-derived per query — the contrast with
[[retrieval-augmented-generation]]. Descends spiritually from Vannevar Bush's [[memex]].

**Thread 1 — Event Modeling (a software-design method).** [[event-modeling]], created by
[[adam-dymitruk]] at [[adaptech-group]], describes information systems as a **timeline of
events** instead of current state, producing a buildable blueprint from just 3 building
blocks (events, commands, [[cqrs|views]]), 4 patterns, and a 7-step workshop
([[eventmodeling-what-is-event-modeling]], [[semaphore-dymitruk-event-modeling]]). It
evolved from [[alberto-brandolini]]'s [[event-storming]] and builds on [[greg-young]]'s
[[cqrs]]/event-sourcing work; it pairs with [[event-sourcing]] and expresses
[[domain-driven-design]] through swimlanes. Headline payoff: a **flat feature-cost curve**
that makes fixed-price, any-order delivery possible.

**Thread 2 — Event sourcing as the backbone of agentic AI.** [[kevin-hoffman]] of [[akka]]
argues that [[event-sourcing]] is the right foundation for [[agentic-ai]] because LLMs are
**nondeterministic**: an immutable event log gives perfect recall, auditability, durable
inter-agent communication, and versioning via replay
([[akka-event-sourcing-backbone-agentic-ai]]). A companion piece argues agentic systems are
**inherently distributed systems** — memory, streaming I/O, orchestration, semantic search,
regional resilience ([[akka-agentic-systems-are-distributed-systems]]). This thread is
externally corroborated in **Thread 5** below ([[agentic-event-driven-systems]]).

**Thread 3 — The agentic-AI landscape (patterns, market, governance).** Four 2025–2026 sources
widen the [[agentic-ai]] hub beyond Akka's infrastructure framing:

- **How to build them.** [[anthropic]]'s effective-agents guide ([[anthropic-building-effective-agents]])
  is the engineering bedrock: start from the [[augmented-llm]], compose five
  [[agentic-workflow-patterns]], and respect the [[agent-vs-workflow]] line — *simple,
  composable patterns over heavy frameworks*. The frontier is [[multi-agent-orchestration]]
  over two protocols, [[model-context-protocol]] (agent→system) and [[agent2agent-protocol]]
  (agent→agent).
- **Where the market is.** [[svitla-agentic-ai-market-trends-2026]] frames the defining tension:
  rapid growth (Gartner: 40% of enterprise apps embedding agents by end-2026) against a
  **~79%-adoption vs ~11%-production gap**, explained by [[agentwashing]] and graded by the
  [[autonomy-ladder]] (most deployments at Level 1–2). Five trends: orchestration, [[agentic-coding]],
  [[guardian-agents]], [[agentic-commerce]], low-code agent building.
- **What works in production.** [[langchain-state-of-agent-engineering-2026]] (technical builders)
  shows ~57% in production, with **quality — not cost — as the #1 blocker**, making
  [[agent-engineering]] and [[agent-observability-and-evals]] table stakes. Top use cases:
  [[customer-support-agents]] and research/data analysis; coding agents dominate daily use.
- **The missing guardrails.** [[deloitte]]'s enterprise survey
  ([[deloitte-ai-agents-scaling-faster-than-guardrails]]) finds **only 21% have mature
  [[agent-governance]]** — adoption is outrunning oversight.

**Thread 4 — Harness engineering (how to make agents reliable).** Seven 2025–2026 sources converge
on a vocabulary: **Agent = Model + Harness**, where the [[agent-harness]] is everything around the
model and **[[harness-engineering]]** is the practice of treating every agent failure as a system
problem to permanently fix — the term named by [[mitchell-hashimoto]]
([[hashimoto-my-ai-adoption-journey]]: AGENTS.md lines + programmed verification tools).
[[langchain-anatomy-of-an-agent-harness]] decomposes the harness into primitives (filesystem,
sandbox, memory, compaction); [[birgitta-bockeler]]/[[thoughtworks]]
([[fowler-bockeler-harness-engineering]]) gives the user-side mental model — **guides (feedforward)
and sensors (feedback)**, each **computational or inferential** ([[feedforward-and-feedback-controls]]),
tuned in a **steering loop**; her follow-up field report
([[fowler-bockeler-maintainability-sensors]]) is the first *worked* example of the **maintainability**
category — sensors-only, almost no guides — finding that computational sensors (linting,
`dependency-cruiser`) win at the file/function level while cross-file modularity needs an inferential
"garbage-collection" review, and that **[[mutation-testing]]** is what exposes the coverage-illusion
once testing is left to AI. The builder-side case studies are [[openai]]'s zero-hand-written-code
product ([[openai-harness-engineering-codex]]: AGENTS.md as a map, [[agent-legibility]], custom
linters, garbage collection) and [[anthropic]]'s recipe for [[long-running-agents]]
([[anthropic-effective-harnesses-long-running-agents]]: initializer-executor, feature lists,
self-verification). The payoff is **[[unattended-coding-agents]]** — agents that run with no human in
the loop until a PR is ready: [[stripe]]'s **minions** ([[stripe-minions-one-shot-coding-agents]])
merge 1,000+ such PRs/week via a deterministic-loop-around-goose harness and tiered "shift-left"
lint/test feedback, while [[mitchell-hashimoto]] shows the modest individual-developer version.
Cross-cutting failure mode: **[[context-rot]]**, managed by **[[context-engineering]]** (which harness
engineering *uses* and extends). An outside practitioner voice, [[nick-tune]]
([[nick-tune-graphs-memory-skills-agents]]), restates this as the agent **substrate** — *Graph +
Memory + Skills* underneath the agent loop, "the model is the commodity, the context is the product" —
where **Memory** is [[event-sourcing]] in disguise (point-in-time-queryable history) and the **Graph**
is [[agent-legibility]] delivered as queryable structure rather than ad-hoc grepping, a fresh tie
between Thread 4 and Threads 1–2.

**How thread 4 ties in:** harness engineering is the environment-and-controls arm of
[[agent-engineering]] (thread 3) and the concrete answer to [[agentic-coding]]'s quality risk. Its
"harness as a cybernetic governor" overlaps with [[agent-governance]]. And it rhymes with threads
1–2: feature lists, progress files, and git history are an **append-only, replayable record** the
next agent session reads to recover state — the same instinct as [[event-sourcing]], applied to an
agent's working memory rather than a domain model.

**The connection between threads 1–2:** the same idea — an **append-only ledger of immutable
events**, with current state derived by replay — underpins both Dymitruk's information-system
blueprints and Akka's agent infrastructure. [[event-sourcing]] is the shared backbone.

**Thread 5 — Agentic event-driven systems (the external bridge, June 2026).** Three independent
2026 sources now connect [[agentic-ai]] to an [[event-driven-architecture]] / [[event-sourcing]]
substrate *explicitly* — the link the KB had previously only synthesized itself in
[[event-sourced-agentic-patterns]]. [[confluent-agentic-event-driven-systems-architecture]] is the
deepest: an 8-layer **closed-loop** reference architecture where agents *subscribe → reason →
publish* and never call each other directly, with production design principles (immutability,
exactly-once, **deterministic replay**, schema governance, policy-governed autonomy) that are
[[event-sourcing]] restated for agent decisions — captured as [[agentic-event-driven-systems]].
[[atlan-event-driven-architecture-for-ai-agents]] names **event sourcing** as one of four agent
patterns (chaining, fan-out, event sourcing, saga). [[solace-multi-agent-systems-real-time-context-eda]]
adds the analyst case ([[gartner]], [[idc]]) that **multi-agent systems** need EDA + real-time context
+ zero-trust agent identity ([[multi-agent-orchestration]], [[agent-governance]]). Caveat: all three
are EDA-tooling vendors ([[confluent]], [[atlan]], [[solace]]), so "you need EDA" is motivated — but
they agree with each other and with the independent [[akka]] thread, and Solace's claims trace to
Gartner/IDC. They describe event *streaming/sourcing*, **not** [[event-modeling]] the design method.

**Thread 1 ↔ 5 — tooling for *doing* Event Modeling with agents.** [[proophboard-skills-ai-agent-event-modeling]]
is a shipping repo of agent **skills + an [[model-context-protocol|MCP]] server** that let coding
agents create and work with [[event-modeling]] elements on **prooph board** ([[prooph-board]]) — the
visual counterpart to [[qlerify]]: the agent as a *practitioner* of Event Modeling. A **second
independent vendor** now sits on this rung: [[fraktalio]]'s Event Modeler exposes a `/mcp` endpoint
where an agent authors the model *and generates Given-When-Then per command, including business
exceptions* ([[fraktalio-event-modeler-connect-ai-agents-mcp]]) — MCP made literal as the agent↔EM
bridge.
[[jwilger-agent-skills-event-modeling]] ([[john-wilger]]) goes one step further on the same SKILL.md
pattern — the event model's *output* (vertical slices + GWT) becomes the **contract that governs an
autonomous coding factory**: GWT scenarios are the TDD acceptance gates, the event-model root is loaded
as context per slice, and autonomy is dialed up a Conservative→Standard→Full [[autonomy-ladder]] as
gates prove out. Together these are the closest concrete evidence yet for [[event-modeled-agent-design]]
and put it firmly on the **Thread 1 ↔ 4** seam ([[harness-engineering]], [[unattended-coding-agents]],
[[agentic-coding]]). Still not a *worked* event model of a multi-agent/harness system — jwilger's
pipeline *consumes* one it doesn't show (the standing gap). Running alongside is a
**practitioner-evangelist** voice, [[martin-dilger]] (building [[eventmodelers-ai]]), who argues the
*why* from daily practice: AI amplifies unclear requirements rather than fixing them
([[dilger-faros-ai-report-amplifies-unclear-requirements]]), so you stop prompting and design the
environment — the event model as [[spec-driven-development|spec]]
([[dilger-spec-driven-development-applied]]); the model dictates *where logic may live* and must be
enforced because agents drift ([[dilger-keep-command-handlers-pure]]); an agent can even bootstrap
the model from a running UI ([[dilger-automatic-domain-discovery-claude-code]],
[[domain-discovery]]); and he now describes the model run as a **live spec** — a background agent
building continuously from board edits, with a slice→tests-as-harness→PR loop that can go to a
modeling-agent→builder-agent "full autopilot" ([[dilger-model-is-a-living-spec-always-on-agent]];
[[long-running-agents]], [[unattended-coding-agents]]). His **Craft Conference** talk crystallizes the
whole thesis into one arc — *"what if your requirements were something you could run?"* — idea→event
model→code→back, naming the full EM + [[event-sourcing]] + [[cqrs]] + [[agentic-coding]] stack
([[dilger-craft-conf-idea-to-event-model-to-code]]). Framing-rich but vendor-marketing — strong
narrative, not independent evidence. Taken together the focus area now shows **both directions of
fit**: agents that *author* the model (Fraktalio, Dilger's discovery) and the model that *governs* the
agent (jwilger's gates, Dilger's slice loop).

**Threads 1 ↔ 4 — Event Modeling applied to agents (active focus).** [[adam-dymitruk]] states the
[[event-modeling]] *method* already describes agent systems — an agent is a **user** or an
**Automation processor**, composable into multi-agent systems without new notation
([[dymitruk-event-modeling-future-proof-agents]]); AI also assists the modeling itself
([[qlerify-event-modeling-tool-ai]]). The KB's synthesis [[event-modeled-agent-design]] maps Event
Modeling constructs onto the harness thread (events↔progress ledger, Automation↔executor/[[ralph-loop]],
GWT↔feature-list specs). This partly closes the long-standing "open edge" — though a *worked* event
model of a multi-agent/harness system is still missing.

**How thread 3 ties in:** Anthropic's nondeterminism-and-iterate framing, the demand for audit
trails in [[agent-governance]], and Akka's event-sourced agent memory are the same instinct from
different angles — *because agents are nondeterministic, you need recall, replay, and
auditability*. Anthropic's [[agent-vs-workflow]] distinction is the architectural twin of the
market's [[autonomy-ladder]].

## Open questions / next sources

- Has anyone applied **Event Modeling specifically** (not just event sourcing) to designing
  agent workflows? **Largely answered along a ladder:** [[adam-dymitruk]] asserts agents are
  users/processors in the model ([[dymitruk-event-modeling-future-proof-agents]]); [[prooph-board]]
  ships agents that *practise* EM ([[proophboard-skills-ai-agent-event-modeling]]); and [[john-wilger]]'s
  `agent-skills` ([[jwilger-agent-skills-event-modeling]]) makes the EM output the **contract that
  governs an autonomous coding factory** — the closest to a worked pipeline. See
  [[event-modeled-agent-design]]. *Still open:* a **worked event model artifact** of a
  multi-agent/harness system itself (jwilger consumes one but doesn't show it). Active focus area with
  a weekly research watch (see [[log]]).
- The agentic-AI sources were vendor content (Akka/Lightbend); now balanced by [[deloitte]]
  (independent survey), [[anthropic]] (practitioner engineering), and primary protocol/analyst
  specs. **Done:** primary [[gartner-40-percent-enterprise-apps-task-specific-agents-2026]],
  [[mcp-specification-2025-11-25]], and [[a2a-protocol-overview]] now sit in `raw/` and
  supersede the secondary Svitla citations for those facts. *Remaining:* Gartner's deeper
  figures live behind paywalled reports; IDC's $1.3T number is still secondhand.
- **Bridge gap — now externally closed (2026-06-12):** the KB's own synthesis
  ([[event-sourced-agentic-patterns]]) mapping Anthropic's patterns and
  [[multi-agent-orchestration]] onto the [[event-sourcing]] backbone is now corroborated by three
  external sources — [[confluent-agentic-event-driven-systems-architecture]],
  [[atlan-event-driven-architecture-for-ai-agents]], [[solace-multi-agent-systems-real-time-context-eda]]
  (see Thread 5 and [[agentic-event-driven-systems]]). *Remaining nuance:* these connect agents to
  event *streaming/sourcing*, not to [[event-modeling]] **the design method** — that specific edge
  ([[event-modeled-agent-design]]) is still the KB's own, and a *worked* multi-agent event model is
  still missing.
- **Captured & ingested (2026-06-12):** the **ESAA** paper (arXiv 2602.23193) — grabbed via the arXiv
  HTML version after the PDF yielded no text — is now [[esaa-event-sourcing-for-autonomous-agents]].
  It's the **non-vendor academic counterpart** to the Thread-5 sources: event sourcing + CQRS for
  multi-agent LLM SWE, reaching the same conclusion as [[event-sourced-agentic-patterns]] with nothing
  to sell. Uses event *sourcing*, not [[event-modeling]] the method, so it strengthens Thread 2, not
  [[event-modeled-agent-design]] directly.
- Capture the **full** MCP/A2A protocol definitions (sub-pages, schemas) if implementation-level
  detail is ever needed; only the spec overviews are in `raw/` so far.
- Deeper Event Modeling mechanics not yet pulled: the Given-When-Then tooling, the official
  spec/cheat-sheet, and worked examples beyond the hotel case.
- Original (still open): what domains will this KB ultimately cover? Event Modeling +
  agentic AI is the first real-content direction.
