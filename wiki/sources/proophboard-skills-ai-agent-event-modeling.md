---
title: "prooph board — AI Agent Skills (proophboard/skills)"
type: source
created: 2026-06-12
updated: 2026-06-12
sources: [proophboard-skills-ai-agent-event-modeling]
raw_file: [raw/articles/proophboard-skills-ai-agent-event-modeling.md]
tags: [event-modeling, agentic-ai, mcp, skills, tooling, focus]
---

# prooph board — AI Agent Skills (proophboard/skills)

GitHub repository by **prooph board**, latest release 5 Jun 2026 (small/new: ~3 stars, 51
commits). The most direct artifact yet of the KB's focus area — **AI agents that *do*
[[event-modeling]]**, not just event sourcing. Raw capture:
`raw/articles/proophboard-skills-ai-agent-event-modeling.md`.

## What it is

A set of installable **agent skill packages** for coding agents (Cursor, Claude Code, Aider, etc.)
that connect to the **prooph board [[model-context-protocol|MCP]] server**. The skills teach an
agent how to correctly create and work with prooph board's Event Modeling elements. prooph board
is an online Event Modeling tool (the visual-modeling counterpart to [[qlerify]] in the KB).

## Key points

- **Skill catalog** at skills.prooph-board.com, in two families: **Event Modeling skills** (core
  modeling guidelines, element descriptions, slice scenarios) and **Cody Engine skills** (technical
  specs for Command, Event, Information, Automation, and UI elements → code generation).
- **Architecture**: skill = `SKILL.md` (instructions) + `skill.json` (metadata) — the same skills
  pattern used by Claude Code/Codex. The MCP server is the agent↔tool channel; skills are the
  domain knowledge that makes the agent model *correctly*.
- **Tagged** `ai-agents`, `event-modeling`, `ai-tools`, `spec-driven-development` — positioning
  Event Modeling as a spec-driven-development substrate for agents.
- Community contribution model (PRs earn a free workspace seat); requested skill ideas include
  model→code generation, legacy-codebase analysis documented as prooph board chapters, and
  ticketing-system sync (Jira/Linear/GitHub Issues).

## Why it matters here

This is a **concrete, shipping** instance of [[event-modeled-agent-design]]: rather than an agent
being *modeled as* a user/processor on a timeline (Dymitruk's claim), here the agent is a
*practitioner* of Event Modeling, with the MCP server + skills as its harness. It maps cleanly onto
the KB's construct table — the Cody Engine "Automation" element is exactly the [[event-modeling]]
Automation pattern, and the element-spec skills are the Given-When-Then contracts. Still **not** a
worked event model of a multi-agent/harness system (the standing gap), but it's the closest tooling
evidence that the agents × Event Modeling intersection is being built in practice.

## Links

Entities: [[prooph-board]]. Concepts: [[event-modeling]], [[event-modeled-agent-design]],
[[model-context-protocol]], [[agentic-coding]], [[claude-agent-sdk]], [[agentic-ai]].
Related: [[qlerify-event-modeling-tool-ai]], [[dymitruk-event-modeling-future-proof-agents]],
[[jwilger-agent-skills-event-modeling]] (sibling artifact — uses the same SKILL.md pattern, but for
agents to *practise* and *build against* an event model rather than draw one on prooph board).
