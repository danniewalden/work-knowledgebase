---
title: "Birgitta Böckeler — Context Engineering for Coding Agents"
type: source
created: 2026-06-30
updated: 2026-06-30
sources: [bockeler-context-engineering-coding-agents]
raw_file: [raw/articles/bockeler-context-engineering-coding-agents.md]
tags: [context-engineering, harness-engineering, agentic-coding, claude-code, mcp, skills, focus]
---

# Birgitta Böckeler — Context Engineering for Coding Agents

Article by **[[birgitta-bockeler]]** ([[thoughtworks]]) in Martin Fowler's "Exploring Gen AI" series
(2026-02-05), captured verbatim. Source: `raw/articles/bockeler-context-engineering-coding-agents.md`.
The taxonomy primary underneath the KB's [[context-engineering]] concept — and the *predecessor* memo
to her [[fowler-bockeler-harness-engineering|harness-engineering]] piece (the article links forward to
it).

## Definition

Quoting colleague Bharani Subramaniam: **"Context engineering is curating what the model sees so that
you get a better result."** The number of options to configure a coding agent's context has exploded;
Claude Code is leading, others following.

## The taxonomy (what "context" is)

- **Reusable prompts** — markdown files, split by intent into **Instructions** ("do this") vs
  **Guidance** (aka rules/guardrails — "always follow this convention"). The two blend but the split
  is useful.
- **Context interfaces** — descriptions telling the LLM *how to fetch more context if it decides to*:
  **Tools** (bash, file search), **[[model-context-protocol|MCP]] servers**, and **Skills** (load-on-
  demand resources). Each one configured consumes context space, so choose strategically. **Files in
  the workspace** are the most basic, powerful interface — so how well your code serves as context
  (AI-friendly design, [[ai-readable-code]]) matters.

## Two organizing axes

- **Who decides to load it (if/when):** the **LLM** (e.g. Skills — prerequisite for unsupervised
  agents, but non-deterministic about *whether* it loads), the **Human** (e.g. slash commands —
  control at the cost of automation), or the **agent software** at deterministic lifecycle points
  (e.g. Claude Code hooks).
- **How much (size):** balance — not too little, not too much. Big context windows don't justify
  dumping; effectiveness drops and cost rises with too much context. Build rules files up **gradually**;
  transparency about what fills the window (e.g. a `/context` command) is a crucial tool feature; some
  tools also compact/optimise under the hood.

## The Claude-Code feature map (Jan 2026)

Classifies each feature on the axes above: **CLAUDE.md** (guidance, always loaded — cf. the
AGENTS.md standardization attempt), **Rules** (path-scoped guidance), **Slash commands** (human-
triggered instructions, *deprecated → Skills*), **Skills** (LLM/human, lazy-loaded), **Subagents**
(own context window, parallelisable, own model/tools), **MCP servers** (LLM-invoked API/tool access),
**Hooks** (deterministic lifecycle scripts), **Plugins** (distribution bundle). She expects Skills to
**absorb both slash commands and rules** as the "storming" phase converges.

## Two caveats worth keeping

- **Sharing is hard** — setups transfer well inside a team, poorly between internet strangers; resist
  overengineering copied context up front; low awareness of what's in your context leads to
  contradictory instructions and blaming the agent for following *your* rules.
- **Illusion of control** — "in spite of the name, this is not *really* engineering." Execution still
  depends on how the LLM interprets it; phrases like "ensure it does X" / "prevent hallucinations"
  overclaim — with LLMs you think in **probabilities** and pick the right level of human oversight.

## Why it matters here

The most structured primary for [[context-engineering]] — gives the concept its vocabulary
(instructions vs guidance; context interfaces; the if/when and how-much axes) and a concrete,
tool-grounded feature map. The Instructions-vs-Guidance split prefigures her harness-engineering
**guides vs sensors** ([[feedforward-and-feedback-controls]]); the "illusion of control" caveat is the
honest counterweight to vendor "ensure/prevent" language. Anchors the [[context-engineering]] →
[[harness-engineering]] lineage the KB treats as nested.

## Touches

[[birgitta-bockeler]] · [[thoughtworks]] · [[context-engineering]] · [[harness-engineering]] ·
[[feedforward-and-feedback-controls]] · [[model-context-protocol]] · [[agentic-coding]] ·
[[ai-readable-code]] · [[context-rot]] · [[claude-agent-sdk]]

_Source: `raw/articles/bockeler-context-engineering-coding-agents.md`._
