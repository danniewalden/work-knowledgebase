---
title: "Source: Eberhardt — Putting Spec Kit Through Its Paces: Radical Idea or Reinvented Waterfall?"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [eberhardt-putting-spec-kit-through-its-paces]
raw_file: [raw/articles/eberhardt-putting-spec-kit-through-its-paces.md]
tags: [spec-driven-development, agentic-coding, controversy, measurement, focus]
---

# Source: Eberhardt — Putting Spec Kit Through Its Paces: Radical Idea or Reinvented Waterfall?

Blog post by **[[colin-eberhardt]]** (CTO, [[scott-logic]]), **2025-11-26**, CC BY-NC-SA 4.0. The
**hands-on trial** the KB's SDD critique cluster has leaned on hardest — and until 2026-08-31 the
wiki's most load-bearing single-source dependency, reached only second-hand through
[[ng-spec-driven-development-is-waterfall-in-markdown|Ng]]. Raw capture:
`raw/articles/eberhardt-putting-spec-kit-through-its-paces.md`.

Method: he **deleted an existing feature** from his own hobby PWA (KartLog, go-kart race data — JS,
Firestore, SvelteKit, SMUI), ~1,000 lines removed, then rebuilt it with GitHub Spec Kit + Copilot
(Claude Sonnet 4.5), committing every step. Chosen deliberately because *"I could confidently write an
unambiguous specification – because I'd already built it."*

## Summary

Spec Kit worked, and cost far more than it returned. Per-step instrumentation of the whole
Constitution → Specify → Plan → Tasks → Implement run, then the same feature-class of work done his
usual way, then a critique in five parts. Verdict: *"I see Specification Driven Development as an
interesting concept, a radical idea, a subject of lively, interesting and healthy debate. But I don't
consider it a viable process, at least not in its purest form, as exemplified by Spec Kit."*

## Key points — the numbers, per step

Feature 1 (circuit CRUD + data-model integration):

| Step | Agent time | His review time | Markdown |
| --- | --- | --- | --- |
| Constitution | 4 min | 5 min | 161 lines |
| Specify | 6 min | 15 min | 230 lines |
| Plan | 8m30 | 2 hours *("might not have been needed")* | 2,067 lines |
| Tasks | (the raw repeats the Plan block's figures verbatim — the Tasks step is described only as a 66-step list) | | |
| Implement | 13m15 | 30 min | 689 loc |
| **Total** | **33m30** | **3.5 hrs** | **2,577 lines md, 689 loc** |

Feature 2 (geolocation): 23m30 agent, ~300 loc, **2,262 lines of markdown**, ~2 hrs review.

His ordinary approach, same class of work: **8 min agent time, 1,000 loc, no markdown, 15 min code
review, 9 min functional test and fixes — and no bugs.**

- **The "~10x" figure, stated precisely.** *"The simple fact is I am a lot more productive without SDD,
  around ten times faster."* **IMPRESSION NOT MEASUREMENT** — his own words, one person, one hobby
  project, one toolkit, no control for ordering or familiarity. The KB must not render it as a datum or
  a rate.
- **Correction the KB already applied and this page confirms:** the "2,500 lines of Markdown in the
  spec phase" the wiki carried until 2026-08-31 was wrong. **2,577 is the cumulative total** for the
  whole feature; **Specify alone was 230 lines**, and **Plan was the bloated step at 2,067**.
- **The plan step's contents are the concrete complaint:** a 444-line module contract *"4x the length
  of the actual module itself"*, a 395-line data model, a 285-line plan restating the tech stack, a
  500-line quick start, and a **406-line research document** whose justifications restate the obvious
  (*"why it is using the SMUI library? erm … because every other page uses that!"*).
- **The dev server didn't start.** The implementation had *"a small, and very obvious, bug"* —
  `circuitsData` never populated from the datastore — fixed by pasting the error into chat *"(vibe
  coding style!)"*. And the process has no answer for it: SDD says clarify the spec and regenerate, but
  *"how to express this bug from a specification perspective? … I asked Copilot, and it concurred, this
  isn't an issue with the spec."* He links the open Spec Kit discussion on exactly this.
- **"Code *is* the law" — his central argument, and the sharpest formal-language claim in the
  cluster.** *"Code is law because it is formal language you can reason about. You can test it. You can
  prove it is right or wrong. Specifications, or at least ones expressed in the markdown format of Spec
  Kit, lack this formality. They are not a law I would put my trust in."*
- **Faux context.** Spec Kit invented rationale — *"Karting users need to log data trackside on mobile
  devices, often with gloves"* — quoted verbatim as the exemplar of AI *"detail that fundamentally
  lacks depth of value."*
- **Specs are point-in-time.** *"In most development processes specifications are a point-in-time tool
  for steering implementation. Once complete, and fully tested, how often do you re-visit a user
  story?"* He is explicitly **not** anti-documentation: architectural decisions and *why* are worth
  capturing — code gives the what, not the why (cf. [[adr]], [[decision-trace]]).
- **"Are agents better at writing markdown or code?"** Code is a far larger share of training data and
  a language models can reason about, so *"asking an agent to write 1000s of lines of markdown rather
  than just asking it to write the code is a misuse of this technology."* He concedes this argument is
  not compelling on its own.
- **"Teaching agents to suck eggs."** Spec Kit's value is a bunch of smart prompts, competing directly
  against frontier labs' own investment in agent planning — and prompt frameworks date almost
  immediately (his worked example: Harper Reed's Feb-2025 codegen workflow already *"feels very
  dated"*).
- **Code is now cheap, and SDD doesn't exploit that.** *"We can create it quickly and throw it away
  just as fast. Spec Kit, and SDD, don't capitalise on this."*
- **He does make the waterfall argument** — unlike Adzic (title question only) and Tornhill (declines it
  outright): a section headed *"A return to waterfall?"* concludes *"Spec Kit drags you right back into
  the past!"*, on the ground that AI makes iteration faster, not slower.

## Limits

- **One hobby app, one framework, n=1, self-instrumented, no blinding, no repetition.** He *is* the
  author of both arms of the comparison and had already built the feature once — which cuts *toward*
  SDD on spec quality and *against* it on the baseline arm's speed.
- The 2-hour Plan and Tasks review times are annotated by him as *"might not have been needed"*, and
  the raw shows the Tasks step's statistics block **duplicating the Plan step's numbers verbatim** — so
  the per-step totals should be read as approximate and the Tasks line as unreported.
- **The source contradicts itself on two line counts and the table above follows the statistics blocks.**
  His prose calls the constitution *"a 189-line markdown file"* where the step statistics say **161**, and
  calls the specification *"a 189-line specification"* where the statistics say **230** (the prose figure
  may predate his edits to each file). Both figures are in the raw; neither is reconciled there.
- **He states his own defences** and they should travel with the figures: Spec Kit is immature and
  evolving; *"I am willing to entertain the possibility that I am simply just using it wrong"*; he
  echoes Böckeler's *"I wasn't quite sure what size of problem to use it for"*; and he wonders whether a
  "vibe engineer" who architects and reviews is even the target audience — *"Perhaps Spec Kit is for
  the vibe coders? For the product owners? For the people who don't write or fully understand code?"*
- Five images (including both process timelines) are noted inline in the raw, not reproduced.

## Connections / contrast

- **Answers a standing open question on [[spec-driven-development]], and against the thesis.** This is
  the KB's only figure on the *cost* side of "the spec is the work", and it points the opposite way
  from [[dilger-faros-ai-report-amplifies-unclear-requirements]]. It remains an impression. And the
  question it does **not** answer is the one that matters for this KB's focus: nothing comparable exists
  for *model-first* SDD as [[martin-dilger]] practises it, so the 10x indicts document-generating
  toolchains and cannot yet be transferred to [[event-modeled-agent-design]].
- **"Code is the law" puts him in [[jeremy-miller]]'s camp, not Dilger's** — and gives
  [[model-as-code-vs-model-as-language]] its clearest *empirical* statement of the model-as-code case:
  markdown lacks formality, so trust the artifact you can test. Note Dilger agrees code is a formal
  language and objects that it is formal about the wrong thing (implementation, not behaviour over
  time), so this is a genuine collision, not a terminological one.
- **His "code is now cheap, throw it away" line is the direct antagonist of "the spec is the work"**:
  if code is disposable, the artifact worth keeping is the *decision record*, not the requirement —
  which is [[decision-trace]]'s position arrived at from the measurement side.
- **With [[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler]]:** he cites her spec-first /
  spec-anchored / spec-as-source ladder and classifies Spec Kit as **spec-as-source**, the purest form
  — the same form [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill]] restricts his
  own critique to. All three sceptics agree the strong form is the target.
- Sceptic cluster: [[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]] ·
  [[zaninotto-spec-driven-development-waterfall-strikes-back]] ·
  [[ng-spec-driven-development-is-waterfall-in-markdown]].

_Related: [[colin-eberhardt]] · [[scott-logic]] · [[spec-driven-development]] ·
[[model-as-code-vs-model-as-language]] · [[agentic-coding]] · [[vibe-modeling]] · [[decision-trace]]._
