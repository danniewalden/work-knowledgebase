---
title: "Jeremy Miller — The Codebase Is the Prompt: Wolverine, Vertical Slices, and AI-Assisted Development"
type: source
created: 2026-06-15
updated: 2026-06-15
sources: [miller-codebase-is-the-prompt-vertical-slices-ai]
raw_file: [raw/articles/miller-codebase-is-the-prompt-vertical-slices-ai.md]
tags: [vertical-slice-architecture, agentic-coding, agent-legibility, context-engineering, harness-engineering, cqrs, focus]
---

# Jeremy Miller — The Codebase Is the Prompt

Blog post by **[[jeremy-miller]]** on *The Shade Tree Developer* (2026-06-04).
Source file: `raw/articles/miller-codebase-is-the-prompt-vertical-slices-ai.md`. Partly a
"strategery" pitch for the **[[critter-stack]]** (Wolverine + Marten), so read the vendor angle in.

## Core thesis — the codebase structure *is* part of the prompt

An agent has a finite context window and **pays — in tokens, latency, and accuracy — for every
irrelevant file it must load** to understand one feature. So the structure of the codebase is now
effectively part of the prompt, and the architecture easiest for an agent to reason about is
**[[vertical-slice-architecture|vertical slices]]**.

- **Why layered architectures fight the agent.** To change one behavior in a canonical Clean/Hexagonal
  solution, the agent must find the controller, request, handler, validator, repository interface +
  implementation, and mapping profiles — six or seven directories, most of it irrelevant. Signal-to-
  noise in the context window collapses, and *that's* the condition under which agents hallucinate:
  inventing abstractions, "fixing" impossible error cases, drifting from intent. "The architecture that
  was supposed to manage complexity ends up manufacturing context pollution." This is **[[locality-of-reference]]**:
  keep everything a feature needs in one place so the agent loads only what's relevant.
- **Co-located is good; *small* is better.** Plain VSA (à la **[[jimmy-bogard]]** + MediatR) still
  carries ceremony — request record, `IRequest<T>` marker, handler class, constructor injection,
  explicit `SaveChangesAsync`, a separate publish call, `Program.cs` registration, validation pipeline
  behavior. Co-located but not small; the agent must still read all of it.

## Wolverine as "VSA compressed as far as the language allows"

Miller's worked comparison strips a "create shipment" slice to almost pure business decision:
handlers discovered **by convention** (no marker interfaces), dependencies via **method injection**
(no constructor/fields), `[Transactional]` lets Wolverine + Marten manage the unit of work and use the
document session as a **transactional outbox**, and **returning an event value *is* publishing it** (a
cascading message). With `Wolverine.Http` the endpoint *is* the handler; with Marten event sourcing the
`[AggregateHandler]` collapses load-decide-append-save into one method that receives current aggregate
state and returns events. "The slice is the decision and nothing else."

## Why compression is the feature for AI

Three compounding reasons: (1) **the whole slice fits in context**, so the agent never reconstructs a
flow from fragments (the hallucination trigger); (2) **less surface to get wrong** — every artifact
removed is one the agent can't fumble (a cascading return can't be forgotten like a hand-written
`Publish` call); (3) **cheaper to operate** — fewer tokens per task is a recurring cost cut every time
*any* agent touches the code (echoes the [[tornhill-codescene-unhealthy-code-agentic-token-cost|code-health → token-cost]] argument from the other direction).

## The honest caveat — compression shifts the burden, it doesn't delete it

When every part is small and stateless, the knowledge of *how the parts wire together* (discovery
conventions, what a cascading return does, what middleware runs) doesn't vanish — it shifts. If it
shifts into the agent's context as **guesswork**, you've traded one problem for another. Miller's
answer: **conventions plus documented context**, encoded as **AI skill files** — "the skills are the
constitution; the slices are the code." Compressed code *without* encoded conventions is just terse
code. (Also: tell the agent not to hand-edit framework-generated glue; and resist regrowing a shared
"services" layer the moment two slices rhyme — the classic VSA duplication critique still applies.)

## Why it matters here

The most worked, code-level treatment in the KB of **VSA as the AI substrate**, and a clean bridge
between [[vertical-slice-architecture]] and the harness thread: locality-of-reference is
[[agent-legibility]] and [[context-engineering]] expressed as *code organization*, and "skills as the
constitution" is exactly [[harness-engineering]]'s guides. Note Wolverine/Marten = **[[critter-stack]]**,
whose **Marten 9.0** is also the DCB implementation referenced on [[dynamic-consistency-boundaries]].

## Touches

[[jeremy-miller]] · [[critter-stack]] · [[vertical-slice-architecture]] · [[locality-of-reference]] ·
[[agent-legibility]] · [[context-engineering]] · [[context-rot]] · [[harness-engineering]] ·
[[agentic-coding]] · [[cqrs]] · [[event-sourcing]] · [[jimmy-bogard]]

_Source: `raw/articles/miller-codebase-is-the-prompt-vertical-slices-ai.md`._
