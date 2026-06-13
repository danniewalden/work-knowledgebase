---
title: Agent Legibility
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [openai-harness-engineering-codex]
tags: [harness-engineering, codex, context]
---

# Agent Legibility

[[openai]]'s framing principle for an agent-first codebase: optimise the repository first for the
*agent's* ability to understand it ([[openai-harness-engineering-codex]]). The operative rule —
**"anything the agent can't access in-context while running effectively doesn't exist."**
Knowledge in Google Docs, Slack threads, or people's heads is invisible to the system, the same
way it would be to a new hire.

Consequences in practice:

- Push tacit knowledge (design rationale, architectural decisions) into **versioned, repo-local
  artifacts** — code, markdown, schemas, executable plans.
- Favour "boring", composable, API-stable technologies the agent can fully model; sometimes
  reimplement a dependency rather than work around opaque upstream behaviour.
- Use **progressive disclosure** (a short AGENTS.md map → structured `docs/`) so context isn't
  crowded out — countering [[context-rot]].

Legibility is the goal that motivates much of [[openai]]'s [[harness-engineering]]; it overlaps
with Böckeler's "ambient affordances" (properties that make an environment harnessable) in
[[fowler-bockeler-harness-engineering]].

_Source: [[openai-harness-engineering-codex]]._
