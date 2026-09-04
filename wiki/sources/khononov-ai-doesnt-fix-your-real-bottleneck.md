---
title: "Source: Khononov — AI Doesn't Fix Your Real Bottleneck"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [khononov-ai-doesnt-fix-your-real-bottleneck]
raw_file: [raw/articles/khononov-ai-doesnt-fix-your-real-bottleneck.md]
tags: [coupling, balanced-coupling, modularity, comprehension-debt, agentic-coding, substrate, focus]
---

# Source: Khononov — AI Doesn't Fix Your Real Bottleneck

Article by **[[vlad-khononov]]** ("Rants on Software Design", vladikk.com, 2026-02-23). Raw capture:
`raw/articles/khononov-ai-doesnt-fix-your-real-bottleneck.md` — an **out-of-window backfill** (2026-02,
filed on the 2026-09-04 sweep), transcribed verbatim, full body through the closing "P.P.S.", lead image
noted inline.

**Markers that travel with every claim below.** **NOT INDEPENDENT:** Khononov is the author of the
[[balanced-coupling|Balanced Coupling]] model and of *Balancing Coupling in Software Design*, and the
post closes by linking that book (an `amzn.to` affiliate link) and coupling.dev — this is the model's own
author arguing that his model is the answer to the AI-era bottleneck, not external corroboration.
**IMPRESSION NOT MEASUREMENT:** the whole argument is analytical. "Every other post on my feed
celebrates…", the "hundred-fold productivity gains" he rebuts, and the claim that the system degrades are
observation and inference, not data from this post. The **4±1 / 7±2** working-memory figures are cited as
"studies" **with no reference given on the page** — cite them as *unreferenced as captured*, never as
this post's evidence.

## Summary

A **Theory of Constraints** argument applied to software: a system's throughput is set by its single
bottleneck, so improving a *non*-bottleneck makes the system **worse**, not better — it piles up
work-in-progress in front of the constraint. Khononov's claim is that **the bottleneck in software
engineering is our ability to comprehend systems**, not our ability to produce code. Writing new code is
"the easy part"; the hard part is *evolving* a system you may not have built, which requires predicting
what a change will do.

Therefore AI, which accelerates code *production*, is speeding up a non-bottleneck: cognitive load piles
up, changes become trial-and-error, and "the Theory of Constraints predicts exactly what happens next:
the system degrades." He extends the point to the agents themselves — "the larger the codebase an LLM has
to work with, the faster its context fills up and the less effective it becomes." The answer is
**modularity**, and the way to get it is to balance three dimensions of coupling.

## Key points

- **The bottleneck claim, stated flatly:** "The bottleneck in software engineering is our ability to
  comprehend systems." Cognitive capacity is the hard ceiling (the 4±1 / 7±2 figures, unreferenced here).
- **His definition of complexity is operational, not aesthetic:** not "this is a hard problem" but
  "**we don't know what will happen when we touch something**" — the state you reach when required
  cognitive load exceeds capacity.
- **This is the source of the full triad.** The three dimensions of coupling are named and defined *here*
  — **shared knowledge** (how much knowledge components share about each other, i.e. the axis the KB's
  [[balanced-coupling]] page calls *strength*), **distance** (physical and organizational), and
  **volatility** (probability a component needs to change at all). The balance rule follows: components
  that change together should be close; components that don't should be far apart; **"volatility
  multiplies the effects of complexity."**
- **Note the boundary between his two February posts.** The *triad* is here. His companion piece
  ([[khononov-coupling-should-be-weighed-not-counted]], 2026-02-26) covers **only the Integration
  Strength axis**. Do not attribute the triad to the coupling post.
- **The reframed question:** not "how do we write code faster?" but "**how do we keep systems
  understandable as they grow?**" AI can help with that — "but only if we point it at the right problem."
- **The P.S. is the load-bearing caveat against agent-generated modularity:** "Generating code that
  *looks* modular and designing a system that *is* modular are two very different things. Modularity is a
  system-level property. It requires understanding the business domain, the organizational structure, and
  the trade-offs between them. That's not a prompting problem."

## Connections / contrast

- **This is [[comprehension-debt]] derived from first principles**, and it arrives at the same place as
  the KB's practitioner voices by a different route. Where [[addy-osmani]] coined comprehension debt as a
  *gap that accumulates* and [[dilger-real-cost-of-ai-is-second-order|Dilger]] priced it on a CTO's
  ledger (~30% cost rise at flat headcount — his field anecdote), Khononov derives it as a **queueing
  consequence**: accelerating an upstream station in front of a constraint is *predicted* to degrade the
  system. Same phenomenon, three registers: theory, coinage, and a priced anecdote.
- **Completes the [[balanced-coupling]] page's own provenance.** That page states the triad but sources
  it to the book and the [[coupling-research-note]]; this is a **first-party blog statement** of all
  three dimensions and the balance rule in the author's own current words, tied explicitly to the AI
  moment.
- **Sharpens the [[khononov-golden-age-of-modularity|"Golden Age of Modularity"]] line.** That post gave
  the two-part modularity test (localized change, predictable effect) and said the vibe-coding wave "only
  pays off when the code is modular." This one supplies the *mechanism* for why — and the P.S. adds a
  claim the KB did not have from him: that an agent producing modular-*looking* code is not the same as a
  modular system, because modularity is a system-level property involving domain and org structure.
- **Converges with the substrate voices without being one of them.** The same conclusion, from
  [[jeremy-miller]] ([[miller-codebase-is-the-prompt-vertical-slices-ai]]), [[rico-fritzsche]],
  [[adam-tornhill]] ([[tornhill-clear-design-principles-agentic-age|CLEAR]]) and
  [[oskar-dudycz|Dudycz's]] closing note in
  [[dudycz-vertical-slices-ownership-and-external-dependencies]] ("it's an old argument that happens to
  have got more valuable") — all of which are also assertion, not measurement. Khononov is the only one
  who grounds it in an established manufacturing principle rather than in agent experience.
- **The skeptic continuity.** Consistent with his contrarian role on [[loop-engineering]] via
  [[khononov-microservices-hype-to-ai-sloop]]: the wave pays off only on a modular substrate.
- Adjacent: [[agentic-coding]] · [[locality-of-reference]] · [[agent-legibility]] ·
  [[token-budget-quality-cliff]] (his "context fills up" claim is that page's argument in one line) ·
  [[business-capabilities]] · [[coupling-taxonomy]].

## Limits

- **No data.** Nothing in this post is measured. The Theory of Constraints mapping is an **analogy
  argued**, not a study of software teams, and "the system degrades" is a *prediction*, not an observed
  outcome. The 4±1 / 7±2 figures are **unreferenced as captured** — do not promote them to citable
  findings on the strength of this page.
- **NOT INDEPENDENT** (see marker): the post's conclusion is the author's own commercial model.
- The **"AI can help with that too"** claim is left undeveloped — no worked example of pointing an agent
  at modularity rather than at code volume. (His [[khononov-modularity-claude-code-plugin|Modularity
  Skills plugin]] is that attempt, and it too is unevaluated.)
- Out-of-window (2026-02); surfaced by backfill, not a new development.

_Source: `raw/articles/khononov-ai-doesnt-fix-your-real-bottleneck.md`._
