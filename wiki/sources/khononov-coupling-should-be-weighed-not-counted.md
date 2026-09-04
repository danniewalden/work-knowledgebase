---
title: "Source: Khononov — Coupling Should Be Weighed, Not Counted"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [khononov-coupling-should-be-weighed-not-counted]
raw_file: [raw/articles/khononov-coupling-should-be-weighed-not-counted.md]
tags: [coupling, balanced-coupling, coupling-taxonomy, metrics, substrate]
---

# Source: Khononov — Coupling Should Be Weighed, Not Counted

Article by **[[vlad-khononov]]** ("Rants on Software Design", vladikk.com, 2026-02-26). Raw capture:
`raw/articles/khononov-coupling-should-be-weighed-not-counted.md` — an **out-of-window backfill**
(2026-02, filed on the 2026-09-04 sweep), transcribed verbatim through the closing "P.S.".

**Markers that travel with every claim below.** **NOT INDEPENDENT:** Khononov authored the
[[balanced-coupling|Balanced Coupling]] model and *Balancing Coupling in Software Design* and runs
coupling.dev — this is the model's own author arguing for it, not external corroboration that Integration
Strength beats Ca/Ce/instability metrics. **IMPRESSION NOT MEASUREMENT:** "in my experience, chasing
those metrics never really made the design more modular" is a **practitioner self-report**, and the
1-outgoing/100-incoming component is a **constructed illustration, not a measured case**. **The post
presents no data.**

## Summary

A focused attack on **counting-based coupling metrics**. Static analysis tools count afferent (Ca) and
efferent (Ce) dependencies and combine them into an instability score `I = Ce / (Ce + Ca)`. Khononov's
objection is that the count is blind to **what flows through** a dependency: a component with 1 outgoing
and 100 incoming dependencies scores ~0.01 ("textbook stability"), yet if that one outgoing dependency
reaches into another component's **implementation details** while all 100 incoming ones go through stable
contracts, "the metric says: rock-solid stability. Reality says: ticking time bomb."

The alternative is to **weigh** each dependency by the *kind of knowledge* it shares — the **Integration
Strength** scale, a four-level ordinal in which each level down "removes an *entire category* of shared
reasons for change." Hence the epigraph ("Words should be weighed, not counted") and the conclusion that a
single intrusive dependency can cause more cascading change than a hundred contract-based ones.

## Key points

- **The four levels of Integration Strength**, strongest → weakest, in his own framing:
  - **Intrusive** — integration through implementation details (direct database access, private object
    manipulation, undocumented internal APIs). "You have to assume that *all* knowledge is shared"; the
    reasons for cascading change are "essentially unbounded." His canonical case: a microservice reading
    another microservice's database directly.
  - **Functional** — shifts from "how?" to "what": components implement closely related or identical
    business requirements, so a rule change forces them to change together (the same validation
    duplicated in frontend and backend; a spec change reflected in only one produces inconsistent
    behaviour).
  - **Model** — shifts from logic to structure: components share a domain model but not the logic
    implementing it (entities, relationships, concepts). When the team's *understanding* of the domain
    evolves, everyone sharing the model adapts.
  - **Contract** — lightest: only an integration contract is shared (API spec, event contract, DTO).
    "Restructure your internals? Rewrite your business logic? Evolve your domain model? No cascading
    changes."
- **The methodological point, not just the scale:** the model "focuses on what matters: the practical
  implications of a dependency. What kinds of shared **reasons for change** does it introduce?"
- **Why the tools count anyway:** "Static analysis tools count because counting is easy to automate. But
  easy to automate and useful are not the same thing. A metric that treats use of reflection to modify a
  private field and an API call as equivalent is likely to point you in the wrong direction."
- **Scope discipline for the KB:** this post covers **only the Integration Strength axis**. The
  three-dimension triad is stated in his companion piece three days earlier
  ([[khononov-ai-doesnt-fix-your-real-bottleneck]]) - do not source the triad here. Note also that in
  that post he names the first axis **"shared knowledge"**, not *strength*: "strength x distance x
  volatility" is the KB and book naming, not the wording of either February post.

## Connections / contrast

- **First-party confirmation of the KB's second-hand scale.** [[balanced-coupling]] and the
  [[coupling-research-note]] already carry the four-level Integration Strength table, reconstructed from
  the book's TOC and coupling.dev. This is Khononov **stating the four definitions himself in prose**,
  with a worked illustration for each level — the closest the KB now has to a first-party text on the
  scale (the research note's standing want). The mapping the research note recorded (intrusive ≈
  classical **content coupling**) is consistent with what he writes here, though he does not use the
  classical vocabulary.
- **Directly relevant to the KB's metric-based sources.** It is a **theoretical objection to
  count/score-based code analysis** of the kind [[adam-tornhill]]/CodeScene sells (see
  [[tornhill-codescene-unhealthy-code-agentic-token-cost]], whose figures are **VENDOR SELF-REPORT**).
  The two are not in direct contradiction — Tornhill's code-health measures are not Ca/Ce ratios — but
  Khononov's "easy to automate and useful are not the same thing" is the sharpest sceptical frame the KB
  has for *any* automatable design metric, including [[fitness-functions]] and
  [[fowler-bockeler-maintainability-sensors|maintainability sensors]]. Worth reading against them.
- **Sits at the modern end of [[coupling-taxonomy]]**, descending from [[larry-constantine]]'s 1974
  levels — the reason the KB keeps both pages.
- **Why it matters for the agent thread.** If an agent is asked to "reduce coupling," a counting metric is
  the thing it can most easily optimise and most easily game; the weighing model is the thing that
  requires domain judgement (his P.S. in the companion post: "that's not a prompting problem"). See
  [[agentic-coding]], [[ai-readable-code]], and his [[khononov-modularity-claude-code-plugin|Modularity
  Skills plugin]] — which encodes exactly this scale as an agent skill, and is itself unevaluated.
- Adjacent: [[business-capabilities]] · [[vertical-slice-architecture]] (maximize coupling inside a
  slice, minimize across — the same "right coupling, right place" instinct) ·
  [[dudycz-vertical-slices-ownership-and-external-dependencies]] (his narrow consumer-declared function
  types are Contract-level coupling by construction).

## Limits

- **No data at all**, by the author's own framing — one constructed illustration and one experience
  report. The claim that weighing "beats" counting is **argued, never tested**.
- **NOT INDEPENDENT** (see marker).
- The scale is **ordinal and judgement-based**; the post gives no procedure for classifying a real
  dependency, and no treatment of the **per-site → per-partition** scoring gap the
  [[coupling-research-note]] flagged as open.
- It also does not address the obvious rejoinder: an automated tool *can* approximate strength (direct DB
  access is detectable). The post treats automation as inherently counting-shaped.
- Out-of-window (2026-02); backfill, not a new development.

_Source: `raw/articles/khononov-coupling-should-be-weighed-not-counted.md`._
