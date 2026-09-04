---
title: Agent Legibility
type: concept
created: 2026-06-11
updated: 2026-06-17
sources: [openai-harness-engineering-codex, miller-codebase-is-the-prompt-vertical-slices-ai, fritzsche-functional-core-imperative-shell-agentic-coding, tornhill-clear-design-principles-agentic-age, khononov-golden-age-of-modularity]
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

**Legibility through code layout (2026-06-15).** [[jeremy-miller]]
([[miller-codebase-is-the-prompt-vertical-slices-ai]]) gives the architectural form of legibility:
"the codebase is part of the prompt," so organizing by [[vertical-slice-architecture|feature slice]]
(not technical layer) means the agent loads only what's relevant — [[locality-of-reference]]. Where this
page pushes tacit knowledge into repo-local artifacts, Miller pushes *the feature itself* into one
place; both reduce the irrelevant context that drives [[context-rot]] and hallucination.

[[fritzsche-functional-core-imperative-shell-agentic-coding|Fritzsche]] adds the enforcement angle:
because "the repository teaches the agent its structure before the prompt does," legibility is held in
place by **project-level skill files** plus review rules that forbid the generic fallback structures
(`service/manager/repository`, `common/shared`) — the "guides" that keep an agent from drifting back
to OOP defaults. The skill *is* the legible record of how features are built here.

**Legibility as named design principles — CLEAR (2026-06-17).** [[adam-tornhill]]
([[tornhill-clear-design-principles-agentic-age]]) names the design side of legibility: agents do
**reconstruction work** (inferring structure from local context), so the goal is to limit the change
*blast radius*. His **CLEAR** principles — Conceptual alignment, Local reasoning, Explicit intent,
Avoid search luck, Reduce the edit surface — are five concrete legibility levers, positioned as a
re-emphasis of classics (information hiding, Law of Demeter) rather than novelty, and explicitly
contrasted with SOLID's human-maintainability target. [[vlad-khononov]]
([[khononov-golden-age-of-modularity]]) gives the theory spine: a design is modular when change is
**localized** (few components, ideally one) and its **effect is predictable** — the same property
stated from coupling theory (his [[balanced-coupling|Balanced Coupling]] model). Both reinforce that
good boundaries are what make a codebase legible/cheap for agents to evolve. This design/code side of
legibility is collected under [[ai-readable-code]].

_Sources: [[openai-harness-engineering-codex]] · [[miller-codebase-is-the-prompt-vertical-slices-ai]] · [[fritzsche-functional-core-imperative-shell-agentic-coding]] · [[tornhill-clear-design-principles-agentic-age]] · [[khononov-golden-age-of-modularity]]._
