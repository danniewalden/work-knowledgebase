---
title: Jeremy Miller
type: entity
created: 2026-06-15
updated: 2026-09-04
sources: [miller-jasperfx-critterstack-ai-event-modeling-strategy, miller-codebase-is-the-prompt-vertical-slices-ai, miller-jasperfx-ai-skills-agent-skills, miller-ai-assisted-production-support-with-critterwatch, miller-pondering-continuous-integration-ai-world-order, miller-new-stuff-in-critter-stack-ai-skills-1-10, miller-open-core-model-sustainable-oss-dotnet]
tags: [person, dotnet, vertical-slice-architecture, event-sourcing, agentic-coding, harness-engineering, focus]
---

# Jeremy Miller

.NET OSS author and the lead behind **JasperFx** / the **[[critter-stack]]** (Wolverine + Marten);
blogs at *The Shade Tree Developer* (jeremydmiller.com). Long-time proponent of feature-oriented
("vertical slice") design in .NET; predecessor framework **FubuMVC** promoted the idea before VSA had
the name. On the KB watch list (blog + LinkedIn) for the event-sourcing / VSA substrate.

## Position — the codebase is part of the prompt

In *The Codebase Is the Prompt* ([[miller-codebase-is-the-prompt-vertical-slices-ai]]) Miller argues
that because an agent pays (tokens, latency, accuracy) for every irrelevant file it loads, codebase
**structure is effectively part of the prompt**, and [[vertical-slice-architecture]] is the
AI-friendliest organization ([[locality-of-reference]]). He positions **Wolverine** as "VSA compressed
as far as the language allows" — convention-discovered handlers, method injection, `[Transactional]`
outbox, cascading-message returns, Marten `[AggregateHandler]` event sourcing — so the slice is "the
decision and nothing else." Crucial honest caveat: compression *shifts* the wiring knowledge into the
agent's guesswork unless conventions are encoded as **AI skill files** ("the skills are the
constitution; the slices are the code") — i.e. [[harness-engineering]] guides.

## Position — vendor-maintained agent skills (2026-07-10)

Miller turns "the codebase is the prompt" into a shipping product with **JasperFx AI Skills**
([[miller-jasperfx-ai-skills-agent-skills]]): a curated library of **81 agent skills** for the
[[critter-stack]] (Marten/Wolverine/Polecat/CritterWatch), "written and maintained by the people who
build these tools," so an agent "**stops guessing from stale training data**" and works from docs
"verified against the actual source code, current as of this month." The design is pure
[[agent-legibility]]: task-shaped, example-heavy, error messages captured **verbatim** from source, and
**self-contained** (a skill that shows a helper embeds its full source — no hunting for a NuGet that
doesn't exist). He frames upkeep as a small hill-climbing loop ("skill told me something stale → fixed,
verified against source, released"). A concrete instance of the **Skills primitive** in
[[loop-engineering]] / [[harness-engineering]] on the event-sourcing substrate. (Vendor context: a paid
product he sells.)

## In the KB

A concrete .NET counterpart to [[jimmy-bogard]]'s VSA origin and to
[[rico-fritzsche-autonomous-domain-capabilities-ccc|Fritzsche's]] capability-locality argument; bridges
[[vertical-slice-architecture]] to [[agent-legibility]] / [[context-engineering]]. Also the source for
the **Marten 9.0 DCB** implementation noted on [[dynamic-consistency-boundaries]]. Caveat: the post is
partly a [[critter-stack]] sales pitch (it advertises paid Critter Stack AI Skills).

## Where he appears

- [[miller-codebase-is-the-prompt-vertical-slices-ai]] — The Codebase Is the Prompt (2026-06-04).
- [[miller-jasperfx-ai-skills-agent-skills]] — JasperFx AI Skills 1.6.0 (2026-07-10).
- [[miller-open-core-model-sustainable-oss-dotnet]] — the open-core model; you cannot vibe-code the production beatings (2026-08-28).
- [[miller-pondering-continuous-integration-ai-world-order]] — CI under agent load (2026-08-31).
- [[miller-new-stuff-in-critter-stack-ai-skills-1-10]] — AI Skills 1.10.0, 102 skills (2026-09-02).
- [[miller-ai-assisted-production-support-with-critterwatch]] — an agent handed a production control surface via MCP (2026-09).

## Where he stands on Event Modeling (2026-08-21)

His full AI strategy post ([[miller-jasperfx-critterstack-ai-event-modeling-strategy]]) makes him the KB's **Model-as-Code**
pole — see [[model-as-code-vs-model-as-language]]. The position and its lineage, in his words:

> "I've long been very dubious about the efficacy of 'low code' visual modeling approaches or application
> generators like JHipster. I'm also not enthusiastic about any of the intermediate DSL approaches I'm
> seeing for modeling event driven architectures using YAML, XML, or custom built textual DSLs… better
> off just adding the visualization capabilities on top of the code."

Read carefully, this is an **economic and track-record argument, not a philosophical one** — the
authoring surface is expensive and has disappointed before — which makes it falsifiable in principle and
unfalsified in practice, since he offers no comparison. Meanwhile he is landing Event Modeling *into* the
Critter Stack (fluent API in `JasperFx.Events`, Bobcat slice visualization, `dotnet watch` live model
editing, CLI export of slices for agents), with the code authoritative: "have the specified model
overridden when real code is built in the system."

His alternative to diagramming rules is to **go straight to BDD specs that become actionable specs** —
which keeps [[given-when-then]] as the hand-authored unit while inferring the structure. Characteristic
hedging throughout: the whole strategy is "spaghetti against the wall," Bobcat is "pretty mushy as far as
details," and on the VSA token claim, "it's incumbent upon people like me to prove that out over time."

## Position — the *running fleet* is the prompt (2026-09)

The runtime counterpart to "the codebase is the prompt." In
[[miller-ai-assisted-production-support-with-critterwatch]] he hands an agent a **production control
surface** over an event-sourced .NET fleet through MCP and works four scenarios end to end. Two positions
worth attributing to him, both stated as internal rules:

- **"A pile of tools doesn't make an agent good at operations — an agent also needs to know the
  discipline."** Hence: *"any time CritterWatch exposes new information through an MCP tool, the paired
  skill work ships with it. A tool with no skill coverage is an under-leveraged tool."* The skill teaches
  the *loop* (summarize → query → act), not the tool list. See [[harness-engineering]].
- **Tools should refuse to report an ambiguous result as an answer** — the `databasesAnnounced` /
  `databasesAnswered` / `partial` contract, and the skill rule *"never answer 'the queue is empty'"* on a
  partial read, which exists because a console once *"rendered 'no dead letters found' over a queue quietly
  holding 42 of them."*

He is also candid about the discomfort — *"Handing an AI agent a control surface for production… makes me a
little nervous, and we built it"* — and about the demo's own failure (his alerting was wrong about his own
fleet mid-post; a Postgres deadlock storm plus a Docker restart, fixed for 1.1). **Markers: VENDOR
SELF-REPORT throughout — his company, his paid product, his fleet, failures he injected himself, nothing
measured.** Catalogue count is now **102 skills** (2026-09-02,
[[miller-new-stuff-in-critter-stack-ai-skills-1-10]]), superseding the 81 recorded above.

## Position — CI is the same practice under new load (2026-08-31)

[[miller-pondering-continuous-integration-ai-world-order]]: CI's purpose is unchanged, but *"with the
extreme load that's come from all of us yahoos using AI agents to code so much faster, GitHub Actions are
very noticeably slower or flat out unreliable on the worst days."* His response is local-first
verification — *"doing trunk based development like it's 2007 and Subversion is the latest hotness!"* —
selective test subsets chosen by changes in flight, a full **"HeavyGate"** only on pushes to `main`, PRs
kept *"in no small part just for traceability"* rather than review, and a **supervisor** ("Bobcat", on the
Microsoft Testing Platform) doing selective retries, process restarts and hard Docker resets on known
flakes. A second-order effect he reports: slow CI **forced flake elimination**, because retry stopped being
cheap. **IMPRESSION NOT MEASUREMENT — no wait times, no before/after, and he concedes his team also added
far more tests, which is an unresolved confound.** [[martin-fowler]] answers the same Paul Stack post and
reaches the same remedy from the opposite premise (*"that was always how Continuous Integration works"*) —
see [[fowler-fragments-2026-09-01]] and [[feedforward-and-feedback-controls]]. **The KB holds that
disagreement open and does not resolve it in either direction:** Fowler says the practice always
prescribed local verification and the CI *server* was never the practice; Miller presents it as reverting
to 2007. Paul Stack's own post is not in `raw/`, so the KB holds two rebuttals and not the primary.

## Position — you cannot vibe-code the production beatings (2026-08-28)

[[miller-open-core-model-sustainable-oss-dotnet]], mostly an OSS-licensing post, carries one argument with
reach: LLMs change the cost of *producing* code, not the cost of the years of adaptation that hardened it —
*"these kinds of tools achieve deep quality through a lot of usage, feedback, and adaptation over time."*
His examples are the irregularities (broker connections dropping, PostgreSQL kill signals creating sequence
gaps, Kubernetes doing Kubernetes things) plus a live one: subsystems he thought were "done" needed fixes
last month *"because new users in new circumstances proved otherwise."* **Maximally interested** — it is
also an argument for buying his support plans — and the direct counterweight to
[[dudycz-fork-can-you-own-it]]'s "LLM as a fork."

_Source pages: [[miller-codebase-is-the-prompt-vertical-slices-ai]] ·
[[miller-jasperfx-ai-skills-agent-skills]] · [[miller-jasperfx-critterstack-ai-event-modeling-strategy]] ·
[[miller-ai-assisted-production-support-with-critterwatch]] ·
[[miller-pondering-continuous-integration-ai-world-order]] ·
[[miller-new-stuff-in-critter-stack-ai-skills-1-10]] ·
[[miller-open-core-model-sustainable-oss-dotnet]]._
