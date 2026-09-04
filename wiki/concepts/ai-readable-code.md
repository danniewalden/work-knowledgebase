---
title: AI-Readable Code
type: concept
created: 2026-06-17
updated: 2026-08-03
sources: [tornhill-clear-design-principles-agentic-age, khononov-golden-age-of-modularity, miller-codebase-is-the-prompt-vertical-slices-ai, fritzsche-functional-core-imperative-shell-agentic-coding, openai-harness-engineering-codex, tornhill-hidden-design-decisions-control-coupling, tornhill-merge-conflicts-agentic-bottleneck, tornhill-ai-readable-code-series, borg-tornhill-code-for-machines-not-just-humans, khononov-modularity-claude-code-plugin, tornhill-opinionated-guide-to-naming, tornhill-cannot-trust-agent-codescene-mcp, tornhill-why-human-level-ai-wont-be-enough, dilger-planning-like-excel-legible-to-human-and-ai, dilger-drawio-model-in-code, fritzsche-why-solid-is-outdated]
tags: [agentic-coding, agent-legibility, code-health, design, focus]
---

# AI-Readable Code

The emerging idea that, in the agent era, source code should be optimized to be **read, reasoned about,
and safely modified by AI coding agents** — not only by humans. The shared premise across its
proponents: an agent infers a system's structure from local context by search, tool use, and
statistical guesswork, so the cost of a change is dominated by **reconstruction work** and the
**blast radius** of the edit. Code that hides intent, ownership, and change boundaries is expensive and
risky for an agent even when it satisfies classic human-oriented principles.

This is the **design/code side** of [[agent-legibility]] (which is the broader "optimize the repo for
the agent's understanding" principle); AI-readable code is what legibility looks like *in the source
itself*.

## The converging voices

- **[[adam-tornhill]] — CLEAR** ([[tornhill-clear-design-principles-agentic-age]]): five named
  principles for AI-readable code — **C**onceptual alignment, **L**ocal reasoning, **E**xplicit intent,
  **A**void search luck, **R**educe the edit surface — pitched as a re-emphasis of classics (information
  hiding, Law of Demeter) against SOLID's human-maintainability target. Ties to his finding that
  unhealthy code raises agent token spend ([[tornhill-codescene-unhealthy-code-agentic-token-cost]]),
  now backed by the peer-reviewed [[borg-tornhill-code-for-machines-not-just-humans]] (Healthy code →
  15–30% lower AI-refactoring break rate; CodeHealth beats perplexity/SLOC as a predictor).
- **[[vlad-khononov]] — modularity / [[balanced-coupling|Balanced Coupling]]**
  ([[khononov-golden-age-of-modularity]]): the theory spine — *localized change + predictable effect*,
  achieved by balancing coupling (strength × distance × volatility). "Boundaries are what AI depends on."
  Now shipped as a runnable agent skill ([[khononov-modularity-claude-code-plugin|Modularity Skills]]):
  review/design skills that flag or prevent coupling imbalances, since AI-generated code accumulates
  architectural debt faster than it can be caught at the line level.
- **[[jeremy-miller]] — "the codebase is the prompt"**
  ([[miller-codebase-is-the-prompt-vertical-slices-ai]]): code *layout* is part of the prompt; feature
  [[vertical-slice-architecture|slices]] keep work local ([[locality-of-reference]]) where layered code
  pollutes the context window.
- **[[rico-fritzsche]] — functional core / imperative shell**
  ([[fritzsche-functional-core-imperative-shell-agentic-coding]]): the repo *shape* instructs the agent
  before the prompt; behavior-named files, share-nothing slices, conventions enforced by skill files.
- **[[openai]] — legibility** ([[openai-harness-engineering-codex]]): "anything the agent can't access
  in-context doesn't exist" — push tacit knowledge into repo-local artifacts; the harness-side root of
  the idea.

## The common thread

All five reduce to: **make intent and boundaries explicit and local, so a change stays small and
predictable.** That is simultaneously a coupling/cohesion argument (Khononov), a code-health argument
(Tornhill), an architecture argument (Miller, Fritzsche — [[vertical-slice-architecture]]), and a
harness argument ([[harness-engineering]], [[agent-legibility]], [[context-engineering]] — less
irrelevant context means less [[context-rot]] and fewer hallucinations). It also rhymes with
[[martin-dilger|Dilger's]] "coupling, not context-window" line from the
[[dilger-event-modeling-agent-harness|Event Modeling Agent Harness]]. The strand now has its first
**empirical anchor**: [[borg-tornhill-code-for-machines-not-just-humans]] (FORGE 2026) measures that
healthier code is measurably safer for an LLM to modify (15–30% lower break rate; CodeHealth a better
predictor than perplexity or SLOC) — turning "AI-readable" from a design intuition into a testable
property.

## Worked examples & scale (Tornhill series)

CLEAR was distilled from concrete refactorings ([[tornhill-ai-readable-code-series]]): the
[[tornhill-hidden-design-decisions-control-coupling|boolean-flag → Strategy]] refactoring shows
*Explicit intent* + *Local reasoning* at the call site (a flag is "cheap for humans, expensive for
models"). The principle also scales up: [[tornhill-merge-conflicts-agentic-bottleneck|merge conflicts]]
are AI-readability failing at the **architecture** level — when boundaries don't give independent work
separate homes, parallel agents collide in the same code, and behavioral code analysis (hotspots,
change coupling) locates the misalignment ([[conways-law]], [[vertical-slice-architecture]]). Two
counter-weights from the same author are worth holding here: *Compressed Cognition* (the cost of agentic
speed is decision density) and *SDD and the Illusion of Known Scope* (a pragmatic check on
[[spec-driven-development|spec-first]] optimism).

## Naming as the highest-leverage move (Tornhill, 2026-06-23)

[[tornhill-opinionated-guide-to-naming]] isolates **naming** as the cheapest, highest-return slice of
AI-readable code: names are "cognitive compression mechanisms" that minimize the **reconstruction work**
for humans *and* agents, with a cited LLM result that improving **identifier names "consistently yielded
the largest returns"** for code understanding (arXiv 2505.10443). Practical heuristics — name for the
*call site*, "Wishful Thinking" first, let **domain types** free parameter names from primitive
obsession, scope-sets-length — operationalize CLEAR's *Explicit intent* and *Local reasoning*.

## You can't trust the agent to self-assess — use a deterministic sensor (Tornhill, 2026-06-22)

[[tornhill-cannot-trust-agent-codescene-mcp]] is the harness-side corollary: an LLM is non-deterministic
and **has no reliable way to assess code health**, and the messy existing code *is* the context, so
agents do worst where they're needed most. Asking an agent to "follow SOLID" or having another LLM
review it doesn't fix this — the answer is a **deterministic, external code-health sensor** (Tornhill
uses the CodeScene [[model-context-protocol|MCP]]) as the agent's source of truth. So AI-readable code is
not only a design target but something a [[harness-engineering|harness]] must *measure* with a
computational ([[feedforward-and-feedback-controls|not inferential]]) sensor.

## Why it matters at all — the environment-over-model floor (Tornhill, 2026-06-30)

[[tornhill-why-human-level-ai-wont-be-enough]] supplies the *theoretical justification* for the whole
concept. Even coding agents at best-human-expert level won't be enough, because AI **raises its own
quality bar** through **scale** (Lehman's laws; defect opportunities grow with code + change volume) and
**speed** (faster generation → higher churn/fault risk = "wrong at scale"), and the stochastic core
means one-in-a-million errors recur across millions of decisions. Tornhill rejects the "superhuman code
quality" path and prescribes the opposite: **"create environments where unreliable agents reliably
produce acceptable outcomes."** That *is* the case for AI-readable code — the leverage is in the
environment (legible, low-blast-radius code + [[harness-engineering|harness]] sensors), not in a better
model — and it links this concept to [[loop-engineering]] and to
[[dilger-harness-is-20-percent-requirements-are-80|Dilger's "harness is 20%"]].

## Legibility of the *spec*, not just the code (Dilger, 2026-07-09)

[[dilger-planning-like-excel-legible-to-human-and-ai]] extends "AI-readable" one level up — to the
**spec/model** itself. His [[eventmodelers-ai]] uses an **Excel-like grid** so every model element has a
**cell-reference coordinate**: an agent can be instructed *("add a field in B3, adjust all dependents")*
and can report back against the same precise handle. "Clear structure… is what makes a spec legible to a
human and an AI at once." Same principle as call-site naming and explicit boundaries — *make intent and
location unambiguous and addressable* — applied to the [[event-modeling|Event Model]] rather than the
source ([[event-modeled-agent-design]], [[spec-driven-development]]).

## A machine-readable model isn't enough — the agent needs a framework (Dilger, 2026-06-30)

[[dilger-drawio-model-in-code]] applies the same logic to the **spec/model layer** but sharpens a
distinction the code-side voices assume: *serializable ≠ agent-editable.* Clients keep their Event Model as
**draw.io XML** in git and let AI manipulate it — the model is "in the code," which Dilger endorses. But raw
XML fails the agent because it gives "no framework to follow, no rules — so it's easy to make mistakes"
(and, humans-side, it isn't directly readable — you need a viewer). His fix is not just a cleaner format but
a **validating framework**: a standardized JSON schema plus an [[model-context-protocol|MCP]] that checks
the agent's edits *before commit*, so the agent self-corrects. This is the model-layer twin of
[[tornhill-cannot-trust-agent-codescene-mcp|"you can't trust the agent to self-assess — use a deterministic
external sensor"]]: AI-readability requires not only explicit, addressable structure (cf.
[[dilger-planning-like-excel-legible-to-human-and-ai|the Excel grid's cell coordinates]]) but an
*enforcement* mechanism that makes malformed edits impossible to land. It also complements
[[event-modeled-agent-design]] and [[spec-driven-development]] — the spec can only be "the source of truth"
if the agent can't silently corrupt it.

## Open question

Is there a consensus *definition* forming, or just parallel vocabularies? A synthesis that maps CLEAR ↔
Balanced Coupling ↔ locality ↔ legibility onto one another would be a natural next page.

## SOLID is the wrong default for agents (Fritzsche, 2026-08)

[[rico-fritzsche|Fritzsche]] adds the strand's sharpest **agent-specific** claim
([[fritzsche-why-solid-is-outdated]]): **SOLID is outdated as a general doctrine and default checklist**,
and — the load-bearing point here — "AI coding agents **reproduce the same [SOLID] structures unless the
repository gives them a different design policy**." So an agent *defaults to* speculative interfaces,
prescient OCP extension points, and SRP-by-technical-concern unless the repo's conventions
([[harness-engineering]] guides, [[agent-legibility]]) say otherwise. His critique lands on the same
target as [[tornhill-clear-design-principles-agentic-age|CLEAR]] and
[[khononov-golden-age-of-modularity|Balanced Coupling]]: four of the five principles (SRP/OCP/ISP/DIP)
give **no failure signal** (every split/extension/interface counts as "compliance"), so they can't reject
a harmful boundary; only LSP (a correctness condition) survives. His replacement is North's **CUPID**
(properties by degree) and "start the review with the change itself" — *which concrete change does this
boundary make cheaper, and who asks for it?*

_Sources: [[tornhill-clear-design-principles-agentic-age]] · [[khononov-golden-age-of-modularity]] · [[miller-codebase-is-the-prompt-vertical-slices-ai]] · [[fritzsche-functional-core-imperative-shell-agentic-coding]] · [[openai-harness-engineering-codex]] · [[tornhill-hidden-design-decisions-control-coupling]] · [[tornhill-merge-conflicts-agentic-bottleneck]] · [[tornhill-ai-readable-code-series]] · [[borg-tornhill-code-for-machines-not-just-humans]] · [[tornhill-opinionated-guide-to-naming]] · [[tornhill-cannot-trust-agent-codescene-mcp]] · [[tornhill-why-human-level-ai-wont-be-enough]] · [[dilger-planning-like-excel-legible-to-human-and-ai]] · [[dilger-drawio-model-in-code]] · [[fritzsche-why-solid-is-outdated]]._
