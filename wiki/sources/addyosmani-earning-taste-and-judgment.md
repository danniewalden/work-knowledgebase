---
title: "Osmani — Earning taste and judgment"
type: source
created: 2026-07-27
updated: 2026-07-27
sources: [addyosmani-earning-taste-and-judgment]
raw_file: [raw/articles/addyosmani-earning-taste-and-judgment.md]
tags: [loop-engineering, ai-readable-code, spec-driven-development, taste, careers, focus]
---

# Osmani — Earning taste and judgment

[[addy-osmani|Osmani]]'s companion to his [[loop-engineering]] and [[addyosmani-own-the-outer-loop|outer-loop]]
pieces (addyosmani.com, 2026-07-14). Thesis: **"Taste used to be a byproduct of the reps. Agents took the
reps. So if you're junior you now have to go get the taste (and judgment) on purpose."** The durable,
ungradeable human contribution isn't getting better at problems with a known answer — it's **choosing what
to build and judging whether it's any good.** "Anything gradeable by someone else is getting automated."

## The setup

Almost all of an engineer's taste/judgment came from thousands of *reps* (boilerplate, bug fixes) — the path
junior→senior. Agents automate the reps, so that path breaks. He marshals 2026 labor data (recent-grad
underemployment ~41.5%; CS-grad unemployment elevated; junior tech postings down 34% since 2020 vs 19% for
senior; AI-exposed 22–25-year-olds −16% relative employment) **against** the optimistic aggregate (WEF: net
+78M roles by 2030) and reconciles them: **the net and the entry level are different questions** — senior
judgment roles grow while the first rung vanishes. Entry-level jobs were never just employment, they were a
**training system**; automating the learning stage "buys output now but leaves society gradually less capable
later." (Russinovich/Hanselman: agents help seniors while robbing juniors; the `sleep()`-to-hide-a-race
example a senior catches and a junior ships.)

## The two debts and the loop boundary

Restates the KB's shared seam: **"We now owe two debts: cognitive surrender and comprehension."** Wharton
(Shaw & Nave, 1,372 people / ~10k trials): people accepted *incorrect* AI output ~80% of the time, accuracy
−15 pts vs no-AI, confidence +12%. The agent runs the **inner loop** (investigate, implement, test, report);
the human owns the **outer loop** — worth-my-attention? verify (diffs, tests, logs, a short *why*) → approve
or block → carry the consequence. **"The boundary is evidence (my psalm)"** — the same inner/outer split as
[[addyosmani-own-the-outer-loop]], and the gap between the loops "is growing rapidly." [[andrej-karpathy|Kent
Beck]] cited: agents likely never possess taste (judgment), so humans supply it.

## Seven habits + four principles (the practitioner core)

Seven things to build taste on purpose: **read far more code than you generate**; keep a **"wrong log"** (one
sentence per agent mistake, patterns after 30 days); **do a few things the hard way** (protect collateral
learning; Karpathy on fundamentals — memory, views, storage — agents get wrong); go **deep on one system to
failure**; **specify and verify separately** ("specification quality is the biggest lever" — the
[[spec-driven-development]] seam); **build an eval/rubric** (correctness, maintainability, efficiency,
security, style) and **run it on 50 real AI PRs** to make your internal quality function explicit (the
grader/verification loop as a *personal calibration tool*); **calibrate autonomy per task** (up on cheap
reversible work, down on expensive failures — [[loop-engineering|back-pressure]] as a senior instinct). Four
principles for where durable value concentrates (optimize for scarce resources — "I can raise money in weeks,
I can't raise a reputation"): **finish the last mile** (the ungradeable 10–20%); **solve the hard version**
(Sutton's bitter lesson as career advice); **build in public near hard problems**; **be a T-shaped
generalist**. Cautions: [[simon-willison|Boris Cherny]] — you still need the craft (languages, compilers,
runtimes, system design); Anthropic's **paradox of supervision** (supervising an agent needs exactly the
skills that atrophy when you over-rely on it); [[simon-willison|Gergely Orosz]] — choose which muscles you let
atrophy (he uses AI for coding, zero for writing).

## Why it matters here

The clearest KB statement of the **ungradeable human residue** once loops automate execution — the positive
complement to the "stay the engineer" caveats in [[loop-engineering]], the taste/judgment side of
[[ai-readable-code]]/[[addyosmani-own-the-outer-loop|Answerability]], and it operationalizes the
personal-eval/rubric habit (a grader loop pointed at yourself). Caveat: a careers/labor essay leaning on
contested 2026 macro data (which he flags himself — "not purely an AI story," partly a post-2022 hiring
correction); marked 100% human-authored by Pangram.

## Connections

[[loop-engineering]] (inner/outer loop, back-pressure, the personal grader) · [[addyosmani-own-the-outer-loop]]
(same inner/outer frame) · [[addyosmani-loop-engineering]] · [[willison-understand-to-participate]] +
[[tornhill-ai-readable-code-series]] (comprehension/cognitive debt) · [[spec-driven-development]] (specify &
verify separately) · [[ai-readable-code]] · [[willison-directly-responsible-individuals]] (carry the
consequence).

_Source: [[addyosmani-earning-taste-and-judgment]] (raw/articles)._
