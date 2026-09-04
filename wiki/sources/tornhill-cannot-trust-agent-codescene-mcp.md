---
title: "Adam Tornhill — You Cannot Trust Your Coding Agent to Produce Maintainable Code (CodeScene MCP)"
type: source
created: 2026-06-29
updated: 2026-06-29
sources: [tornhill-cannot-trust-agent-codescene-mcp]
raw_file: [raw/notes/tornhill-cannot-trust-agent-maintainable-code-codescene-mcp.md]
tags: [ai-readable-code, harness-engineering, agent-legibility, agentic-coding, code-health, focus]
---

# Adam Tornhill — You Cannot Trust Your Coding Agent to Produce Maintainable Code

LinkedIn post by **[[adam-tornhill]]** (2026-06-22), captured verbatim from a live session. Source:
`raw/notes/tornhill-cannot-trust-agent-maintainable-code-codescene-mcp.md`.

## The argument

"You just cannot trust your coding agent to produce maintainable or even machine-legible code." Told to
fix a specific code-health issue in already-poor code, his agent produced "a software design disaster
where one problem was traded for an even worse one." Three reasons asking an agent to "follow SOLID,"
"write clean code," or have *another LLM* review it doesn't work — "you'd spend a ton of tokens and
still get the same subpar code":

- **LLMs are non-deterministic** — "code quality is too important to leave to chance."
- **An LLM has no reliable way of assessing code health.**
- **The existing code is a large part of the context** — so agents perform *worst exactly where they're
  needed most*: in complex, unstructured code.

## The fix — a deterministic external sensor

"This problem is already solved." Tornhill uses **deterministic Code Health feedback through the
CodeScene MCP** in his coding workflow, **"giving the agent an external source of truth rather than
asking it to judge its own output."** He warns of companies "on the highway to legacy code": code-health
sins accumulate into a downward spiral where neither human nor agent can evolve the code. He has coded
**100% agentically for nine months** and finds this "strikingly obvious the moment you do anything
beyond a toy project."

## Why it matters here

The sharpest practitioner statement of the **code-health-as-harness-sensor** pattern, and the
behavioral punchline under the peer-reviewed [[borg-tornhill-code-for-machines-not-just-humans]]
finding. The move — *a deterministic ([[feedforward-and-feedback-controls|computational]]) sensor as the
agent's external source of truth, because an inferential/LLM self-review can't be trusted on code
health* — is a concrete [[harness-engineering]] guide-and-sensor instance ([[model-context-protocol|MCP]]
as the delivery), and sits squarely on [[ai-readable-code]] / [[agent-legibility]]. Echoes
[[fowler-bockeler-maintainability-sensors|Böckeler]]: computational sensors beat inferential ones for
exactly this. Caveat: CodeScene is Tornhill's own product (motivated); single anecdote, not a study.

## Touches

[[adam-tornhill]] · [[harness-engineering]] · [[ai-readable-code]] · [[agent-legibility]] ·
[[agentic-coding]] · [[feedforward-and-feedback-controls]] · [[model-context-protocol]] ·
[[borg-tornhill-code-for-machines-not-just-humans]] · [[fowler-bockeler-maintainability-sensors]]

_Source: `raw/notes/tornhill-cannot-trust-agent-maintainable-code-codescene-mcp.md`._
