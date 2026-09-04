---
title: "Source: Willison — Introducing wrapture (Dumpleton's agent-driven library)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [willison-introducing-wrapture]
raw_file: [raw/articles/willison-introducing-wrapture.md]
tags: [agentic-coding, vibe-modeling, testing, observability, short]
---

# Source: Willison — Introducing wrapture

Blogmark by **[[simon-willison]]**, 2026-08-31, relaying Graham Dumpleton's "Introducing wrapture" and its
follow-up "Unit testing with wrapture." Raw capture: `raw/articles/willison-introducing-wrapture.md`.
**Deliberately short page — one library announcement, one durable claim. Secondhand: the primaries at
grahamdumpleton.me were not captured.**

## Summary

**wrapture** is a young Python library (weeks old) from Graham Dumpleton — author of `wrapt`, `mod_wsgi`
and New Relic's Python agent — extending `wrapt`'s monkeypatching ideas so that the *same* wrapping
mechanism serves both **testing** (as an alternative to `unittest.mock`, with `on_call.returns(...)` and
`on_call.transforms_result(...)` bindings) and **tracing** (OpenTelemetry export, plus a purely
configuration-based mode that adds tracing to an existing project via a TOML stanza of `observe`
targets and `sink` outputs, with no code change). Dumpleton's framing: *"Attaching observation to code you do not control,
recording what flows through it, and doing so without disturbing the program being watched, is a problem I
have never really stopped thinking about."*

## Key points

**The reason this is in the KB is the authorship disclaimer, which is unusually careful and is a
SELF-REPORT ABOUT HIS OWN PROCESS:**

> "Every line of code and documentation in wrapture was written by an AI assistant working under my
> direction. I want to be upfront about that, and equally upfront about what it was not. **This was not
> vibe coding**, where a one-shot prompt produces a pile of generated code and the person driving hopes for
> the best because they lack the knowledge to judge what came back. Vibe coding has earned its bad
> reputation. I engineered wrapture carefully from the start. I have spent a long time in this particular
> corner of Python and knew exactly what the result needed to be, and **the AI was the means of producing
> it rather than the source of the design**."

Three things that makes it worth a page:

- **It states the distinction the KB draws with [[vibe-modeling|vibe coding]] vs [[agentic-coding]] in a
  practitioner's own words, and locates the boundary in *design authority*, not in tooling, review volume,
  or output quality.** "The means of producing it rather than the source of the design" is the crispest
  one-line statement of that boundary in the KB.
- **He grounds the claim in deep prior domain expertise** — *"a long time in this particular corner of
  Python"* (his words; the capture gives no duration). That is [[fritzsche-what-ai-changes-is-which-work-stays-hard]]'s and
  [[highsmith-practitioner-voice]]'s thesis instantiated: what he brought was the knowledge of what the
  result needed to be.
- Willison's own assessment is a hedge, not an endorsement: *"still a very young project — just a few
  weeks old — but it's off to a very promising start."*

## Limits

- **Secondhand** (Willison relaying Dumpleton) and the disclaimer is **the author's own account of his own
  process** — unverifiable, and the kind of claim everyone tells favourably about themselves. Do not
  promote it to evidence that agent-driven authorship *works*; the library's quality is untested, its age
  is weeks, and no defect, review or maintenance data exists.
- **Nothing is measured.** No time saved, no comparison, no baseline.
- The library itself is off-thread for this KB except as a Python-side [[agent-observability-and-evals]]
  tool; nothing in it is event-sourcing or Event-Modeling adjacent.

## Connections / contrast

- **Next to [[willison-claudes-new-system-prompt]]** (whose tracking system Fable 5.1 wrote end-to-end)
  and [[willison-sqlite-utils-4-mostly-written-by-fable]], this is the third late-2026 case in the KB of an
  experienced maintainer shipping an agent-authored library **under their own name and judgement**. The
  common factor in all three is a maintainer with deep prior ownership of the problem — which is a
  selection effect, not a demonstrated method.
- The tracing-without-touching-the-program idea is adjacent to [[agent-observability-and-evals]] and to
  the "attach observation to code you do not control" problem that the [[model-context-protocol]] tooling
  in this batch ([[miller-ai-assisted-production-support-with-critterwatch]]) solves at the operations
  layer rather than the call layer.

## Related

[[agentic-coding]] · [[vibe-modeling]] · [[simon-willison]] · [[agent-observability-and-evals]] ·
[[fritzsche-what-ai-changes-is-which-work-stays-hard]] · [[highsmith-practitioner-voice]] ·
[[willison-sqlite-utils-4-mostly-written-by-fable]]
