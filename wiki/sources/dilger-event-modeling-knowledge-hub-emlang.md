---
title: "Martin Dilger — Event Modeling as a knowledge hub; EmLang support"
type: source
created: 2026-06-21
updated: 2026-06-21
sources: [dilger-event-modeling-knowledge-hub-emlang]
raw_file: [raw/notes/dilger-event-modeling-knowledge-hub-emlang-support.md]
tags: [event-modeling, knowledge-management, agentic-ai, spec-driven-development, tool, focus]
---

# Martin Dilger — Event Modeling as a knowledge hub; EmLang support

LinkedIn post by **[[martin-dilger]]** (~2026-06-20; captured 2026-06-21 via logged-in Chrome).
Source file: `raw/notes/dilger-event-modeling-knowledge-hub-emlang-support.md`. On the EM × agents
focus ([[event-modeled-agent-design]]); tooling/vision.

## What it says

- **The problem isn't ignorance, it's scatter.** "It's not that we don't know what our systems should be
  doing" — that knowledge is fragmented across tickets, Confluence, code, Slack threads, and people's
  heads, "inaccessible unless you already know where to look."
- **Event Modeling as a *knowledge hub*, not "modeled software."** Dilger reframes EM as the single place
  to go to understand how a system actually works — "simple language, simple terms, simple patterns" — and
  then, once captured, that model becomes **the blueprint for implementation, for humans and for agents
  alike.** (Note the resonance with this KB's own premise: a single accessible compiled store of system
  knowledge.)
- **Format-agnostic, access-first.** He explicitly doesn't care *how* the model is authored — directly on
  [[eventmodelers-ai|the platform]], local YAML imported later, JSON, Markdown, or **an agent adding
  knowledge via [[model-context-protocol|MCP]]**. "The format isn't the point. Access is."
- **Concrete change: EmLang support.** He added **EmLang** — a YAML dialect for describing systems — as an
  import format to the platform. He doesn't endorse every EmLang choice but calls it "a solid starting
  point" engineers like for its simplicity, so he's opening the platform to it: you can import EmLang
  models and make them accessible to anyone.

## Why it matters here

Two threads. (1) **EM-as-knowledge-base** generalizes Dilger's "model is the source of truth"
([[dilger-is-code-still-the-source-of-truth]]) from a spec-for-build into a durable, queryable *system of
record* for how a system works — a model-as-living-documentation that both humans and agents read. (2)
**Format pluralism + MCP ingestion** is a small but real interoperability move: a YAML dialect (EmLang)
and agent-written models via MCP make [[eventmodelers-ai]] a hub other tools/agents feed, echoing the
[[prooph-board]]/[[fraktalio-event-modeler-connect-ai-agents-mcp|Fraktalio]] "agents author the model via
MCP" pattern. Reinforces [[spec-driven-development]] and [[event-modeled-agent-design]].

## Caveats

Vendor self-report for [[eventmodelers-ai]]. "EmLang" is referenced without a captured spec/provenance
(an external YAML dialect Dilger is adopting, not defining) — worth a follow-up capture if it recurs. The
"knowledge hub" framing is aspirational vision, not a shipped, reviewed feature set.

## Touches

[[martin-dilger]] · [[eventmodelers-ai]] · [[event-modeling]] · [[spec-driven-development]] ·
[[model-context-protocol]] · [[event-modeled-agent-design]] · [[prooph-board]]

_Source: `raw/notes/dilger-event-modeling-knowledge-hub-emlang-support.md`._
