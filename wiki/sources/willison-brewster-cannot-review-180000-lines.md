---
title: "Source: Rick Brewster — \"I cannot possibly review 180,000 lines of code\" (via Willison)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [willison-brewster-cannot-review-180000-lines]
raw_file: [raw/articles/willison-brewster-cannot-review-180000-lines.md]
tags: [comprehension-debt, verification-burden, agentic-coding, coding-agents, vibe-coding, self-report, focus]
---

# Source: Rick Brewster — "I cannot possibly review 180,000 lines of code" (via Willison)

A **quotation post** by **[[simon-willison]]** (simonwillison.net, **2026-09-02**) carrying words by
**[[rick-brewster]]**, author of Paint.NET, from a Paint.NET forum thread. Raw capture:
`raw/articles/willison-brewster-cannot-review-180000-lines.md`. Willison's contribution is the
selection and framing; every quoted sentence is Brewster's.

## Summary

To make Paint.NET run on WINE, where Direct2D "will never be completed enough," Brewster shipped
**an internal, from-scratch, clean-room reverse-engineered rewrite of Direct2D**
(`PaintDotNet.Windows.Direct2D1.Managed.dll`), written — in his words — "by our good friend Claude,
without whom this would NOT have been possible and would NEVER have happened."

He then says the part the KB was missing a primary for:

> "Most of this code is, as they say, 'vibe coded.' By that I mean that it has not been thoroughly
> reviewed, it's more 'trust me bro' style. **I cannot possibly review 180,000 lines of code**, it's
> just way way *way* too much. For reference, the rest of Paint.NET is about 700,000 lines of code and
> I've been working on it for over 20 years."

This is [[comprehension-debt]] stated by the debtor, at the moment of taking it on, with no plan to
pay it down — and it is the blunt end of the [[verification-burden]] dispute this batch documents.

## Key points

- **The ratio is what makes it striking, and it is not a measurement.** ~180k agent-written lines added to a ~700k-line codebase one person has
  maintained for 20+ years: a ~26% increment of unreviewed code into a codebase whose entire history
  is one human's understanding. All three counts are **his own, stated in a forum post** — no tooling,
  method or repo audit is cited (**IMPRESSION NOT MEASUREMENT** — practitioner self-report).
- **"Not thoroughly reviewed" is not "not reviewed."** The same quote describes real, targeted
  intervention: "I had to babysit Claude quite a bit to make sure it did resource management correctly
  (for awhile it just wasn't doing the COM equivalent of `AddRef()` for reference counted objects,
  oops). I had to slap it a few times when I found some really bad design or architecture decisions."
  So the *practice* is spot inspection of high-risk seams — closer to
  [[tornhill-controlling-the-uncertainty-machine|Tornhill's uncertainty triage]] than to abdication —
  but Brewster claims no method, no test boundary and no deterministic enforcement behind it. He
  simply names the gap and ships.
- **Capability is uneven, and he says so.** "At times, Claude was working with the fury of 10 freshly
  unshackled Einstein genius-level 10x coders. And other times ... well, not so much." He is
  separately impressed by the agent's "clever and tireless reverse engineering work ... to figure out
  all the formulas needed for implementing Direct2D's built-in effects library" — a task with a
  **cheap external oracle** (does the effect render the same?), which is why it is exactly the shape
  of work an unread 180k lines can succeed at.
- **The task shape licenses the risk.** This is a *clean-room reimplementation of a documented,
  externally specified API* behind a feature flag (`/wine`), on an opt-in experimental path. The
  behavioural spec exists outside the code and outside Brewster's head. That is not the general case,
  and nothing in the quote generalises it.
- **A named position in the dispute:** review is not "expensive" here, it is *impossible*, and the
  answer is to accept the debt rather than restructure the practice. No other source in this batch
  takes that position.

## Limits

- **Practitioner self-report on his own project**, about his own unreviewed code — the one party with
  both the best access and the least distance. Line counts, review depth and the agent's
  contribution are all unverified.
- **A forum post relayed through a blog**, not an article or a study; Willison adds no analysis.
- **Single case, unusual shape**: solo maintainer, hobby-adjacent product, opt-in experimental target,
  a spec-defined reimplementation. Do not read it as a claim about enterprise codebases.
- No defect, incident, performance or maintenance data — the interesting number (what the unreviewed
  180k costs over the next two years) does not exist yet. Worth revisiting.
- The "10 Einstein 10x coders" line is a joke, not a productivity claim, and must not be promoted to
  one.

## Connections / contrast

- **[[verification-burden]]** — this is the extreme case on that page: the one where the volume has
  already passed any possible human read, admitted in public.
- **[[comprehension-debt]]** — the page's existing defence is "read the diffs." Brewster is the
  counter-example that shows the defence has a ceiling: at 180k lines it is not a choice you decline,
  it is a choice you no longer have. He also fits Dilger's incident-shaped worry recorded on
  [[software-factory]] ("production burning and no one there to navigate the code base").
- **Against [[laycock-maybe-we-shouldnt-be-reviewing-all-this-code|Laycock]]**: she argues the
  functions of review should move earlier (pairing, team design, [[fitness-functions]]); Brewster is a
  team of one, so none of her mechanisms are available to him — which is itself informative about the
  scope of her prescription.
- **With [[willison-more-than-just-code-review|Willison's own position]]**: Willison says
  line-by-line review was never the best verification instrument. Brewster supplies no substitute
  instrument at all, which is the difference between "verify another way" and "trust me bro."
- **Against [[khononov-value-of-90-percent-done-never-lower|Khononov's aphorism]]** that the value of
  99%-done "has never been lower" — Brewster shipped the 99% and named the missing 1% as review. (An
  inference of this page, not a claim either author makes.)
- **[[willison-conceptual-integrity-and-counting-lines-of-code]]** — Willison's "cognitive capacity is
  the new limiting factor, so load-balance it across a team" is exactly what a solo maintainer cannot
  do. Same author, same fortnight, and the pairing is the sharpest statement of the constraint.
- Also relevant: [[vibe-modeling]] (he uses "vibe coded" in Karpathy's original sense — no attention
  paid to how the code works), [[willison-vibe-engineering]] (the accountable counterpart he is
  explicitly *not* claiming), [[agentic-coding]], [[unattended-coding-agents]].

## Links

Entities: [[simon-willison]] · [[rick-brewster]] · [[anthropic]]. Concepts:
[[verification-burden]] · [[comprehension-debt]] · [[agentic-coding]] · [[vibe-modeling]] ·
[[attention-bottleneck]]. Related sources: [[willison-more-than-just-code-review]] ·
[[willison-conceptual-integrity-and-counting-lines-of-code]] ·
[[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]] ·
[[tornhill-controlling-the-uncertainty-machine]] · [[tune-no-rapport-with-a-model-you-didnt-code]].

_Raw source: `raw/articles/willison-brewster-cannot-review-180000-lines.md`._
