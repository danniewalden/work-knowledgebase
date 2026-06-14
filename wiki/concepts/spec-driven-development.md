---
title: Spec-Driven Development
type: concept
created: 2026-06-13
updated: 2026-06-14
sources: [dilger-spec-driven-development-applied, dilger-faros-ai-report-amplifies-unclear-requirements, dilger-keep-command-handlers-pure, jwilger-agent-skills-event-modeling, dilger-model-is-a-living-spec-always-on-agent, fraktalio-event-modeler-connect-ai-agents-mcp]
tags: [event-modeling, agentic-coding, spec-driven-development, harness, focus]
---

# Spec-Driven Development

The practice of producing a **clear, validated specification of intended behavior before any code is
written** — and, in the agent era, using that spec as the *environment* that constrains an AI coding
agent rather than trying to steer it with better prompts. Named and evangelized by
**[[martin-dilger]]** ([[dilger-spec-driven-development-applied]], with a `#specdrivenbook` tag for his
book *Spec Driven*), but the underlying move is shared across the KB's harness thread.

## The core argument

- **Prompt engineering is the wrong lever.** Dilger calls it "a desperate attempt to force a language
  model to behave through better wording" that "didn't work." You can't *force* an agent ("AI is like
  a teenager"); you **design an environment where good behavior is the path of least resistance** and
  add feedback loops that keep answering "am I holding this right?"
- **The spec is the environment.** [[event-modeling]] supplies "clarity of intent before a single line
  of code gets written"; that artifact becomes the agent's source of truth. Dilger's rule of thumb:
  *every process that worked well without AI works even better with AI*, because such processes make
  the right thing easier than the wrong thing.
- **Unclear requirements get amplified, not fixed.** The Faros AI Report's quality regressions
  (incidents/PR +242.7%, review time +441.5%) are read as evidence that throughput without an upstream
  spec just ships defects faster ([[dilger-faros-ai-report-amplifies-unclear-requirements]]).
- **The spec is the work — and it's *live*.** Dilger's sharpest statement: "The spec isn't a stepping
  stone to the code anymore. The spec is the work. Everything else follows." He describes an agent
  building continuously from a model as he edits it, with a slice→tests-as-harness→implement→PR loop
  ([[dilger-model-is-a-living-spec-always-on-agent]]). On the tooling side, [[fraktalio]]'s Event
  Modeler has an agent author the model and its Given-When-Then specs over MCP
  ([[fraktalio-event-modeler-connect-ai-agents-mcp]]) — spec-first realized as a feature.

## Relationship to the rest of the KB

Spec-driven development is the *requirements/intent* face of [[event-modeled-agent-design]]: where
that page maps Event Modeling constructs onto agents, this names the discipline of putting the model
*first*. It converges with [[harness-engineering]]'s guides-and-sensors model and
[[feedforward-and-feedback-controls]] (the "am I holding this right?" loops are inferential sensors),
and with [[context-engineering]] (the spec is high-value context loaded before work). The strongest
worked instance is [[jwilger-agent-skills-event-modeling]], where the spec — vertical slices + Given-
When-Then scenarios — literally becomes the machine-checkable contract (TDD acceptance gates) for an
autonomous build. [[dilger-keep-command-handlers-pure]] is the cautionary corollary: a written spec/
skill is necessary but **not sufficient** — the harness must *enforce* it, because agents drift.

## Open questions

Most spec-driven claims in the KB are practitioner assertions or single-developer projects; a
production case study quantifying spec-first vs. prompt-first agent output (the inverse of the Faros
numbers) is still wanted.

_Sources: [[dilger-spec-driven-development-applied]] ·
[[dilger-faros-ai-report-amplifies-unclear-requirements]] · [[dilger-keep-command-handlers-pure]] ·
[[jwilger-agent-skills-event-modeling]] · [[dilger-model-is-a-living-spec-always-on-agent]] ·
[[fraktalio-event-modeler-connect-ai-agents-mcp]]._
