---
title: Jeremy Miller
type: entity
created: 2026-06-15
updated: 2026-08-31
sources: [miller-jasperfx-critterstack-ai-event-modeling-strategy, miller-codebase-is-the-prompt-vertical-slices-ai, miller-jasperfx-ai-skills-agent-skills]
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

_Source pages: [[miller-codebase-is-the-prompt-vertical-slices-ai]] · [[miller-jasperfx-ai-skills-agent-skills]] · [[miller-jasperfx-critterstack-ai-event-modeling-strategy]]._
