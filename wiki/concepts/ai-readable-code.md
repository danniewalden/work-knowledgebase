---
title: AI-Readable Code
type: concept
created: 2026-06-17
updated: 2026-09-04
sources: [tornhill-clear-design-principles-agentic-age, khononov-golden-age-of-modularity, miller-codebase-is-the-prompt-vertical-slices-ai, fritzsche-functional-core-imperative-shell-agentic-coding, openai-harness-engineering-codex, tornhill-hidden-design-decisions-control-coupling, tornhill-merge-conflicts-agentic-bottleneck, tornhill-ai-readable-code-series, borg-tornhill-code-for-machines-not-just-humans, khononov-modularity-claude-code-plugin, tornhill-opinionated-guide-to-naming, tornhill-cannot-trust-agent-codescene-mcp, tornhill-why-human-level-ai-wont-be-enough, dilger-planning-like-excel-legible-to-human-and-ai, dilger-drawio-model-in-code, fritzsche-why-solid-is-outdated, tornhill-beyond-lambdas-raising-the-abstraction-level, tornhill-controlling-the-uncertainty-machine, tornhill-blast-from-the-past-sdd-illusion-of-known-scope, tornhill-compressed-cognition-cost-of-faster-coding]
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
  achieved by balancing coupling (shared knowledge × distance × volatility — see [[balanced-coupling]] on the axis naming). "Boundaries are what AI depends on."
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
counter-weights from the same author are worth holding here:
[[tornhill-compressed-cognition-cost-of-faster-coding|*Compressed Cognition*]] (the cost of agentic
speed is decision density) and
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|*SDD and the Illusion of Known Scope*]] — not
merely "a pragmatic check on [[spec-driven-development|spec-first]] optimism" but a positive claim about
readability's limits: **implementation is the discovery process**, each specified requirement spawns tens
of implicit design decisions (Glass's requirements explosion, **as relayed by Tornhill**), and *"the
moment a model becomes the implementation, it ceases to be a good model."*

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

## Name the nameless — abstraction level at expression scale (Tornhill, 2026-09-01)

[[tornhill-beyond-lambdas-raising-the-abstraction-level|Beyond Lambdas]] is the series' newest
walkthrough and its smallest-scale lever. The asymmetry it turns on: *"The nice thing about lambdas is
that they optimize for **writing** code… The bad thing about lambdas is that they optimize for writing
code. They do so at the expense of **reading** code, which is arguably a much more frequent activity."*
A three-line `map/filter/sum` stream over dice rolls is "trivial" in mechanics and opaque in purpose —
"it could be anything" — until the lambdas are named as domain operations (`AttackRoll::applyStrengthModifier`,
`AttackRoll::isSuccessfulHit`), and in Clojure a step further, naming the **pipeline elements**
themselves so "the code now reads like a story." His line: **"Anonymous functions are anonymous
thoughts."**

Three claims worth keeping beyond the refactoring:

- **Abstractions need not be reused to be justified.** "Abstractions can be simple. Ridiculously
  simple… **Lines of code are not a finite resource.**" His test is about reading, not economy: *"if it
  elevates the level of the code, then it has earned its rights."* A deliberate break with the DRY-first
  reflex, and — unengaged by either author — the opposite stance from
  [[willison-conceptual-integrity-and-counting-lines-of-code|Willison's]] hard-ceiling defence of LOC as
  a productivity indicator. Both are on-thread; the KB holds both.
- **The target is reconstruction work**, the same target as
  [[tornhill-clear-design-principles-agentic-age|CLEAR]]: new tasks arrive inside an existing codebase,
  and "the closer our abstractions reflect the problem domain," the less has to be reconstructed before
  a safe change.
- **This is the precondition for reading selectively.** Every remedy on [[verification-burden]] —
  Tornhill's own included — assumes a human or agent can cheaply recover intent from a fragment. Naming
  is how that stays affordable: the *supply* side of a reading budget whose *demand* side he prices in
  [[tornhill-compressed-cognition-cost-of-faster-coding|Compressed Cognition]].

A style argument with a toy example: one D&D snippet in two languages, no measurement, and the agent
claim is by reference to CLEAR rather than tested. The nearest actual evidence remains
[[borg-tornhill-code-for-machines-not-just-humans]] and the LLM identifier-name result relayed in
[[tornhill-opinionated-guide-to-naming]] — neither about lambdas.

## Enforce what you don't inspect (Tornhill, 2026-08-20)

The page's design advice acquires a *reason* here. If nobody reads all the code
([[verification-burden]]), then AI-readable code stops being a courtesy to future humans and becomes
the load-bearing guarantee: [[tornhill-controlling-the-uncertainty-machine]] argues "AI amplified the
need for maintainable code" because "successful features attract change," and answers the obvious
question — how do you keep uninspected code maintainable? — with a **multi-layered safety net**:
accumulated SKILLs capturing style and architecture rules, plus **deterministic** enforcement (linters,
vulnerability scanners, custom architectural and e2e checks, and CodeScene's CodeHealth MCP).
*"These rules and constraints need to be enforced. Deterministically."* **VENDOR SELF-REPORT** — the
prescription names his own company's product; the premise it rests on is his separate argument that an
LLM cannot reliably self-assess code health ([[tornhill-cannot-trust-agent-codescene-mcp]]). See also
[[fitness-functions]], where the same move appears as a build-time constraint.

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

_Sources: [[tornhill-clear-design-principles-agentic-age]] · [[khononov-golden-age-of-modularity]] · [[miller-codebase-is-the-prompt-vertical-slices-ai]] · [[fritzsche-functional-core-imperative-shell-agentic-coding]] · [[openai-harness-engineering-codex]] · [[tornhill-hidden-design-decisions-control-coupling]] · [[tornhill-merge-conflicts-agentic-bottleneck]] · [[tornhill-ai-readable-code-series]] · [[borg-tornhill-code-for-machines-not-just-humans]] · [[tornhill-opinionated-guide-to-naming]] · [[tornhill-cannot-trust-agent-codescene-mcp]] · [[tornhill-why-human-level-ai-wont-be-enough]] · [[dilger-planning-like-excel-legible-to-human-and-ai]] · [[dilger-drawio-model-in-code]] · [[fritzsche-why-solid-is-outdated]] · [[tornhill-beyond-lambdas-raising-the-abstraction-level]] · [[tornhill-controlling-the-uncertainty-machine]] · [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]]._
