---
title: "Dilger — The model is a living spec (the always-on agent)"
type: source
created: 2026-06-14
updated: 2026-06-14
sources: [dilger-model-is-a-living-spec-always-on-agent]
raw_file: [raw/articles/dilger-model-is-a-living-spec-always-on-agent.md]
tags: [event-modeling, agentic-coding, spec-driven-development, harness, long-running-agents, unattended-agents, focus]
---

# Dilger — The model is a living spec (the always-on agent)

LinkedIn post by **[[martin-dilger]]** (2026-06-14, ~12h before capture). The most concrete
operational picture yet of his [[spec-driven-development]] workflow: an Event Model that an agent
treats as a **continuously executing** spec rather than a hand-off artifact. Raw capture:
`raw/articles/dilger-model-is-a-living-spec-always-on-agent.md`.

## Key points

- **The origin anecdote.** After a workshop, everyone logged off and Dilger stayed to tidy the model —
  moved blocks, adjusted slices. He then noticed a background agent (left running "in a loop —
  standard setup for us at this point") had *never stopped*: it was picking up every board change in
  real time and building against it, with no prompt and without him remembering it was there.
- **The reframe: no hand-off.** He had thought of AI-assisted dev as a **relay race** — "model first,
  then hand it off, then wait. A sequence … with a clear baton pass." What he saw was "one continuous
  flow": no break between human modeling and machine building. "What if you could **speak your system
  into existence** — someone models as you talk, and something else builds as you model?"
- **The 24/7 pipeline.** His current setup: place a **Slice** in `planned`, and an agent will (1)
  **generate the tests from the spec — the harness**, (2) implement using the red tests as guidelines,
  (3) create a branch, (4) open a PR or merge. "No handover. No friction. No waiting." It can go
  further: a **modeling agent** models and puts slices to `planned`, a **builder agent** takes over —
  "Full autopilot. From spoken idea to running code, without a single person touching an IDE."
- **The thesis line.** "The spec isn't a stepping stone to the code anymore. **The spec is the work.
  Everything else follows.**"
- Closes with a workshop promo (next week; includes a 6-month [[eventmodelers-ai]] license).

## Why it matters

This is the **operational** complement to [[dilger-spec-driven-development-applied]] (the *why*). It
upgrades the Dilger thread from "design the environment" framing to a described mechanism: the Event
Model as a live spec that drives a [[long-running-agents|long-running]], effectively
[[unattended-coding-agents|unattended]] build loop — slice→tests-as-harness→implement→PR. The
slice→"generate tests from the spec (the harness)"→"implement against red tests" sequence is
[[event-modeled-agent-design]]'s Given-When-Then-as-acceptance-gate claim stated as a daily workflow,
and it matches [[jwilger-agent-skills-event-modeling]]'s factory pipeline from the practitioner side.
The "modeling agent → builder agent" split is a concrete instance of agents as **users/processors**
composed on one timeline ([[dymitruk-event-modeling-future-proof-agents]]).

## Caveats

LinkedIn marketing for a workshop and platform; assertion-level, no metrics, no repo. "Standard setup
for us" and "agents running 24/7" are self-report. The always-on loop also raises an unaddressed
[[dilger-keep-command-handlers-pure|drift/enforcement]] question the post doesn't touch.

## Links

Entities: [[martin-dilger]], [[eventmodelers-ai]]. Concepts: [[spec-driven-development]],
[[event-modeling]], [[event-modeled-agent-design]], [[agentic-coding]], [[long-running-agents]],
[[unattended-coding-agents]], [[agent-harness]], [[ralph-loop]], [[feedforward-and-feedback-controls]].
Related sources: [[dilger-spec-driven-development-applied]], [[dilger-keep-command-handlers-pure]],
[[jwilger-agent-skills-event-modeling]], [[fraktalio-event-modeler-connect-ai-agents-mcp]],
[[stripe-minions-one-shot-coding-agents]], [[anthropic-effective-harnesses-long-running-agents]].
