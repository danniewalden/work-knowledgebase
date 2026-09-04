---
title: "Source: Nick Tune — No rapport with a domain model you didn't code"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [tune-no-rapport-with-a-model-you-didnt-code]
raw_file: [raw/notes/tune-no-rapport-with-a-model-you-didnt-code.md]
tags: [verification-burden, domain-driven-design, vibe-modeling, comprehension-debt, self-report, focus]
---

# Source: Nick Tune — No rapport with a domain model you didn't code

LinkedIn post by **[[nick-tune]]** (**2026-08-28**), captured verbatim at
`raw/notes/tune-no-rapport-with-a-model-you-didnt-code.md` via logged-in Chrome (the headless watch
cannot render that feed; the date is derived from a relative age stamp, so accurate to the day). Short
post, no links, no evidence — but the most *upstream* statement of the verification problem in this
batch.

## Summary

Two claims, in order.

First, capability: "Working with coding agents to create and refine a domain model is painful because
they are not that good at it by default (that's the nice way of putting it)." Skills and guardrails
help "a bit" — and he has built those; see
[[nick-tune-enforced-application-architecture-agents-humans]].

Second, and the real point: **even when the output is fine, the modelling relationship is not.**

> "discussing and refining a domain model is not the same as writing the lines of code yourself. I
> don't feel as connected, I don't feel that the model is as deeply embedded in my mind as it would be
> if I wrote the code. And that means the domain model is going to be worse because I'm clearly
> missing some nuances that could lead to big modelling breakthroughs."

And the concession that makes it worth a page: **"At this point I'm struggling to see how to get the
same level of rapport with the model without actually writing the code. Maybe it's not even
possible."**

## Key points

- **He relocates the loss from *review* to *modelling*.** Everyone else in this batch is arguing about
  what to do with code an agent already wrote. Tune's claim is that the damage happens *before* the
  code: the modelling insight that came free from typing the model out does not arrive, so **the model
  itself is worse** — not merely less understood.
- **Typing was doing epistemic work.** The implicit premise is that writing the code is a mode of
  *thinking about the domain*, not a transcription step — which is precisely the premise
  [[spec-driven-development]] and the "describe, don't build" workflows assume away, and which
  [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill's "SDD and the Illusion of Known Scope"]] attacks from
  the implementation side ("implementation was never just typing — it's discovery and learning").
- **"Missing some nuances that could lead to big modelling breakthroughs"** names an *unobservable*
  cost. There is no diff to inspect, no test that fails, no metric that moves: the breakthrough that
  didn't happen leaves no trace. That is what makes it the hardest item in the batch to verify or
  refute — and the reason it cannot be answered by any of the other three remedies.
- **"Maybe it's not even possible"** is unusual in this literature: a tracked DDD practitioner stating
  an open problem with no proposed fix, from someone who normally ships a mechanism
  (Rivière, graph+memory+skills).

## Limits

- **THIN CAPTURE.** A short LinkedIn post: no evidence, no case, no example model, no comparison. It
  is a first-person report about the author's own felt connection to his own models.
- **IMPRESSION NOT MEASUREMENT, and unusually strongly so** — the claim is explicitly about a feeling
  ("I don't feel as connected") from which he *infers* a quality loss ("and that means the domain model
  is going to be worse"). The inference is not demonstrated; no worse model is shown.
- **Unfalsifiable as stated.** A missed modelling breakthrough is unobservable by construction; the
  KB should hold this as a **hypothesis with a named mechanism**, not a finding.
- Confounded with the first claim: if agents are "not that good at it by default," some of the felt
  loss may be output quality rather than lost rapport. He does not separate them.
- LinkedIn-derived date and text; canonical permalink recorded in the capture.

## Connections / contrast

- **[[verification-burden]]** — the **fourth position**, and the only one that says the other three are
  solving the wrong problem. Brewster accepts the debt, Laycock relocates review's functions earlier,
  Tornhill triages and substitutes tests + enforcement; Tune says none of that restores the
  understanding, because the understanding came from *writing*, and review was never where it lived.
  Note that he and Laycock share a diagnosis ("understand systems, not diffs") while disagreeing
  about whether her earlier-and-collaborative practices can supply it.
- **[[comprehension-debt]] — the modelling-side variant.** That page already holds the code side
  (unread code) and Dilger's requirements side (problems you described but didn't solve). This is the
  third face: **models you didn't build**. It is the closest thing in the KB to a statement that the
  debt may be *unpayable*, not merely unpaid.
- **[[domain-driven-design]] / [[vibe-modeling]]** — the sharpest available caution on
  agent-assisted modelling from a DDD name, and the counterweight to the vibe-modelling optimism the
  KB holds elsewhere. Also read against [[domain-discovery]] and [[event-storming]]: those are
  *collaborative* discovery formats, i.e. the pre-existing answer to "how do you get rapport with a
  model you didn't personally type" — a group already faces that problem, and event-storming exists
  because of it. Whether that generalises to a human/agent pair is exactly the open question.
- **[[event-modeling]] seam.** If rapport comes from *building the model*, then a modelling notation a
  human authors and an agent implements ([[model-as-code-vs-model-as-language]],
  [[event-modeled-agent-design]]) is a candidate answer to Tune's "maybe it's not even possible" — the
  human keeps the modelling act and delegates the typing. That is a KB hypothesis, not his suggestion,
  and it is the single most useful open question this capture raises for the focus area.
- **[[nick-tune-enforced-application-architecture-agents-humans]]** — note the tension inside his own
  work: build-enforced architecture guarantees the *shape* of code nobody read, but nothing about the
  build enforces modelling insight. He is candid that the guardrails only make agents "a bit better."
- **[[tornhill-compressed-cognition-cost-of-faster-coding]]** — Tornhill's prescription for recovered
  hours is "train as an end-user… master the problem domain," i.e. rebuild domain expertise away from
  the code. That is the closest thing in the batch to a reply to Tune, from someone not addressing him.
- Also: [[balanced-coupling]] and [[khononov-golden-age-of-modularity]] (Khononov's modelling-side
  neighbour), [[agent-legibility]], [[ai-readable-code]].

## Links

Entities: [[nick-tune]] · [[adam-tornhill]] · [[vlad-khononov]]. Concepts:
[[verification-burden]] · [[comprehension-debt]] · [[domain-driven-design]] · [[vibe-modeling]] ·
[[domain-discovery]] · [[event-modeling]] · [[model-as-code-vs-model-as-language]] ·
[[spec-driven-development]]. Related sources:
[[nick-tune-enforced-application-architecture-agents-humans]] · [[nick-tune-graphs-memory-skills-agents]] ·
[[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]] ·
[[tornhill-controlling-the-uncertainty-machine]] · [[willison-brewster-cannot-review-180000-lines]].

_Raw source: `raw/notes/tune-no-rapport-with-a-model-you-didnt-code.md`._
