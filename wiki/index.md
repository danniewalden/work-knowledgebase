# Index

The catalog of every page in the wiki. The LLM updates this on every ingest and
reads it first when answering a query. Each entry: link + one-line summary.

## Overview

- [[overview]] — running synthesis of everything known so far

## Sources

- [[karpathy-llm-wiki]] — Karpathy's "idea file" describing the LLM Wiki pattern this KB is built on
- [[eventmodeling-what-is-event-modeling]] — Dymitruk's canonical write-up of the Event Modeling method
- [[semaphore-dymitruk-event-modeling]] — interview: Event Modeling vs. event storming, DDD, OCP, event sourcing
- [[akka-event-sourcing-backbone-agentic-ai]] — Akka: why event sourcing is the foundation for agentic AI
- [[akka-agentic-systems-are-distributed-systems]] — Akka: agentic systems are inherently distributed systems
- [[anthropic-building-effective-agents]] — Anthropic's practitioner guide: build agents from simple, composable patterns
- [[deloitte-ai-agents-scaling-faster-than-guardrails]] — Deloitte survey: only 21% have mature agentic-AI governance
- [[langchain-state-of-agent-engineering-2026]] — LangChain survey (1,340): production, use cases, blockers, tooling
- [[svitla-agentic-ai-market-trends-2026]] — five 2026 trends; adoption-vs-production gap; case studies
- [[mcp-specification-2025-11-25]] — primary MCP spec overview: roles, features, security principles
- [[a2a-protocol-overview]] — primary A2A docs: agent-to-agent interop, Linux Foundation, spec layers
- [[gartner-40-percent-enterprise-apps-task-specific-agents-2026]] — primary Gartner release: five-stage forecast, origin of "agentwashing"
- [[fowler-bockeler-harness-engineering]] — Böckeler/Thoughtworks: the guides-and-sensors mental model for coding-agent harnesses
- [[fowler-bockeler-maintainability-sensors]] — Böckeler's sensors-only field report: linting, dependency rules, AI modularity review, mutation testing
- [[openai-harness-engineering-codex]] — OpenAI case study: ~1M LOC shipped with zero hand-written code via Codex
- [[anthropic-effective-harnesses-long-running-agents]] — Anthropic's initializer-executor recipe for agents across many context windows
- [[langchain-anatomy-of-an-agent-harness]] — LangChain's first-principles "Agent = Model + Harness" decomposition
- [[firecrawl-what-is-an-agent-harness]] — definitional survey collating the harness discourse (vendor blog)
- [[hashimoto-my-ai-adoption-journey]] — Hashimoto's six-step essay; the primary source that named "harness engineering"
- [[stripe-minions-one-shot-coding-agents]] — Stripe's unattended one-shot agents: 1,000+ merged PRs/week
- [[dymitruk-event-modeling-future-proof-agents]] — Dymitruk: agents are "users or processors" in Event Modeling (primary)
- [[qlerify-event-modeling-tool-ai]] — AI-assisted Event Modeling tool; "Automation as an actor"; GWT per event
- [[confluent-agentic-event-driven-systems-architecture]] — Confluent: 8-layer closed-loop agentic EDA; event sourcing as agent design principles
- [[solace-multi-agent-systems-real-time-context-eda]] — Solace: Gartner/IDC case that multi-agent systems need EDA + real-time context
- [[atlan-event-driven-architecture-for-ai-agents]] — Atlan: EDA patterns for agents; names event sourcing as a core agent pattern
- [[proophboard-skills-ai-agent-event-modeling]] — prooph board repo: AI agent skills + MCP server for *doing* Event Modeling (focus area)
- [[esaa-event-sourcing-for-autonomous-agents]] — academic preprint: event sourcing + CQRS for multi-agent LLM SWE (non-vendor corroboration)
- [[jwilger-agent-skills-event-modeling]] — portable agent skills: EM output (slices + GWT) governs an autonomous coding "factory" (focus area)
- [[dilger-faros-ai-report-amplifies-unclear-requirements]] — Dilger on Faros AI report: AI amplifies unclear requirements; Event Model as the fix (focus area)
- [[dilger-spec-driven-development-applied]] — Dilger: you can't force an agent, you design the environment; EM as the spec (focus area)
- [[dilger-keep-command-handlers-pure]] — Dilger: Claude Code drifted off the event model into the routing layer; enforce, don't just document (focus area)
- [[dilger-automatic-domain-discovery-claude-code]] — Dilger: an agent maps a product's live UI into a visual storyboard; automated discovery (focus area)
- [[dilger-model-is-a-living-spec-always-on-agent]] — Dilger: the model is a *live* spec; an always-on agent builds from board edits; slice→tests-as-harness→PR 24/7 pipeline (focus area)
- [[dilger-hold-my-beer-engineer]] — Dilger: short teaser fronting an "Event Modeling applied" article; solution-first instinct vs. model-first (stub, focus area)
- [[fraktalio-event-modeler-connect-ai-agents-mcp]] — Fraktalio: Event Modeler ships MCP agent integration; agent authors the model + GWT-per-command (focus area)
- [[pellegrini-dynamic-consistency-boundary]] — Pellegrini: origin post naming Dynamic Consistency Boundary; DCB as an event-sourcing optimistic lock (seed source)
- [[bogard-vertical-slice-architecture]] — Bogard: origin post for Vertical Slice Architecture; couple in a slice, not across layers; CQRS out of the gate (seed source)
- [[tornhill-codescene-unhealthy-code-agentic-token-cost]] — Tornhill/CodeScene: unhealthy code +35–45% agent token spend; agents worst in high-debt legacy code (code health × harness)
- [[goeleven-event-sourcing-not-auditing-for-free]] — Goeleven: event sourcing ≠ auditing for free; augment the decision log with who/when/where/what/why; business-capability streams (focus substrate)
- [[goeleven-event-model-to-code-series]] — Goeleven: translating an Event Model into code; role + business-capability swimlanes; command→Aggregate→events→Outbox→Projection→read model (focus area)
- [[homann-business-capabilities]] — Homann (Microsoft, 2006): seminal primary on business-capability mapping; capability = "what not how" black box; connectors; nested taxonomy (focus area)
- [[daniel-event-modeling-wardley-mapping]] — Daniel: Event Modeling × Wardley Mapping; Wardley=where/why, EM=what to build (stub, focus area)
- [[dilger-craft-conf-idea-to-event-model-to-code]] — Dilger (Craft Conf talk): "what if requirements were something you could run?"; idea→model→code→back; model as living spec driving codegen + agentic coding (focus area)
- [[nick-tune-graphs-memory-skills-agents]] — Nick Tune: Graph + Memory + Skills + Agent as the substrate underneath an agent; "model is the commodity, context is the product" (focus area)

## Entities

- [[andrej-karpathy]] — AI researcher; originator of the LLM Wiki and append-and-review note
- [[adam-dymitruk]] — creator of Event Modeling; CEO/founder of Adaptech Group
- [[adaptech-group]] — Dymitruk's consultancy; where Event Modeling was developed; fixed-price delivery
- [[kevin-hoffman]] — Akka PM/author; argues event sourcing is the backbone of agentic AI
- [[akka]] — Lightbend's distributed-systems platform, positioned for agentic AI
- [[greg-young]] — CQRS/event-sourcing figure; long-running process specs Event Modeling builds on
- [[alberto-brandolini]] — creator of Event Storming, the workshop Event Modeling evolved from
- [[anthropic]] — AI lab; author of the effective-agents guide; maker of Claude, MCP, Claude Code
- [[deloitte]] — professional-services firm; publisher of the 2026 State of AI in the Enterprise survey
- [[langchain]] — maker of LangChain/LangGraph/LangSmith; author of the State of Agent Engineering survey
- [[gartner]] — analyst firm; source of the most-cited agentic-AI forecasts (adoption, agentwashing, guardian agents)
- [[salesforce-agentforce]] — Salesforce's agentic platform; most-cited production deployment example
- [[svitla-systems]] — AI/ML services firm; author of the 2026 market-trends survey
- [[openai]] — AI lab; maker of Codex; flagship harness-engineering case study
- [[thoughtworks]] — software consultancy; home of Böckeler and the harness-engineering article's venue
- [[birgitta-bockeler]] — Thoughtworks Distinguished Engineer; author of the harness-engineering mental model
- [[martin-fowler]] — software-engineering author; martinfowler.com is the article's publication venue
- [[mitchell-hashimoto]] — HashiCorp/Ghostty founder; named "harness engineering" (Feb 2026)
- [[stripe]] — fintech; built "minions," unattended one-shot coding agents at production scale
- [[qlerify]] — online AI-assisted Event Modeling tool; generates models and code from descriptions
- [[confluent]] — Kafka/Flink data-streaming vendor; author of the agentic EDA architecture write-up
- [[solace]] — event-broker/"Agent Mesh" vendor; author of the MAS-needs-EDA analyst synthesis
- [[atlan]] — metadata/governance "context layer" vendor; author of the EDA-for-agents primer
- [[prooph-board]] — online Event Modeling tool + Cody Engine; ships AI agent skills and an MCP server
- [[idc]] — analyst firm; cited for the "80% of agentic use cases need real-time data by 2027" forecast
- [[john-wilger]] — developer; author of jwilger/agent-skills (Event Modeling as an agent SDLC skill + factory pipeline)
- [[martin-dilger]] — Event Modeling/event-sourcing practitioner; author "Understanding Eventsourcing"/"Spec Driven"; building eventmodelers.ai
- [[eventmodelers-ai]] — Dilger's agentic software modeling platform; automated UI domain discovery; spec-driven agent builds
- [[fraktalio]] — Belgrade tooling company; Event Modeler board with MCP agent integration (agent authors model + GWT) (focus area)
- [[sara-pellegrini]] — software architect; originator of Dynamic Consistency Boundaries and the "Kill Aggregate" series
- [[jimmy-bogard]] — .NET OSS author (AutoMapper, MediatR); originator of Vertical Slice Architecture
- [[adam-tornhill]] — CodeScene founder; behavioral code analysis; code health as a lever on AI-agent cost/reliability
- [[yves-goeleven]] — Azure MVP / NServiceBus core team; event modeling, event sourcing, business-capability design (focus substrate)
- [[ulrich-homann]] — Microsoft architect; author of the seminal 2006 business-capability-mapping paper
- [[nebulit]] — Martin Dilger's company (GmbH); Event Modeling / event-sourcing consulting + training; vehicle behind eventmodelers.ai
- [[nick-tune]] — DDD author/architect; watch-listed voice on agent substrate (Graph+Memory+Skills) and context engineering

## Concepts

- [[llm-wiki]] — pattern where an LLM compiles raw sources into a persistent, compounding wiki
- [[append-and-review-note]] — single plain-text note; append to top, let old notes sink, review
- [[retrieval-augmented-generation]] — retrieve-at-query-time approach the LLM Wiki contrasts with
- [[memex]] — Vannevar Bush's 1945 curated knowledge store; spiritual predecessor of the LLM Wiki
- [[event-modeling]] — design systems as a timeline of events; 3 blocks, 4 patterns, 7-step workshop
- [[event-sourcing]] — store state as an append-only log of immutable events ("no erasers")
- [[event-storming]] — Brandolini's sticky-note domain workshop; Event Modeling's origin
- [[cqrs]] — separate write (commands) from read (views); the basis of Event Modeling's building blocks
- [[agentic-ai]] — goal-seeking, autonomous LLM systems; nondeterministic, inherently distributed (hub page)
- [[domain-driven-design]] — match code to the business domain; shown in Event Modeling via swimlanes
- [[agent-vs-workflow]] — Anthropic's distinction: predefined code paths vs LLM-directed processes
- [[augmented-llm]] — the building block: an LLM with retrieval, tools, and memory
- [[agentic-workflow-patterns]] — five composable patterns: chaining, routing, parallelization, orchestrator-workers, evaluator-optimizer
- [[multi-agent-orchestration]] — specialized agents coordinating; MCP (vertical) + A2A (horizontal)
- [[model-context-protocol]] — Anthropic's standard for connecting agents to tools/data (agent→system)
- [[agent2agent-protocol]] — Google's protocol for agent→agent delegation (agent→agent)
- [[agentic-coding]] — most-used daily agent type; verifiable via tests; Claude Code, Cursor, Copilot
- [[customer-support-agents]] — most common production use case; conversation + tool-driven action
- [[agentic-commerce]] — agents that compare, decide, and buy on a user's behalf
- [[agent-engineering]] — discipline of iterating nondeterministic LLMs into reliable systems
- [[agent-observability-and-evals]] — tracing + offline/online evals; quality is the #1 production blocker
- [[agent-governance]] — decision boundaries, monitoring, audit trails; only ~21% mature
- [[guardian-agents]] — agents that monitor other agents for compliance, safety, drift
- [[agentwashing]] — marketing assistants as agents; explains the adoption-vs-production gap
- [[autonomy-ladder]] — chain → workflow → partially → fully autonomous; most deployments at L1–2
- [[event-sourced-agentic-patterns]] — synthesis: Anthropic's patterns mapped onto the event-sourcing backbone
- [[event-modeled-agent-design]] — synthesis: Event Modeling as a design method for agent/multi-agent systems (focus area)
- [[harness-engineering]] — hub: building/improving the agent harness; failure → permanent fix
- [[agent-harness]] — Agent = Model + Harness; primitives, architecture patterns, vs framework/orchestrator
- [[context-engineering]] — deciding what enters the context window each step; nested inside harness engineering
- [[context-rot]] — degradation as the context window fills; the problem context engineering manages
- [[long-running-agents]] — agents working across many context windows; the initializer-executor pattern
- [[feedforward-and-feedback-controls]] — guides vs sensors × computational vs inferential (Böckeler)
- [[agent-legibility]] — optimise the repo for the agent's understanding; "what it can't see doesn't exist"
- [[ralph-loop]] — hook that reinjects the prompt in a clean context window to continue work
- [[unattended-coding-agents]] — agents that run with no human in the loop until a PR is ready (Stripe minions; Hashimoto's background agents)
- [[claude-agent-sdk]] — Anthropic's general-purpose agent harness; foundation beneath Claude Code
- [[event-driven-architecture]] — events-not-calls design style; the genus containing event sourcing/CQRS; why agents converge on it
- [[agentic-event-driven-systems]] — closed-loop agents on an event backbone; event sourcing restated for agents (external bridge)
- [[open-closed-principle]] — open for extension, closed for modification; the basis of Event Modeling's flat feature-cost curve
- [[conways-law]] — systems mirror team communication structure; applied as swimlanes in Event Modeling
- [[react-loop]] — reason → act → observe loop that drives an agent's per-step tool use
- [[fitness-functions]] — automated architecture-invariant checks; the "architecture fitness" harness category
- [[mutation-testing]] — measures test-suite *effectiveness* (surviving mutants); the sensor that catches the coverage illusion
- [[spec-driven-development]] — produce a clear spec before code; in the agent era, the spec is the environment that constrains the agent (focus area)
- [[domain-discovery]] — the "understand" phase of modeling; now also done by agents walking a product's live UI (focus area)
- [[dynamic-consistency-boundaries]] — DCB: per-decision runtime consistency scope (optimistic lock) replacing the fixed aggregate; Pellegrini origin (focus substrate)
- [[vertical-slice-architecture]] — VSA: organize code by feature slice not layer; couple in a slice; CQRS out of the gate; maps to Event Modeling slices (focus substrate)
- [[business-capabilities]] — what an org does (stable "what" not "how"); capability swimlanes as long-term-stable boundaries; coupling/cohesion unit; agent ownership boundary (focus area)
- [[wardley-mapping]] — Simon Wardley's strategy maps (value chain × evolution); pairs with capabilities + Event Modeling (where-to-go vs what-to-build) (focus area, stub)
