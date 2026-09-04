---
title: "Fritzsche — Why SOLID Is Outdated"
type: source
created: 2026-08-03
updated: 2026-08-03
sources: [fritzsche-why-solid-is-outdated]
raw_file: [raw/articles/fritzsche-why-solid-is-outdated.md]
tags: [ai-readable-code, design-principles, solid, cupid, coupling-cohesion, agentic-coding, focus]
---

# Fritzsche — Why SOLID Is Outdated

Blog article by **[[rico-fritzsche]]** (ricofritzsche.me, 2026-08-01). "I recommended SOLID for years. I
was wrong." The precise claim: **SOLID is wrong as a general design doctrine and as a default checklist.**
Raw: `raw/articles/fritzsche-why-solid-is-outdated.md`.

## The argument

- **Priced for a dead world.** The principles were justified by hour-long compiles and risky releases
  (Martin's own "environment viscosity"). Tooling killed that cost; the rules stayed as ritual — shaping
  reviews, interviews, training. **The agent-era hook:** "AI coding agents reproduce the same structures
  unless the repository gives them a different **design policy**" — SOLID is now a *default an agent
  inherits*, which puts this squarely on the [[ai-readable-code]] thread.
- **Five letters from different eras, four with no failure signal.** LSP (Liskov 1987), OCP (Meyer 1988),
  plus Martin's DIP/ISP/SRP — a sub-type contract, a cohesion rule, an extension policy, an interface
  technique, and a dependency rule at one level. SRP/OCP/ISP/DIP give **no signal when the rule is
  *damaging* the design** (every split/extension-point/interface counts as "compliance"). Only **LSP** is
  exempt — a broken sub-type contract fails a test.
- **OCP is a bet on prediction.** Closing a module needs knowing where change arrives; Martin conceded
  closure "takes a certain amount of prescience." A wrong guess is dead structure (North's "Cruft
  Accretion Principle"). Justified only when callers can't ship together (published API, plug-in, event
  schema, cross-team consumer). Inside one app, prefer direct change; add an extension point when callers
  change independently, behaviors must coexist at runtime, or the variation recurs.
- **"One reason to change" decides nothing.** SRP permits splitting by technical concern, stakeholder,
  capability, or deployment — all at once. Better criteria: **Parnas** (hide a *decision likely to
  change*), **Ousterhout** (hide substantial complexity behind a simple interface — shallow classes
  increase navigation).
- **Every interface needs a reason.** ".NET's `services.AddScoped<InvoiceCalculator>()`" — a concrete
  registration is fine; an `I`-prefixed pair with one owner/impl/caller adds a type, a name, a file, a
  mapping, and a navigation step for nothing. Ask: *which concrete change does this boundary make cheaper,
  and who asks for it?*
- **Replacement:** North's **CUPID** (Composable, Unix-philosophy, Predictable, Idiomatic, Domain-based) —
  properties held *by degree*, so you can assess and improve one in context without minting another type.
  Start reviews with **the change itself**, not the acronym.

## Why it matters here

- A strong new voice on [[ai-readable-code]]: like [[tornhill-clear-design-principles-agentic-age|Tornhill's
  CLEAR]] it argues the design rules that make code tractable for agents are *not* SOLID, and (crucially)
  that agents **default to SOLID unless the repo's design policy says otherwise** — a
  [[harness-engineering]] / [[agent-legibility]] point (the repo's conventions are the guide). Converges
  with [[khononov-golden-age-of-modularity|Khononov]] (judge coupling, not rule-compliance) and his own
  FC/IS-for-agents recipe.
- Caveat: opinionated single-author essay; the one empirical item cited (a 2024 SOLID-comprehension study)
  actually found SOLID-restructured code *easier* to understand short-term — Fritzsche notes its scope
  (self-rated, short-term, selected ML code) excludes long-term/interface-heavy maintenance.

## Links

Entities: [[rico-fritzsche]], [[adam-tornhill]], [[vlad-khononov]]. Concepts: [[ai-readable-code]],
[[coupling-taxonomy]], [[balanced-coupling]], [[agentic-coding]], [[harness-engineering]],
[[agent-legibility]].
Related sources: [[tornhill-clear-design-principles-agentic-age]], [[khononov-golden-age-of-modularity]],
[[fritzsche-clean-architecture-capability-over-layers]],
[[fritzsche-functional-core-imperative-shell-agentic-coding]].

_Raw source: `raw/articles/fritzsche-why-solid-is-outdated.md`._
