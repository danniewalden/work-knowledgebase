---
title: Overview
type: overview
created: 2026-06-11
updated: 2026-08-16
sources: [ng-spec-driven-development-is-waterfall-in-markdown, bockeler-tdd-inside-the-agent-loop, dilger-eventmodelers-supports-esdm-export, dilger-highlighting-markers-give-context-to-agents, dilger-describing-without-solving-burns-you-out, dilger-the-shapes-event-modeling-anti-patterns, dilger-agentic-collaboration-freeform-drawings, dilger-99-percent-software-boring-two-patterns, dilger-event-model-structure-linter-reference-catalog, dymitruk-ai-melts-barrier-event-modeling-is-the-map, ahe-agentic-harness-engineering, dilger-triplet-flexible-agent-enabled-architecture, addyosmani-earning-taste-and-judgment, addyosmani-software-factories-light-and-dark, willison-fireside-chat-claude-code-team, karpathy-llm-wiki, eventmodeling-what-is-event-modeling, semaphore-dymitruk-event-modeling, akka-event-sourcing-backbone-agentic-ai, akka-agentic-systems-are-distributed-systems, anthropic-building-effective-agents, deloitte-ai-agents-scaling-faster-than-guardrails, langchain-state-of-agent-engineering-2026, svitla-agentic-ai-market-trends-2026, mcp-specification-2025-11-25, a2a-protocol-overview, gartner-40-percent-enterprise-apps-task-specific-agents-2026, fowler-bockeler-harness-engineering, fowler-bockeler-maintainability-sensors, openai-harness-engineering-codex, anthropic-effective-harnesses-long-running-agents, langchain-anatomy-of-an-agent-harness, firecrawl-what-is-an-agent-harness, hashimoto-my-ai-adoption-journey, stripe-minions-one-shot-coding-agents, dymitruk-event-modeling-future-proof-agents, qlerify-event-modeling-tool-ai, confluent-agentic-event-driven-systems-architecture, solace-multi-agent-systems-real-time-context-eda, atlan-event-driven-architecture-for-ai-agents, proophboard-skills-ai-agent-event-modeling, esaa-event-sourcing-for-autonomous-agents, jwilger-agent-skills-event-modeling, dilger-spec-driven-development-applied, dilger-faros-ai-report-amplifies-unclear-requirements, dilger-keep-command-handlers-pure, dilger-automatic-domain-discovery-claude-code, dilger-model-is-a-living-spec-always-on-agent, dilger-hold-my-beer-engineer, fraktalio-event-modeler-connect-ai-agents-mcp, dilger-craft-conf-idea-to-event-model-to-code, nick-tune-graphs-memory-skills-agents, rico-fritzsche-autonomous-domain-capabilities-ccc, miller-codebase-is-the-prompt-vertical-slices-ai, dymitruk-ai-trained-on-dysfunction-agents-are-a-must, dilger-dcb-is-what-event-sourcing-should-have-been, dilger-event-modeling-agent-harness, dilger-is-code-still-the-source-of-truth, dilger-adding-perspectives-to-event-modeling, atomicobject-cqrs-event-sourcing-production-walkthrough, tornhill-clear-design-principles-agentic-age, khononov-golden-age-of-modularity, event-modeling-event-sourcing-podcast, axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember, roden-event-sourcing-meets-mcp-whole-story-for-llms, borg-tornhill-code-for-machines-not-just-humans, coupling-research-note, addyosmani-loop-engineering, langchain-the-art-of-loop-engineering, swyx-loopcraft-art-of-stacking-loops, fowler-agentic-programming, bockeler-context-engineering-coding-agents, dilger-first-event-modeling-conference-munich-recap, anthropic-getting-started-with-loops, willison-rewriting-bun-in-rust, tornhill-why-human-level-ai-wont-be-enough, dilger-planning-like-excel-legible-to-human-and-ai, esdm-event-sourced-domain-modeling, adaptech-workflow-not-inside-giant-process-manager, dilger-extending-event-modeling-query-when, dilger-flea-market-model-to-deploy, dilger-drawio-model-in-code, jwilger-agent-skills-factory-pipeline, willison-vibe-engineering, prefect-loops-vs-graphs, khononov-microservices-hype-to-ai-sloop, devadoss-cead-capability-aligned-agent-design, skelton-team-topologies-foundation-ai-roi, willison-lethal-trifecta, yordis-prieto-code-is-the-ultimate-diagram, roden-too-many-islands-em-conf-2026, dora-roi-ai-assisted-software-development-2026, fritzsche-command-context-consistency-principle, fritzsche-who-owns-a-rule-shared-across-domain-capabilities, fritzsche-why-solid-is-outdated, fritzsche-choosing-storage-is-choosing-what-your-system-forgets, fritzsche-why-your-software-cannot-explain-business-decisions, dilger-spec-driven-tools-need-event-modeling-front-half, dilger-real-cost-of-ai-is-second-order]
tags: [meta, event-modeling, event-sourcing, event-driven-architecture, agentic-ai, agent-patterns, governance, market, harness-engineering]
---

# Overview

The running synthesis of this knowledge base — the current, best summary of what
is known across all ingested sources. The LLM keeps this current as sources are
added: it's the page you read to get the big picture without drilling into
individual pages.

## Current state

Six content threads now, plus the meta-layer this KB runs on. Threads 1–2 cover Event Modeling and
the event-sourcing backbone; 3 the agentic-AI landscape; 4 harness engineering (how to make agents
reliable); 5 the external bridge — agentic event-driven systems; 6 the design substrate around Event
Modeling (ES/DCB/CQRS/VSA/business capabilities). An active focus connects Event Modeling to agent
design (see [[event-modeled-agent-design]]).

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
that makes fixed-price, any-order delivery possible. The **running conversational primary** under
Threads 1–2 is Dymitruk & [[martin-dilger]]'s weekly [[event-modeling-event-sourcing-podcast]] (46 eps,
2024–2026), where the design substrate gets argued out: aggregate-killing → [[dynamic-consistency-boundaries|DCB]],
**sagas → to-do lists** (now with a dedicated primary — [[adaptech-workflow-not-inside-giant-process-manager|Adaptech's
"don't put your workflow inside a giant process manager"]]: a projected to-do list + focused
single-responsibility processors, [[process-managers-and-todo-lists]]),
[[vertical-slice-architecture|slices]] as the unit of work, [[given-when-then]]
specs, [[event-versioning-and-upcasting|schema migration]], and — dominating Season Two — AI /
[[agentic-coding]], the [[ralph-loop]], [[vibe-modeling]], and "Event Modeling 2.0." Captured as
**show-notes only** (YouTube transcripts were blocked), so it's framing/agenda evidence, not a verified
record.

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
- **Whether it pays off.** [[dora]]'s **2026 ROI report**
  ([[dora-roi-ai-assisted-software-development-2026]], Google Cloud) supplies the return-on-investment
  frame: **AI is an amplifier** of the organizational system (not the tools); value realises on a
  **J-Curve** (a productivity dip = learning curve + verification tax + downstream adaptation before
  gains); ROI flows through **seven capabilities → DORA delivery metrics → DevEx/UX → cost/revenue**; and
  the agentic-era reframing is *"ROI = latent human creativity unlocked, not headcount replaced."* Because
  inference cost fell ~280×, the cost centre **shifts from compute to governance** (the verification +
  instability taxes). It's the market-research face of the KB's environment-over-model through-line
  (cf. [[borg-tornhill-code-for-machines-not-just-humans]], [[dilger-harness-is-20-percent-requirements-are-80]])
  and the now-captured primary behind [[skelton-team-topologies-foundation-ai-roi]] (closing the standing
  [[dora]] marker).

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
between Thread 4 and Threads 1–2. Two **canonical primaries** now anchor the vocabulary the thread had
been citing loosely: [[martin-fowler]]'s [[fowler-agentic-programming|Agentic Programming]] bliki gives
the vendor-neutral *definition* (prompt-then-review; distinct from [[vibe-modeling|vibe coding]] and
autocomplete; names [[harness-engineering]] + domain understanding as the new skills), and
[[birgitta-bockeler]]'s [[bockeler-context-engineering-coding-agents|Context Engineering for Coding
Agents]] is the taxonomy primary under [[context-engineering]] (instructions vs guidance; context
interfaces; who-loads / how-much axes; the "illusion of control" caveat) — the predecessor memo to her
harness-engineering piece.

**Thread 4 sub-thread — loop engineering (the layer above the harness, June 2026, active focus).** A
named evolution of harness engineering has crystallized: **[[loop-engineering]]** — *designing the
system that prompts, verifies, and stops the agent, instead of being the one who prompts it.* Coined as
"loopcraft" by [[swyx]] ([[swyx-loopcraft-art-of-stacking-loops]], gathering the
Steinberger/Cherny/[[andrej-karpathy|Karpathy]] "loop discourse" and the **"Salty Lesson for agents"** —
build systems that scale with more agents, don't fix things yourself), it sits **one floor above the
[[harness-engineering|harness]]**: the harness makes one run reliable, the loop runs it on a timer, in
parallel, and feeds its own improvement. [[addyosmani-loop-engineering|Addy Osmani]] gives the
definitional build — **five primitives + on-disk memory** (automations = the heartbeat, worktrees,
skills, MCP connectors, maker≠checker sub-agents; "the agent forgets, the repo doesn't") shipping
natively in both Codex and Claude Code — with three caveats that *sharpen* as the loop improves
(verification is still yours, comprehension debt, cognitive surrender: "stay the engineer").
[[langchain-the-art-of-loop-engineering|LangChain]] supplies the **four-loop taxonomy** (agent →
verification grader → event-driven/always-on → **hill-climbing**, where an analysis agent reads traces
and *rewrites the harness config*) — loop 4 closing the missing return path from
[[agent-observability-and-evals]] back into the harness. This sub-thread absorbs and renames existing
KB concepts: [[ralph-loop]] is the level-1 agent loop made persistent;
[[long-running-agents]]/[[unattended-coding-agents]] ([[stripe-minions-one-shot-coding-agents|minions]])
are the level-3 event-driven loop. **[[anthropic]]'s own [[anthropic-getting-started-with-loops|"Getting
started with loops"]] (Claude Code team, 2026-06-30) now supplies the vendor-canonical counterpart** —
loops as "agents repeating cycles until a stop condition," classified into **turn-based / goal-based
(`/goal`) / time-based (`/loop`, `/schedule`) / proactive**, a near-exact cross-map onto LangChain's four
loops but named from the operator's side and tied to concrete primitives (the `/goal` evaluator model =
the grader loop; "encode the fix to improve the system" = the hill-climbing loop; a fresh-context
reviewer agent = maker≠checker). The stack now also has its **best public worked case at extreme scale**:
[[willison-rewriting-bun-in-rust|Willison on the Bun Zig→Rust rewrite]] — a **~1M-assertion TypeScript
test suite acting as a language-independent conformance suite** (the grader/verification loop made cheap
and deterministic) plus "monitored workflows… prompting Claude to edit the loop" and **"fixing the
process that generates the code instead of hand-fixing the code"** (the hill-climbing loop in the wild),
coordinated parallel agents, a +1M-line PR, ≈$165k in tokens — an existence proof that a conformance
suite can *be* the loop's grader. Open seam: whether an [[event-modeling|Event Model]] supplies the
loop's goals + stop conditions (slice = unit of work, [[given-when-then|GWT]] = the verification
rubric) — tying loop engineering to [[dilger-event-modeling-agent-harness|Dilger's Event Modeling Agent
Harness]] on the focus area. The strand's **light independent evidence is now partly addressed**: the
academic primary [[ahe-agentic-harness-engineering|AHE (Lin et al., Fudan/Peking, arXiv 2604.25850)]]
turns the hill-climbing loop into a controlled experiment — an evolution agent autonomously rewrites a
coding agent's **decoupled seven-component harness** (base model frozen) via three observability pillars
(component / experience / decision) plus a **falsifiable change-manifest with per-edit rollback**, lifting
Terminal-Bench 2 pass@1 69.7→77.0% over ten iterations and beating the hand-built Codex-CLI harness, with
the gain in **tools/middleware/memory not the prompt** and positive cross-benchmark/cross-model transfer
(largest on weaker bases — the environment substituting for model capability). It also names the loop's
honest failure mode ("regression blindness" — it can say why an edit helps but not what it will break).
Caveat: vendor/practitioner framing dominates the rest of the strand (LangChain product pitch, Anthropic
product doc, Osmani's own tooling-series, Willison's link-blog over Anthropic-internal data), strong
convergence; AHE is the first controlled evidence but is a single-benchmark research prototype. The strand
also gained its **top rung** — the [[software-factory]] ("an org chart made of loops":
[[addyosmani-software-factories-light-and-dark]], via [[dex-horthy]]), with **light-vs-dark**,
**back-pressure** (verification, not generation, is the constraint), and **loops-vs-graphs** as its handles,
and [[comprehension-debt]] as the debt a dark factory silently takes on — while
[[addyosmani-earning-taste-and-judgment]] names the **ungradeable residue** (taste/judgment) left to humans
once loops automate the reps, and [[willison-fireside-chat-claude-code-team|Anthropic's own team]] supplies a
worked instance (automated review built over months with an eval-set regression guard, markdown-per-channel
memory, auto mode). The strand is **no longer advocate-only**: [[vlad-khononov]]
([[khononov-microservices-hype-to-ai-sloop]]) is the KB's first **skeptic** on it — the "AI (s)loop" hype
rhymes with the microservices hype of 12 years ago, a crowd chasing something most can't define, likely to
end in a distributed-monolith-style hangover. The strand also has its **first negative eval** (2026-08-10):
[[birgitta-bockeler]] tested whether telling an agent to follow **TDD inside its own loop** helps and found
**no quality gain, no mutation-score gain, and 3–8.5× the tokens** — because the TDD instruction suppressed
the up-front design the non-TDD runs performed, and because a self-graded red step proves nothing ("a red
test tells you the agent ran it and saw failure, **not that the failure was for the right reason**")
([[bockeler-tdd-inside-the-agent-loop]]). Her generalisation is a design rule for the whole strand — stop
specifying *how* the model works, monitor **outcomes**, and be deliberate about "where we insert ourselves
as arbiters," i.e. spend the budget on [[feedforward-and-feedback-controls|sensors]] ([[mutation-testing]])
rather than process **guides**. It also sharpens rather than dents the focus area's
[[given-when-then|GWT]] claim: her target is the agent *inventing its own tests*, not an externally
authored acceptance spec — the specification belongs outside the loop, only the iteration inside. And a
**macro layer above the loop** has been named:
[[graph-engineering]] ([[prefect-loops-vs-graphs]], [[jeremiah-lowin|Lowin]]/Prefect) — loops model *one
agent's* internal behaviour, **directed agentic graphs** are the multi-agent orchestration *across* many
(nodes = agent invocations with per-node tools/model/access, edges hand control back), a framing adjacent to
[[nick-tune]]'s graph substrate and sparked by Steinberger's viral tweet. Term-lineage note: this whole
"accountable counterpart to vibe coding" vocabulary traces to [[willison-vibe-engineering|Willison's "vibe
engineering"]] (Oct 2025), which the field later renamed "agentic engineering." On the focus area, [[dilger-triplet-flexible-agent-enabled-architecture|Dilger's
"Triplet"]] now gives the EM×agents thread its packaged operating model — Event Modeling + Vertical Slices +
Event Sourcing in union, sold as a "flexible, agent-enabled architecture" whose low coupling is what makes a
slice cheap for an agent to build (one slice = one agent's context), the structural precondition under
[[dilger-event-modeling-agent-harness|the Event Modeling Agent Harness]].

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

**Thread 5 extension — the event *store* as agent memory (June 2026).** Two new event-sourcing-vendor
sources push past "agents need an event backbone" to *which* backbone, and *why it pays off twice*.
[[axoniq]] ([[allard-buijze]], creator of Axon Framework) argues agent
**[[agent-explainability|explainability]] is an infrastructure problem, not a model problem**:
state-based systems overwrite the causal history regulators now demand (EU AI Act, SR 11-7, GDPR
Art. 22), and only an event store can answer *why* a decision was made
([[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]]). It draws a sharper **event
store vs. event stream** line than the streaming sources above: a store records *why* (full causal
context, replayable), a stream (Kafka) only moves *what* — so the closed-loop backbone needs an
event-sourced *store of decisions*, not just a bus. [[golo-roden]] (the native web / EventSourcingDB)
takes the *context-quality* angle: CRUD is "only the last chapter," an event store gives an LLM "the
whole story," **events are the natural language for LLMs**, and [[model-context-protocol|MCP]] is the
data-agnostic bridge that exposes them ([[roden-event-sourcing-meets-mcp-whole-story-for-llms]]).
Synthesis: **the same immutable log delivers two agent payoffs — explainability (why it decided) and
context (what it needs to decide well)** — captured in the new [[agent-explainability]] concept, tying
Thread 5 to [[context-engineering]] (Thread 4) and the [[model-context-protocol|MCP]] focus seam. Both
are vendor-authored (motivated) but consistent with the independent [[akka]] thread and the non-vendor
[[esaa-event-sourcing-for-autonomous-agents|ESAA]] preprint. [[golo-roden]]'s company
[[thenativeweb]] has since extended this bet from the event *store* up to the *modeling* layer with
**[[esdm-event-sourced-domain-modeling|ESDM]]** (2026-07) — an MIT-licensed YAML language + offline
linter that describes event-sourced ([[domain-driven-design|DDD]]/[[cqrs]]/[[event-sourcing]]) domains
as version-controlled files, with [[dynamic-consistency-boundaries|DCB]] a first-class kind,
[[given-when-then|GWT]] + Domain Storytelling extensions, and "modeling with AI" a first-class use case.
It lands squarely on the **Threads 1↔4** focus as the open, tool-backed **file-format + linter rung** of
[[event-modeled-agent-design]] — the shipped counterpart to [[dilger-event-modeling-knowledge-hub-emlang|Dilger's
EmLang]] ambition (file-first + offline, vs the board+MCP camp of
[[fraktalio-event-modeler-connect-ai-agents-mcp|Fraktalio]]/[[proophboard-skills-ai-agent-event-modeling|prooph
board]]); it models ES/DDD/CQRS *structure*, not the [[event-modeling]] timeline method.

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
agent (jwilger's gates, Dilger's slice loop). Dilger has since crystallized the execution side into a
named **Event Modeling Agent Harness** ([[dilger-event-modeling-agent-harness]], 2026-06-17): a 24/7
[[ralph-loop]] whose **unit of work is the EM slice** on a Draft→Ready→In Progress→Done board, GWT
scenarios as the BDD feedback backbone, cheap local models doing the coding once a "blue-print
architecture" makes it "painting by numbers" — and argues a need for huge reasoning/context usually
signals **coupling**, not a model limit. He puts the stakes in an explicit **80/20 split**
([[dilger-harness-is-20-percent-requirements-are-80]], 2026-06-29): the harness and the code are only
~20% of the solution; the other **80% is clarifying requirements and business processes** — "a human,
communications problem" with no technical fix — so an event-modeled spec is what makes the harness pay
off (a pointed challenge to Thread 4 on *where the leverage is*). He states the underlying conviction plainly: **code is a
lagging indicator of intent; the model/spec is the source of truth**, so AI-generated code is "almost
disposable," regeneratable from the model with drift auto-detected
([[dilger-is-code-still-the-source-of-truth]]) — and even pushes model-as-single-source into the
visualization layer, projecting one event model into audience-specific **Perspectives** (and mooting
auto-generated C4) ([[dilger-adding-perspectives-to-event-modeling]]). He now names the **mechanism**
that makes an event model *agent-usable* ([[dilger-planning-like-excel-legible-to-human-and-ai]],
2026-07-09): freeform whiteboards (and Event Models) degrade without an owner, so [[eventmodelers-ai]]
uses an **Excel-like left-to-right grid** that enforces a storyboard *and* gives every element a
**cell-reference coordinate** — making the model addressable in both directions ("add a field in B3,
adjust all dependents" ↔ "there's a problem in B3…"). "Clear structure… is what makes a spec legible to a
human and an AI at once" — a concrete refinement of his model-as-agent-spec claim that also lands on the
[[ai-readable-code]] strand (legibility of the *spec*, not just the code). A cluster of **early-August
2026** Dilger posts adds a **third direction of fit — the agent *critiques* the model** (beyond
authors-it / governed-by-it): a `/wdyt` AI-skill that flags his named [[event-modeling-anti-patterns|"Shapes"
anti-patterns]] ([[dilger-the-shapes-event-modeling-anti-patterns]]) and a mooted **EM "linter"** grading a
board's structure against a reference catalog via Claude Code
([[dilger-event-model-structure-linter-reference-catalog]]) — model-level quality gates upstream of the
code-level GWT gate; plus a **freeform-drawing** modality where the agent reads board sketches and draws
back via MCP ([[dilger-agentic-collaboration-freeform-drawings]]), and the "**really only two patterns**"
(State change / State view) reduction whose point is that EM's *repetitiveness* gives an agent tight
guardrails not a blank page ([[dilger-99-percent-software-boring-two-patterns]]). The **mid-August**
continuation of that cluster does two things. First, it turns the "what form must the model take"
question into its own page, [[agent-readable-model-artifacts]]: the answer is **addressability**, and the
ladder now reaches its top rung — [[eventmodelers-ai]] **exports any Event Model to
[[esdm-event-sourced-domain-modeling|ESDM]]** (a *competitor's* open format) over UI/API/MCP/CLI, "so your
agent can request any modeled slice or chapter in the format it needs," with a joint [[golo-roden|Roden]]–Dilger
extension announced to carry EM's timeline into ESDM ([[dilger-eventmodelers-supports-esdm-export]]). That
closes the KB's standing "ESDM/EmLang materialization" gap, collapses the file-first-vs-board+MCP framing,
and is the first real bridge across the fragmentation [[roden-too-many-islands-em-conf-2026|Roden
complained about]] — arriving as vendor interop rather than governance
([[em-standardization-foundation]]). A third machine-readable surface lands alongside it: **screen
markers**, region-scoped "what matters right now" annotations agents read, validate, and build UI from
([[dilger-highlighting-markers-give-context-to-agents]]). Second — and more usefully — the cluster
finally supplies **counter-weight**. Dilger names the failure mode of his own thesis: teams that "stop
solving problems and just describe them, and then hand it to AI and hope it figures out the solution"
are "checking out before it gets interesting," and *"describing a problem without solving it leaves a
hole that keeps growing"*; he reports burnout from supervising five parallel agent sessions "like a
kindergartner," with the sharp aside that "a few years ago, we were obsessed with protecting people from
context switching. Now we call the same thing productivity"
([[dilger-describing-without-solving-burns-you-out]] — the requirements-side form of
[[comprehension-debt]]). The counter-weight then arrives from **outside** the thread as well
(ingested 08-16, Dannie-directed, published 2026-03):
[[ng-spec-driven-development-is-waterfall-in-markdown|Alvis Ng's "Spec-Driven Development Is Waterfall in
Markdown"]] was the KB's first *captured* external critique of [[spec-driven-development|SDD]] — **not the
first written**; see the correction on that page. It relays an empirical record the wiki did not then hold
— Eberhardt's Scott Logic SpecKit trial (on his own hobby app, not a production codebase; 2,577 lines of
Markdown across the whole feature, bugs surviving, and his impression of **~10x slower** than iterative
prompting), **Böckeler's** Kiro analysis (16 acceptance criteria for a minor bug fix; sole-authored, not
"Fowler/Böckeler"), Augment Engineer's 1,300 lines of Markdown to render a date, Marmelab's "The Waterfall
Strikes Back", and
[[gojko-adzic]] — from inside the BDD tradition — relayed as calling SDD "the revenge of waterfall or BDD
taken to a new level" (**a misreading: that is Adzic's title, posed as a question, and he answers the BDD
half "it does not, really" — primary captured 2026-08-31**). Ng's mechanism
is an *interface* argument rather than a quality one: an agent "produces code that matches the words, not
the intent," and a written spec **flattens designers, DevOps and product into one voice — the author's**,
so it becomes *"a contract between you and the LLM that nobody else signed."* His replacement is
[[decision-trace|a decision trace]] harvested from recorded cross-functional syncs (structured notes →
ticket → human-written prompt → in-flight decision log), which fails *legibly* where a stale spec fails
silently. Two things keep this from simply refuting the KB's thesis: his target is the **document-first
toolchains** (SpecKit/Kiro/Tessl), which is nearly the same complaint as
[[dilger-spec-driven-tools-need-event-modeling-front-half|Dilger's own "they skip the digging"]]; and
every figure is secondhand, from a solo personal trial, with an unevaluated replacement. What it does
force onto [[event-modeled-agent-design]] is a **sharper question than the KB had been asking** — not
*what form must the model take* (the addressability ladder above) but *whose model is it*, since a model
authored solo and handed to agents is exactly the artifact Ng describes, whatever its format; the wiki
has no captured evidence that modelling sessions resist that flattening in practice.
[[adam-dymitruk|Dymitruk]]
sharpens the durable-asset case in the same window: the model is the **map** into the system, so *which LLM
you use* "doesn't matter that much" — "picking up pennies in front of a steamroller"
([[dymitruk-ai-melts-barrier-event-modeling-is-the-map]]), the LLM-agnostic form of model-as-source-of-truth
(vs [[yordis-prieto-code-is-the-ultimate-diagram|Prieto's]] code-first inverse). The **first Event Modeling
Conference** (Munich, Oct 2025; recap [[dilger-first-event-modeling-conference-munich-recap]]) adds
three focus-relevant signals: a **Dymitruk×Dilger standardization JV** (new company for EM tooling +
standards, plus a certification program — a governance move for the method); [[allard-buijze]]'s
keynote demoing the **AxonIQ platform turning Event Models into working code** (the most concrete
model→code artifact yet for [[event-modeled-agent-design]], though a staged vendor demo); and a
**balanced, "it depends" reading of the [[dynamic-consistency-boundaries|DCB]]-vs-aggregates debate**
that tempers the partisan captures elsewhere in the KB. It also surfaces a notable tension —
Dilger's *"the model is not the implementation"* (a guide, not a blueprint) sitting against his own
[[dilger-is-code-still-the-source-of-truth|"model is the source of truth"]] line. The **2nd**
conference (25–26 June 2026) now **has its published recap** — [[golo-roden]]'s
[[roden-too-many-islands-em-conf-2026|"Too Many Islands, Too Few Bridges"]] (closing a watch item open
since 07-18). Its defining theme is that the ES/CQRS/DDD world is **"an archipelago"** — fragmented by
methodology, vocabulary, canonical examples, and tooling — and its outcome was **"The Munich Event"**, a
signed flip-chart proposal for a neutral **standards foundation** (Linux-Foundation/CNCF spirit) prioritising
shared terminology/formats/examples then wider adoption ([[em-standardization-foundation]]). Roden's own
talk, *"Your Domain Model Belongs in the Repository,"* argued the model must live as versioned plain text in
Git beside the code (else it "dies the moment the workshop ends") and demoed [[esdm-event-sourced-domain-modeling|ESDM]]
round-tripping **code→model→code** live with an AI (reverse-engineer a model from an app, then generate
Kotlin + Python from it) — a worked instance on the [[event-modeled-agent-design]] seam. This reframes
[[johansen-is-it-safe-to-jump-em-conf-2026|Johansen's]] "constraint is adoption, not technique" as: standardization *is* the adoption play. A sharp new **tension** also lands here: [[yordis-prieto-code-is-the-ultimate-diagram|Yordis Prieto]] argues the exact inverse of the model-first camp — **code is the source of truth, the diagram is a throwaway discovery tool** to be *regenerated from the code* — so the KB now holds both directions of the "regenerate to avoid stale artifacts" arrow (Roden/Dilger: code from the model; Prieto: the picture from the code), with Dymitruk endorsing both people despite the disagreement.

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

**Thread 6 — The design substrate around Event Modeling (ES / DCB / CQRS / VSA / business capabilities).**
Dannie broadened the focus (2026-06-14) to the engineering substrate beneath Event Modeling, and two
days of sources now populate it. **[[business-capabilities]]** (flagged important) is grounded on the
[[ulrich-homann]] 2006 primary (capability = stable "what", a black-box with a service-level contract)
and applied by [[yves-goeleven]] (capability swimlanes; "contract between capabilities"); **[[rico-fritzsche]]**
adds the agent-era sharpening — most architectures give a capability *no home*, so make each a
**Request Processing Unit** that builds local context from recorded events (**Command Context
Consistency**, [[autonomous-domain-capabilities]]). His 2026-06-17 follow-ups
([[rico-fritzsche-rpu-reactor-vocabulary]]) work this out fully — **retiring "Feature Slice"** for a
named vocabulary (RPU / Reactor / Interaction / Delivery Mechanism / Providers / Event Store) and framing
layered architecture as **"distributed technical ownership"** where the capability, not an object model
or aggregate, must be the boundary. **[[vertical-slice-architecture]]** ([[jimmy-bogard]]
origin) gains a concrete *AI-substrate* reading: [[jeremy-miller]]'s **"the codebase is the prompt"**
([[miller-codebase-is-the-prompt-vertical-slices-ai]]) argues layered code pollutes the context window
while feature slices keep work local ([[locality-of-reference]]) — bridging VSA to [[agent-legibility]]
and [[harness-engineering]] ("skills are the constitution; the slices are the code"). **[[dynamic-consistency-boundaries]]**
([[sara-pellegrini]] origin) gets a naming provocation from [[martin-dilger]]: DCB is just
[[event-sourcing]] done right, and the aggregate is the *static* boundary
([[dilger-dcb-is-what-event-sourcing-should-have-been]]). [[rico-fritzsche]] then locates his **CCC**
relative to DCB ([[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]]): same append-rejection
principle, but CCC is representation-agnostic while DCB is a tag-based event-store *contract* — and
**Event Sourcing requires no aggregates** in the first place, the aggregate-rebuild recipe being one
implementation the DDD community conflated with the definition. A through-line across Fritzsche, DCB, and
Goeleven: **build a decision's context from the relevant recorded events, not from a shared
aggregate/object model** — and that capability-owned, event-sourced unit is a natural **agent-ownership
boundary** ([[event-modeled-agent-design]]). [[adam-dymitruk]] supplies the blunt motive: AI was
"trained on dysfunction," so agents need a spec/scaffold to assemble best-practice systems
([[dymitruk-ai-trained-on-dysfunction-agents-are-a-must]]). Caveat: heavily practitioner/vendor
framing (Critter Stack, eventmodelers.ai, Fritzsche's own coinage) — strong convergence, light
independent evidence. The **capabilities × strategy** corner is now grounded on the [[simon-wardley]]
primary ([[wardley-maps-value-chains-and-evolution]], via [[chris-daniel]]): value chains start from the
user need; components evolve Genesis→Commodity; **invest/differentiate on the left, optimize/buy on the
right** — and Daniel's [[daniel-event-modeling-wardley-mapping|EM × Wardley]] sequence ("Wardley = where
to go and why; Event Modeling = what to build") joins [[wardley-mapping]] to [[business-capabilities]].
The flagged-important **business-capabilities** corner now also has an explicit **agent-era spine** (2026-07):
[[john-devadoss|deVadoss]]'s **CEAD** ([[devadoss-cead-capability-aligned-agent-design]]) makes *"capability
before agent"* the design rule — decompose a multi-agent system around durable business capabilities, and
carry each as an **Agent Capability Contract (ACC)**, framed as the agent-era descendant of the SOA/Homann
contracted black box (now bearing autonomy, memory, and verification), with the warning that ungoverned
**agent sprawl = a distributed monolith** (governance can't compensate for weak boundaries). [[matthew-skelton|Skelton]]
supplies the **organization-side mirror** ([[skelton-team-topologies-foundation-ai-roi]], grounded on the
2026 DORA ROI report): value-flow-aligned [[team-topologies|teams]] are the boundaries that make autonomous
agents effective, with **data-as-a-product** digestible for humans *and* agents. Together they close the loop
**capability → team → agent**, extending Homann → Goeleven → [[rico-fritzsche|Fritzsche]] from a code/ownership
pattern into the primary unit of *multi-agent architecture* itself.

A distinct **"design for agents / AI-readable code"** strand has now consolidated inside this thread:
the shared claim that **good boundaries and modularity are what make a codebase tractable, cheap, and
safe for AI agents to evolve**. [[vlad-khononov]] supplies the design-theory spine — his **Balanced
Coupling** model (coupling = strength × distance × volatility) and a two-part modularity test (*change
is localized* + *its effect is predictable*) framed as the thing AI depends on
([[khononov-golden-age-of-modularity]]) — and as of 2026-06-22 he has **shipped that thesis as a tool**:
a Claude Code plugin ([[khononov-modularity-claude-code-plugin|Modularity Skills]]) whose two skills
review a codebase for coupling imbalances and design modular architectures (self-reviewing until clean).
That makes the "design discipline → **agent harness skill**" pattern span *both* threads — the coupling
substrate (Khononov) and Event Modeling itself ([[jwilger-agent-skills-event-modeling]],
[[proophboard-skills-ai-agent-event-modeling]] on Thread 1 ↔ 5). [[adam-tornhill]] turns this into named principles for the
agentic age — **CLEAR** (Conceptual alignment, Local reasoning, Explicit intent, Avoid search luck,
Reduce the edit surface), explicitly contrasted with SOLID and aimed at limiting an agent's
*reconstruction work* / change blast-radius ([[tornhill-clear-design-principles-agentic-age]]). These
join [[jeremy-miller|Miller's]] "codebase is the prompt" and [[rico-fritzsche|Fritzsche's]]
functional-core/imperative-shell to converge with [[agent-legibility]] and [[locality-of-reference]] —
and they echo Dilger's "coupling, not context-window." This strand now has its first **peer-reviewed
empirical anchor**: [[borg-tornhill-code-for-machines-not-just-humans]] (Borg/Tornhill et al., FORGE
2026) measures that healthier code (CodeScene **CodeHealth ≥ 9**) is safer for an LLM to modify — a
**15–30% lower AI-refactoring break rate**, with CodeHealth a better predictor of correctness than
perplexity or SLOC — turning [[ai-readable-code]] from design intuition into a testable property and
giving [[agentic-coding]] a sensor-based reason to route AI work by code health. Tornhill then supplies
the strand's **theoretical floor** ([[tornhill-why-human-level-ai-wont-be-enough]], 2026-06-30): even
best-human-expert-level agents won't be enough, because AI *raises its own quality bar* via **scale**
(Lehman's laws; defects grow with code + change volume) and **speed** (faster generation → "wrong at
scale"), and the stochastic core makes rare errors recur across millions of decisions — so the answer is
not "superhuman code quality" (no training/feedback signal for it) but to **"create environments where
unreliable agents reliably produce acceptable outcomes."** This is the sharpest statement of the KB's
**environment-over-model** through-line, converging with [[dilger-harness-is-20-percent-requirements-are-80|Dilger's
"harness is 20%"]] and putting a *why* under both [[harness-engineering]]/[[loop-engineering]] and
AI-readable code. This strand now has a **first product application**: a 2026-06-22 deep-research note ([[coupling-research-note]]) asks what a **dependency-edge weight should mean** on a user-needs/capability map (a future "boundary-weighting" feature), and lands on Khononov's [[balanced-coupling|Balanced Coupling]] as the direct fit — exposing two *editor-judgment* dials, **Integration Strength** (4-level: intrusive→functional→model→contract) and **Volatility-coupling**, while treating **Distance** as a partition property rather than an edge weight. It situates Khononov against the wider [[coupling-taxonomy]] landscape ([[larry-constantine|Stevens/Myers/Constantine 1974]], change-coupling, [[team-topologies]] as partition-side constraints) and reframes [[conways-law]] as a *homomorphic force* — software-boundary weights are implicitly a model of team-coordination friction, which is why boundaries are interpretive. Research input, not a decision. On the concrete-grounding side, the substrate
finally has a **production reference**: [[atomicobject-cqrs-event-sourcing-production-walkthrough|Atomic
Object's]] no-toy-code [[event-sourcing]]/[[cqrs]] walkthrough (commands-as-intent, aggregate state
machines, snapshots, upcasters, idempotent projections, advisory locks) — whose "keep aggregates small,
solve cross-aggregate work with async projections" advice is the conventional counterpoint to the
[[dynamic-consistency-boundaries|DCB]] "kill the aggregate" line. **[[urs-enzler]]** then adds a **third
axis** to that debate ([[enzler-event-sourcing-aggregates-dcb-or-what]], 2026-06-23): the cheapest
consistency boundary is often **no concurrency at all** — "small data" + a task-based UI
(command-per-task, no unit-of-work), replacing a concurrent design with a non-concurrent one
(draft-intent + single-threaded batch), and serialising only where needed via infrastructure (Service
Bus sessions). DCB removes the boundary as a modeling commitment; the conventional view shrinks it;
Enzler removes the *concurrency* so it rarely binds — a pragmatic "you might not need it" that also
rhymes with [[fritzsche-ccc-atomic-append-serialized-write-order|Fritzsche's]] serialised-write-order
point one layer down. [[dilger-how-does-dcb-affect-event-modeling|Dilger]] then closes the loop from the
**modeling** side (2026-07-06): adopting DCB leaves Event Modeling untouched — if anything simpler. You
draw **one swimlane per bounded context** and swimlanes revert to showing **integration** between
systems/teams, not stream design; there is **no separate "Decision Model"** because the read-set a
command handler needs is exactly the **[[given-when-then|GWT]] GIVEN** clause, from which the Axon **Build
Kit** generates the handler's Criteria query + tests (tags treated as indices, added only before an agent
takes the slice). This answers the Munich-recap's recurring *"where does the logic / Decision Model go?"*
question and ties the DCB debate directly to the [[event-modeled-agent-design|model→GWT→generated-code]] seam.

A **late-July/August 2026 Fritzsche cluster** (surfaced via a live-Chrome sweep — his Ghost blog is
client-rendered, so the headless watch had been reporting it "evergreen") consolidates the substrate.
[[fritzsche-command-context-consistency-principle]] is now the KB's **canonical
[[command-context-consistency|CCC]] primary**, stating the store-agnostic rule the KB had been citing only
in fragments — *record a command's outcome only while the facts its decision read still hold* — and
resolving the aggregate/DCB debate cleanly: the aggregate is the **Static Consistency Boundary**, DCB is
CCC's **tag-based event-store form**, and a relational DB enforces the *same* principle with conditional
`UPDATE` + `FOR SHARE` + a `UNIQUE` constraint (a guard must **cover the context and never less**).
[[fritzsche-who-owns-a-rule-shared-across-domain-capabilities]] answers the standing objection to capability
autonomy — shared invariants (identity/money/compliance) don't force a central service layer if you name
the *kind* of knowledge (state-invariant@commit / external-fact@Provider / semantics@pure-type /
shared-policy@versioned-release+conformance-suite) and keep the **final decision with the owning capability**
("one policy, many local evaluators"). [[fritzsche-why-your-software-cannot-explain-business-decisions]] and
[[fritzsche-choosing-storage-is-choosing-what-your-system-forgets]] split the **method from the store**:
the explicit `command→context→decide→outcome` path (the RPU) is what makes a decision explainable, and
"append keeps facts, overwrite keeps state" — so [[event-sourcing]] is a *storage decision*, not
"thinking in events." And [[fritzsche-why-solid-is-outdated]] lands on the [[ai-readable-code]] strand with
its sharpest agent point: **agents reproduce SOLID's speculative structures unless the repo's design policy
says otherwise**, so SOLID (four of five principles have no failure signal) is the wrong default; North's
**CUPID** and "start the review with the change" replace it. On the EM×agents seam,
[[dilger-spec-driven-tools-need-event-modeling-front-half]] adds a fresh interop direction — Event Modeling
as the **front half** that feeds Spec-Driven toolkits (Spec-Kit/Spec-Kitty/Kiro) that otherwise "skip the
digging" (a planned `eventmodelers export --spec-kitty` bridge) — and [[dilger-real-cost-of-ai-is-second-order]]
gives [[comprehension-debt]] its worked field anecdote (a CTO's ~30% cost rise at flat headcount, hidden in
second-order costs), the cost-accounting face of the [[dora-roi-ai-assisted-software-development-2026|DORA]]
J-Curve.

## Open questions / next sources

- Has anyone applied **Event Modeling specifically** (not just event sourcing) to designing
  agent workflows? **Largely answered along a ladder:** [[adam-dymitruk]] asserts agents are
  users/processors in the model ([[dymitruk-event-modeling-future-proof-agents]]); [[prooph-board]]
  ships agents that *practise* EM ([[proophboard-skills-ai-agent-event-modeling]]); and [[john-wilger]]'s
  `agent-skills` ([[jwilger-agent-skills-event-modeling]]) makes the EM output the **contract that
  governs an autonomous coding factory** — the closest to a worked pipeline. See
  [[event-modeled-agent-design]]. *Still open, but narrower as of 2026-08-31:* a **worked event model
  artifact** of a multi-agent/harness system itself (jwilger consumes one but doesn't show it). Dilger's
  self-training modeling agent ([[dilger-one-million-tokens-self-training-modeling-agent]]) is the nearest
  thing yet and does **not** close it — it is a system that *produces* event models, not one that *is*
  one. What it does close is a different gap: the model as a **grading rubric** for agent output, via
  structural diff against a corpus of hand-crafted good models, which is the first mechanism the KB has
  for the long-asserted "a formal model makes agent output checkable" claim. Active focus area with a
  weekly research watch (see [[log]]).
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
  still missing. **Hunt result (2026-06-15):** a fresh search for a *worked Event Model of a multi-agent/
  harness system* still turned up nothing — the closest remain [[esaa-event-sourcing-for-autonomous-agents]]
  and [[confluent-agentic-event-driven-systems-architecture]] (event *sourcing/EDA*, both already
  ingested). An **in-house worked model now exists** (`outputs/worked-event-model-autonomous-coding-factory.md`,
  2026-06-15): an autonomous coding factory modeled end-to-end (7 slices, 6 agent processors on
  role/capability swimlanes, GWT contracts, guardian-veto subscriber, autonomy-ladder orchestrator,
  DCB-style append invariant). It closes the "no worked example at all" gap; an **independent,
  published** real-world one is still wanted.
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
- **Primaries behind the SDD critique (opened 2026-08-16 — 3 of 4 captured 2026-08-31, none yet
  ingested).** [[ng-spec-driven-development-is-waterfall-in-markdown]] brought the first numbers against
  spec-first agent workflows into the KB, all of them secondhand. Three of the four originals are now in
  `raw/`: **Eberhardt/Scott Logic**, *Putting Spec Kit Through Its Paces* (2025-11-26 — the ~10x figure,
  which turns out to be a self-reported impression on a hobby app, not a measurement on a production
  codebase); **Böckeler**, *Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl* (2025-10-15
  — sole-authored, not "Fowler/Böckeler", and the origin of the spec-first/spec-anchored/spec-as-source
  taxonomy the KB already uses); **Zaninotto/Marmelab**, *The Waterfall Strikes Back* (2025-11-12).
  **Still open:** a primary for **[[gojko-adzic]]** — his 2025-09-29 LinkedIn Pulse post is the earliest
  of the four and the only one from the BDD tradition, but LinkedIn was blocked on the 08-31 hunt; the KB
  still holds nothing of his despite leaning on [[given-when-then]] throughout.
  **The chronology finding matters more than the captures.** All three predate Ng by four to five months
  and each cites the one before it, so Ng is the downstream synthesis of an **Oct–Nov 2025 critique
  wave**, not its origin. Every page describing him as "the first outside-in critique" was corrected on
  2026-08-31, but [[spec-driven-development]] still needs rewriting *from* the primaries rather than from
  his summary of them.
- Original (still open): what domains will this KB ultimately cover? Event Modeling +
  agentic AI is the first real-content direction.
