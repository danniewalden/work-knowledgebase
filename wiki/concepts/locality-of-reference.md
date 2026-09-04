---
title: Locality of Reference (for coding agents)
type: concept
created: 2026-06-15
updated: 2026-06-17
sources: [miller-codebase-is-the-prompt-vertical-slices-ai, fritzsche-functional-core-imperative-shell-agentic-coding, tornhill-clear-design-principles-agentic-age]
tags: [agentic-coding, vertical-slice-architecture, agent-legibility, context-engineering, harness-engineering]
---

# Locality of Reference (for coding agents)

The principle, named by **[[jeremy-miller]]** ([[miller-codebase-is-the-prompt-vertical-slices-ai]]),
that **everything a feature needs should live in one place** so a coding agent loads only what's
relevant to the task. Borrowed from the hardware sense (data accessed together stored together),
applied to codebase organization in the agent era.

## Why it matters for agents

An agent has a finite context window and **pays — in tokens, latency, and accuracy — for every
irrelevant file it must load**. So *codebase structure is effectively part of the prompt*. Layered
(Clean/Hexagonal) architectures scatter one behavior across six or seven directories (controller →
request → handler → validator → repository interface + impl → mapping profiles), most of it irrelevant
to the change. Signal-to-noise collapses, and that's the condition under which agents **hallucinate** —
inventing abstractions, "fixing" impossible errors, drifting from intent. The architecture meant to
manage complexity ends up *manufacturing context pollution*.

The practitioner conclusion of the last year: **feature-organized, [[vertical-slice-architecture|vertical-slice]]
code is cheaper and safer for an agent than layer-organized code** — and *small* slices beat merely
co-located ones, because every artifact removed is one the agent can't fumble and every token saved is a
recurring cost cut.

## Where it sits

- The **architectural expression** of [[agent-legibility]] ("what the agent can't see in-context
  doesn't exist") and of [[context-engineering]] / countering [[context-rot]] — but achieved through
  *code layout* rather than docs or retrieval.
- The "why" under [[vertical-slice-architecture]]'s claim to be AI-friendly, and the link from VSA into
  the [[harness-engineering]] thread.
- The token-cost angle mirrors [[tornhill-codescene-unhealthy-code-agentic-token-cost]] (unhealthy code
  raises agent token spend) from the structure side rather than the code-health side.
- Named as design principles by [[adam-tornhill|Tornhill's]]
  [[tornhill-clear-design-principles-agentic-age|CLEAR]]: its **L — Local reasoning** is locality
  directly, and **R — Reduce the edit surface** is the same blast-radius goal; both frame locality as a
  lever on an agent's *reconstruction work*. See also [[ai-readable-code]].
- **Caveat (Miller):** locality alone isn't enough — the *implicit wiring* (conventions, generated glue)
  must still be encoded for the agent (skill files), or it reappears as guesswork.

## How to build it (Fritzsche, 2026-04-16 ingest)

[[fritzsche-functional-core-imperative-shell-agentic-coding|Fritzsche]] gives the concrete recipe for
*producing* locality: (1) the **repo shape instructs the agent before the prompt** — generic names
(`service`, `manager`, `repository`, `common/`, `shared/`) reproduce the old structure, so close those
escape routes; (2) shape the slice internally with **Functional Core / Imperative Shell** (pure
decision core + IO-only shell) and **behavior-describing file names** (`load_registration_context`,
`decide_registration`, `append_registration`); (3) **share nothing that carries domain meaning** and
keep **cross-feature dependencies exceptional**, so a slice can be "changed, regenerated, or replaced
from its own slice." Crucially he agrees with Miller's caveat: the conventions must be encoded as
**project-level skill files** ("the skill defines the generation environment") or the codebase drifts
back to OOP defaults. His practical replaceability test is the operational definition of locality.

_Sources: [[miller-codebase-is-the-prompt-vertical-slices-ai]] · [[fritzsche-functional-core-imperative-shell-agentic-coding]] · [[tornhill-clear-design-principles-agentic-age]]._
