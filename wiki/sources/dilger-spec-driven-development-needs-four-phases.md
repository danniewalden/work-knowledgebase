---
title: "Dilger — Spec-Driven Development needs 4 phases"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [dilger-spec-driven-development-needs-four-phases]
raw_file: [raw/notes/dilger-spec-driven-development-needs-four-phases.md]
tags: [spec-driven-development, event-modeling, method, focus]
---

# Dilger — Spec-Driven Development needs 4 phases

LinkedIn post by **[[martin-dilger]]**, 2026-08-29. Raw capture:
`raw/notes/dilger-spec-driven-development-needs-four-phases.md`.

## The argument

> 1. Idea → Intent
> 2. Intent → Spec
> 3. Spec → Code
> 4. Code → Operations & Maintenance

> "Most frameworks and handbooks like Kiro, SpecKit and also Anthrophics latest Handbook on Software SDLC
> - focus almost exclusively on 3) … Leaving out 75% of the work, that needs to be done. that's why you
> constantly struggle."

His difficulty ranking: **1 and 4 are the hard ones**; 2 "is mechanical if 1) is done right"; 3 is "the
easiest of them all." And the test: *"You are not doing SDD if you don't have an answer to 1) or 4)."*

## Why it matters here

**It reframes the whole SDD critique cluster as a scoping error rather than a method error.** The four
captured critics all attack phase 3's artifacts — [[gojko-adzic]] on specs being scope-of-work not
specification, [[birgitta-bockeler]] on the taxonomy and the MDD parallel, Zaninotto on markdown
bureaucracy, Eberhardt on the ~10x cost. Dilger's counter is that they are all evaluating the phase the
tools happen to implement, and that the phase is the easy one. Whether that is a real reframing or a
convenient deflection is the interesting question — it is unfalsifiable as stated, since any SDD failure
can be attributed to a missing phase 1.

Two connections the KB can make that the post does not:

- **Phase 1 is where [[event-modeling]] claims to live** — idea to intent, worked out collaboratively
  before anything is written down as spec. That is the "front half" argument of
  [[dilger-spec-driven-tools-need-event-modeling-front-half]] restated as a numbered pipeline.
- **Phase 4 is almost entirely absent from this KB.** Operations and maintenance of agent-built systems
  is a gap no captured source addresses, and it is the phase he calls hardest alongside phase 1. Worth
  chasing.

Note the alignment with [[gojko-adzic]]'s independent complaint that Spec Kit lacks a **scoping phase** —
different vocabulary, adjacent diagnosis, neither citing the other.

## Caveats

- Very short and assertive; no evidence, no worked example of phases 1 or 4.
- Vendor-adjacent: the missing phases are the ones his platform and consulting sell.
- "Anthrophics" is his typo, preserved in the raw capture.

## Related

[[spec-driven-development]] · [[event-modeling]] · [[triplet-architecture]] · [[martin-dilger]] ·
[[dilger-spec-driven-tools-need-event-modeling-front-half]] · [[gojko-adzic]] ·
[[model-as-code-vs-model-as-language]]
