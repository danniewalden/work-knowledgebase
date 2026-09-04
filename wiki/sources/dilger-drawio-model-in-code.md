---
title: "Martin Dilger — Are you using Draw.io for Event Modeling? (model-in-code needs a framework + MCP guardrails)"
type: source
created: 2026-06-30
updated: 2026-06-30
sources: [dilger-drawio-model-in-code]
raw_file: [raw/notes/dilger-drawio-event-modeling-model-in-code.md]
tags: [event-modeling, model-in-code, mcp, ai-readable-code, agentic-coding, focus]
---

# Martin Dilger — Are you using Draw.io for Event Modeling? (model-in-code needs a framework + MCP guardrails)

LinkedIn post by **[[martin-dilger]]** (2026-06-30; captured same day via logged-in Chrome).
Source file: `raw/notes/dilger-drawio-event-modeling-model-in-code.md`. On the EM × agents focus — the
argument for *why raw diagram XML fails the agent case*.

## What it argues

Dilger observes that clients keep their [[event-modeling]] model as **draw.io XML in the repo and use AI to
manipulate it directly**, and he **agrees with the instinct** — *"We need the model in the code" — and I
fully agree.* Draw.io is free, serializes to XML, and lets you keep the model in git, "where it belongs most
of the time." But working from raw draw.io has drawbacks — and the key ones are about the **agent**:

- **Non-technicians can't contribute** directly to raw XML.
- **AI has no framework to follow, no rules — so it's easy to make mistakes.** (The load-bearing point:
  an agent editing an unconstrained diagram format has nothing to validate against.)
- **The XML isn't human-readable** — you need the web/desktop viewer, which "creates friction."
- **Collaboration is harder** — "what's not committed doesn't exist."

His recommended path on the [[eventmodelers-ai|Eventmodelers Platform]] (which "fully supports that model —
I use it myself like this"): edit the model → **export to a standardized JSON format** → **version it in
git** → use a **local agent to manipulate the JSON** (they provide [[claude-agent-sdk|skills]] for this) →
**but also leverage the [[model-context-protocol|MCP]] to validate changes before commit**. The MCP is the
missing framework: it *"gives the agent guardrails and feedback and prevents costly mistakes… the agent will
just self-correct."* The JSON can then be visualized in the platform's **Model-Viewer** (accessible to
anyone), and the same model **supports code generation / AI-assisted development via Build-Kits (Node, Java,
Kotlin)** ([[dilger-build-kits-model-to-generated-code]]).

He closes with his recurring framing — book / training / conference / now "enterprise-grade tooling" — "the
[thing] I wish I had when I started," making EM + [[event-sourcing]] + AI-assisted development accessible.

## Why it matters here

This is the cleanest statement of a specific claim in the [[ai-readable-code]] / [[agent-legibility]] thread
applied to the **spec/model layer**: a model that lives in code is necessary but **not sufficient for an
agent** — the agent needs a *framework* (schema + validation) so its edits are checkable, and an
[[model-context-protocol|MCP]] provides that validate-before-commit feedback loop so it self-corrects. It's
the model-side analogue of [[tornhill-cannot-trust-agent-codescene-mcp|Tornhill's "you can't trust the agent
to self-assess — use a deterministic external sensor"]]: raw draw.io XML is the unguarded environment; the
standardized JSON + MCP is the guarded one. It also sharpens [[spec-driven-development]] — "the spec is the
work" only holds if the agent can't silently corrupt the spec — and echoes his
[[dilger-planning-like-excel-legible-to-human-and-ai|"legible to a human and an AI at once"]] and
[[dilger-keep-command-handlers-pure|"a written skill is necessary but not sufficient — guardrails must be
enforced"]] positions.

## Caveats

Vendor post positioning his own platform against a free incumbent (draw.io); the guardrail/self-correction
claims are self-report with no captured demo or accuracy measure.

## Touches

[[martin-dilger]] · [[event-modeling]] · [[eventmodelers-ai]] · [[model-context-protocol]] ·
[[ai-readable-code]] · [[agent-legibility]] · [[spec-driven-development]] · [[claude-agent-sdk]] ·
[[event-sourcing]] · [[event-modeled-agent-design]] · [[dilger-build-kits-model-to-generated-code]] ·
[[dilger-keep-command-handlers-pure]] · [[tornhill-cannot-trust-agent-codescene-mcp]]

_Source: `raw/notes/dilger-drawio-event-modeling-model-in-code.md`._
