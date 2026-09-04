---
title: Colin Eberhardt
type: entity
created: 2026-09-04
updated: 2026-09-04
sources: [eberhardt-putting-spec-kit-through-its-paces]
tags: [spec-driven-development, agentic-coding, person, focus]
---

# Colin Eberhardt

**CTO of [[scott-logic]]**, a UK software consultancy, and author of the KB's most instrumented
hands-on [[spec-driven-development|SDD]] trial ([[eberhardt-putting-spec-kit-through-its-paces]],
2025-11-26). Until 2026-08-31 the wiki knew of him only as an unnamed "Scott Logic SpecKit trial"
reached second-hand through [[ng-spec-driven-development-is-waterfall-in-markdown|Ng]].

**Method:** deleted a ~1,000-line feature from his own hobby PWA (KartLog — go-kart race data; JS,
Firestore, SvelteKit) and rebuilt it with GitHub Spec Kit + Copilot, committing and timing every step,
then compared against his ordinary iterative workflow.

**Findings that travel:** 33m30 agent time, 689 loc, **2,577 lines of markdown**, 3.5 hrs review, and a
broken dev server — against 8m agent time, 1,000 loc, no markdown, 24 min review and no bugs his usual
way. *"Around ten times faster"* without SDD — **IMPRESSION NOT MEASUREMENT**: his own words, n=1, one
hobby app, one toolkit, no control for ordering or for the fact that he had already built the feature
once. Never render it as a rate or a benchmark. The instrument readings are real but come from **one
self-instrumented run with no repetition**, and the Tasks step's statistics block **duplicates the Plan
step's verbatim** in the original, so per-step totals are approximate and Tasks is effectively
unreported.

**A figure this KB had wrong, corrected here.** The *"2,500 lines of Markdown in the spec phase"* the
wiki once carried was wrong: **2,577 is the cumulative total for the whole feature**; Specify alone was
**230** lines; **Plan** was the bloated step at **2,067**.

**His argument, and it puts him in the model-as-code camp:** *"Code is law because it is formal language
you can reason about… Specifications, or at least ones expressed in the markdown format of Spec Kit,
lack this formality. They are not a law I would put my trust in."* Plus: code is now cheap and
disposable, so SDD fails to capitalise on the one thing agents changed; and specs are point-in-time
artifacts rarely revisited — the only argument in the KB against **spec-anchoring itself**, independent
of notation. He is not anti-documentation: architectural decisions and *why* are worth keeping
([[adr]], [[decision-trace]]).

**Hedges he states himself, and which should travel with the figures:** Spec Kit is immature; *"I am
willing to entertain the possibility that I am simply just using it wrong"*; he echoes
[[birgitta-bockeler|Böckeler's]] *"I wasn't quite sure what size of problem to use it for"*; and he
wonders whether an architect-reviewer "vibe engineer" is even the target audience. Verdict: *"an
interesting concept, a radical idea… But I don't consider it a viable process, at least not in its
purest form."* **He rejects the purest form while defending the debate — do not file him as a flat
anti-SDD voice.** One further caveat on independence: he is CTO of a consultancy that sells development
services.

_Related: [[scott-logic]] · [[spec-driven-development]] · [[model-as-code-vs-model-as-language]] ·
[[agentic-coding]] · [[vibe-modeling]] · [[gojko-adzic]] · [[francois-zaninotto]]._

_Source pages: [[eberhardt-putting-spec-kit-through-its-paces]]._
