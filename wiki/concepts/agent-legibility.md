---
title: Agent Legibility
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [openai-harness-engineering-codex, miller-codebase-is-the-prompt-vertical-slices-ai, fritzsche-functional-core-imperative-shell-agentic-coding, tornhill-clear-design-principles-agentic-age, khononov-golden-age-of-modularity, breunig-who-taught-the-models-to-do-that, zalando-agentic-engineering-snapshot, willison-claudes-new-system-prompt, willison-understanding-chatgpt-work, mcateer-evolution-of-the-agent-harness, cao-agentic-software-restructuring-software-paradigm]
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

## Models reason anywhere that can hold text — so every text field is now output

[[breunig-who-taught-the-models-to-do-that|Breunig, 2026-08-30]]: models are trained to *"search, reflect,
factor, and plan in text before delivering a final response,"* and *"they'll reason **pretty much anywhere
that can hold text**."* Two instances he cites: with reasoning disabled, models think in their regular
output; with Qwen 3.6's thinking hobbled, **the model shifted its reasoning into code comments.** Current
frontier models *"write novels in comments,"* treating them *"like a scratchpad rather than, well, code
comments."*

Independently, [[zalando-agentic-engineering-snapshot|Zalando]] reports the same spill in a different
field: *"even commit messages carry the footprint of coding agents, typically around the 5k character
mark. In one extreme case, we found a commit message to include a full log of unit test execution"* — and
their response is a **pre-commit constraint**.

Two consequences for this page. **(1)** Comments and commit messages are no longer purely human-facing
documentation; scratchpad overflow into them is a **predictable output of training**, not sloppiness, so
the fix is a constraint at the boundary rather than an instruction in a prompt. **(2)** It is a reason the
in-repo-artifact patterns work at all — an on-disk artifact is not only memory, it is **where reasoning
goes when it cannot go anywhere else**, which is part of why
[[edwards-alexander-an-accidental-blackboard|the repo-as-blackboard]] effect emerged and why
[[dilger-highlighting-markers-give-context-to-agents|deliberately legible in-repo artifacts]] and the
[[llm-wiki]] pattern get traction. Neither source connects these; the KB can.

**The mirror image — legibility of the harness to *you* (2026-09).** This page's rule governs what the
agent can see. Two same-week captures document the reverse, and it bounds the whole practice: for a
harness you rent, the decisive layers are not published. [[anthropic]] publishes consumer system prompts
with revision history but not Claude Code's or Cowork's, and — per the model's own account of its context —
the published core prompt is followed by unpublished *"feature- and tool-specific blocks that get added
depending on what's enabled for the session"* ([[willison-claudes-new-system-prompt]]; **a MODEL
SELF-REPORT, not documentation**). [[openai]] publishes neither prompts nor tool descriptions, so the only
available instrument was to have a ChatGPT Work session inventory **itself** — it reported **223 tools and
44 skills** ([[willison-understanding-chatgpt-work]]; **also a model self-report**). Legibility is
therefore high for the layer you build and near-zero for the layer you rent, and the asymmetry is a vendor
choice rather than a property of the technology. See [[agent-harness]].

**What survives absorption.** [[mcateer-evolution-of-the-agent-harness|McAteer (2026-08-22)]] argues that as
models absorb harness capabilities into their weights ([[harness-absorption]]), what is left is the set of
things no model can absorb — **permissions, identity, trust and legibility** — because "a model that absorbs
permissions into itself has dissolved permissions." On that reading this page describes the *durable* part of
harness work and much of the rest is temporary scaffolding. It is a practitioner prediction in an essay, not
evidence — but it is a direct claim about where to invest, and it converges with
[[cao-agentic-software-restructuring-software-paradigm|Cao]]'s academic version of the same relocation
(architectural oversight, quality calibration, ethical governance as the human differentiators — *single-author
arXiv position preprint, not peer-reviewed*). Where the surviving harness becomes a surface aimed at the human
rather than the model, see [[attention-interface]].

_Sources: [[openai-harness-engineering-codex]] · [[miller-codebase-is-the-prompt-vertical-slices-ai]] · [[fritzsche-functional-core-imperative-shell-agentic-coding]] · [[tornhill-clear-design-principles-agentic-age]] · [[khononov-golden-age-of-modularity]] · [[breunig-who-taught-the-models-to-do-that]] · [[zalando-agentic-engineering-snapshot]] · [[willison-claudes-new-system-prompt]] · [[willison-understanding-chatgpt-work]] · [[mcateer-evolution-of-the-agent-harness]] · [[cao-agentic-software-restructuring-software-paradigm]]._
