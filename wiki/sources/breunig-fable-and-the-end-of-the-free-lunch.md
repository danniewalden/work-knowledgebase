---
title: "Source: Breunig — Fable & The End of the Free Lunch"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [breunig-fable-and-the-end-of-the-free-lunch]
raw_file: [raw/articles/breunig-fable-and-the-end-of-the-free-lunch.md]
tags: [harness-engineering, economics, model-routing, context-engineering, focus]
---

# Source: Breunig — Fable & The End of the Free Lunch

Source: **Drew Breunig**, *"Fable & The End of the Free Lunch"*, dbreunig.com, **2026-08-23**. Raw
capture: `raw/articles/breunig-fable-and-the-end-of-the-free-lunch.md`. Companion to
[[breunig-harnesses-are-situated-agents]]; surfaced via [[simon-willison|Willison's]] same-day
quotation. Very short (~400 words) and the only **economic** argument for harness work in the KB.

## Summary

An analogy, carried carefully. Under **Moore's Law** it made no sense to ruthlessly optimize code —
"in 18 months, a CPU would arrive that would double your performance" (Herb Sutter's **"free lunch"**).
When single-threaded performance stagnated in the mid-2000s, *"we suddenly had to think about
parallelization, architecture, memory locality… **We had to think about what work went where.**"*
Breunig claims model pricing has just crossed the same threshold: **before Fable, harness and context
work was largely wasted effort** because a cheaper-or-equal model would arrive and paper over the
problems. Fable was *"incredible"* but expensive enough — and the cheaper alternatives good enough —
that *"we started to think about what work went where."*

## Key points

- **The reframe: harness engineering as an economics story, not a capability story.** The KB's
  [[harness-engineering]] page argues the harness raises reliability. Breunig adds the orthogonal
  argument: **the harness is what lets a cheaper model do the work.** *"As we continue to develop better
  harnesses it will be easier to provide weaker (but still great) models with sufficient context to
  perform well."*
- **"What work goes where" becomes a first-class harness concern** — i.e. **model routing by
  cost/capability** is part of the harness design, not an optimization afterthought.
- **His own worked pattern:** *"I frequently chat with Fable to interrogate and shape a design, before
  handing off a brief to GLM."* Expensive model for design interrogation; cheap model for execution
  against a written brief. This is a **spec-shaped handoff**, and it is the whole mechanism in one
  sentence.
- **He pre-answers the obvious objection.** *"I get pushback that falling inference prices will
  eventually bring us back to sending everything through the largest models. But I'm not so sure: those
  same gains will benefit the K3s and Qwens"* — the price floor moves down for everyone, so the *ratio*
  persists even if the absolute cost falls.
- **A second, non-price lock-in.** *"Fable's **other** shock likely locks in this change. Fable's access
  controls, dynamic degradation, and required data retention spooked enough companies (and countries!)
  into thinking about where they send their traces and where they get their tokens."* So routing is
  driven by **data governance and jurisdiction**, not only by cost — which makes it durable even if the
  price argument weakens.
- **Limits.** A blog post of roughly 400 words; **no numbers of its own beyond price ratios asserted without
  source** — "GLM 5.2… roughly 1/9th the cost (and ~1/5th the cost of Opus 5)" is stated flatly with no
  citation, and the quality comparison is explicitly a shrug: *"Is GLM 1/9th the quality of Fable?
  Perhaps, for certain classes of tasks. But for most rote coding it's more than sufficient."* That is a
  **practitioner impression, not a measurement** — there is no benchmark, no task taxonomy, and no
  definition of "rote." Every model name (Fable, Opus 5, GLM 5.2, K3, 5.6) and every price ratio is
  **date-bound to August 2026** and will be wrong shortly. The opening premise — "agentic coders are
  balking at Anthropic's pricing" — is sourced to "some talk today." The Moore's-Law analogy is doing a
  lot of the argumentative work and is not defended.

## Connections / contrast

**This is the missing "why bother" for [[harness-engineering]] and [[context-engineering]].** Both KB
pages justify the work on reliability grounds. Breunig supplies a cost mechanism: a better harness
substitutes for a better model. That makes harness quality **fungible with token spend**, which connects
directly to [[tornhill-codescene-unhealthy-code-agentic-token-cost|Tornhill's]] claim that unhealthy code
raises agent token spend 35–45% (a **vendor claim**) and to
[[borg-tornhill-code-for-machines-not-just-humans|Borg & Tornhill's]] peer-reviewed finding that code
health predicts refactoring correctness — three sources, one economics: **the environment is a
substitute for model capability.** [[tornhill-why-human-level-ai-wont-be-enough]] states the general
form.

**It is the strongest argument in the KB for the [[event-modeling]] seam.** A well-specified slice with
its [[given-when-then|given/when/then]] is precisely *"sufficient context"* that lets a weaker model
execute a brief — the capture note makes this connection and it holds: Breunig's own workflow (interrogate
the design with the expensive model, hand a **brief** to the cheap one) is
[[spec-driven-development]] rediscovered as a cost-control measure. Compare
[[dilger-harness-is-20-percent-requirements-are-80]] — if requirements are 80% of the value, then the
requirements artifact is what buys you the cheap-model discount.

**Against [[breunig-harnesses-are-situated-agents|his own companion piece]]:** there he argues harnesses
are getting *stickier* (SaaS-like lock-in around the eight layers). Here he argues the harness's job is
to make the **model** swappable. Both can hold — the harness becomes the durable asset precisely because
what it wraps is commoditized — but note the asymmetry: **models become fungible, harnesses do not.**
That is a sharper version of the KB's [[agent-harness]] "not the same as the model" boundary.

**It also reframes [[token-budget-quality-cliff]] and multi-model routing.**
[[addyosmani-code-agent-orchestra|Osmani's]] `MODEL_ROUTING.md` (planning → cheaper model,
implementation → Sonnet/Opus/Codex, review → a dedicated security model) is the same practice as a
config file; [[miracle-my-loop-engineering-workflow|Miracle's]] commission rule — "Subagents default to
the cheaper model tier; spend the expensive one on the critical path" — is it as a standing instruction.
Breunig supplies the reason all three are doing it.

**Caution for the KB's own framing:** do not let this become "harness work is now proven worthwhile."
The claim is that the *incentive* changed, and it rests on one author's read of one month's pricing.

## Links

[[harness-engineering]] · [[context-engineering]] · [[agent-harness]] · [[loop-engineering]] ·
[[token-budget-quality-cliff]] · [[spec-driven-development]] · [[given-when-then]] · [[event-modeling]] ·
[[agent-governance]] · [[locality-of-reference]] · [[simon-willison]] · [[adam-tornhill]] ·
[[breunig-harnesses-are-situated-agents]] · [[breunig-who-taught-the-models-to-do-that]] ·
[[tornhill-codescene-unhealthy-code-agentic-token-cost]] ·
[[borg-tornhill-code-for-machines-not-just-humans]] ·
[[tornhill-why-human-level-ai-wont-be-enough]] ·
[[dilger-harness-is-20-percent-requirements-are-80]] ·
[[addyosmani-code-agent-orchestra]] · [[miracle-my-loop-engineering-workflow]]

_Source: [[breunig-fable-and-the-end-of-the-free-lunch]] (raw: `raw/articles/breunig-fable-and-the-end-of-the-free-lunch.md`)._
