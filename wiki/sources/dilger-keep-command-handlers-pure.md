---
title: "Dilger — Keep your Command Handlers pure (not even Claude understands this)"
type: source
created: 2026-06-13
updated: 2026-06-13
sources: [dilger-keep-command-handlers-pure]
raw_file: [raw/articles/dilger-keep-command-handlers-pure.md]
tags: [event-modeling, agentic-coding, cqrs, guardrails, skills, command-handler, focus]
---

# Dilger — Keep your Command Handlers pure (not even Claude understands this)

LinkedIn post by **[[martin-dilger]]** (2026-06-10, edited). A concrete **Claude Code** anecdote that
doubles as an argument for why [[event-modeling]] and architectural guardrails matter when an agent
writes the code. Raw capture: `raw/articles/dilger-keep-command-handlers-pure.md`.

## The anecdote

Assigned a vertical slice, Claude Code wanted to put a business rule (users can own only one
organization) into the **routing layer** (`routes.ts`) and write a route/integration test for it —
**ignoring the Event Model and the Given-When-Then scenarios**. Dilger's read:

- **"LLMs don't understand architecture. They recognize patterns."** If your architecture allows
  logic in five places, the agent will put it in any of them — "sometimes they'll even invent a
  sixth."
- Letting the rule live in routing means you suddenly *need* route tests, which Claude would happily
  generate — **"treating the symptom, not the cause."** The decision never belonged there.
- The skill *said* to keep handlers pure ("It's literally stated in the Skill. You did read it, did
  you?") — i.e. a written [[claude-agent-sdk|skill]] is necessary but **not sufficient**; the agent
  still drifted, so guardrails must be enforced, not just documented.

## The rule (his prescription)

Keep **Command Handlers pure**: business decisions in one place, explicit inputs, deterministic
outcomes — understandable, readable, testable. The routing/transport layer's only job is to *collect
data*; pass everything the decision needs through the **command** ("the command is your DTO"). Push
every business decision into the handler, keep controllers/routes/transports dumb, and **make that
one place visible in your Event Model**. (He notes a latent concurrency issue this leaves, unaddressed
in the post.)

## Why it matters

The most concrete in-KB evidence of an agent **drifting off the event model** and the guardrail
response. It puts teeth on [[event-modeled-agent-design]]: the model isn't just upstream alignment, it
defines *where logic is allowed to live*, and the harness must enforce that. Connects [[cqrs]] /
command-handler purity to [[agentic-coding]] guardrails, [[agent-legibility]] (the model as the map
the agent must respect), and the skills-as-contract idea from [[jwilger-agent-skills-event-modeling]].

## Caveats

A single anecdote, one developer, no repo link; the concurrency caveat he flags is left open.

## Links

Entities: [[martin-dilger]], [[anthropic]]. Concepts: [[event-modeling]], [[cqrs]],
[[event-modeled-agent-design]], [[agentic-coding]], [[agent-legibility]], [[claude-agent-sdk]],
[[domain-driven-design]].
Related sources: [[dilger-spec-driven-development-applied]],
[[dilger-faros-ai-report-amplifies-unclear-requirements]], [[jwilger-agent-skills-event-modeling]],
[[proophboard-skills-ai-agent-event-modeling]].
