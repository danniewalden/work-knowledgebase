---
title: "Source: Simon Willison — Conceptual integrity and counting lines of code"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [willison-conceptual-integrity-and-counting-lines-of-code]
raw_file: [raw/articles/willison-conceptual-integrity-and-counting-lines-of-code.md]
tags: [attention-bottleneck, verification-burden, comprehension-debt, metrics, agentic-coding, focus]
---

# Source: Simon Willison — Conceptual integrity and counting lines of code

Blog post by **[[simon-willison]]** (simonwillison.net, **2026-08-19**) publishing two highlights from
his *Talking Postgres* podcast appearance with Claire Giordano ("How AI is changing software
development"), from a lightly edited transcript. Raw capture:
`raw/articles/willison-conceptual-integrity-and-counting-lines-of-code.md`. Two arguments, both
relevant here.

## Summary

**1. Lines of code, defended — because there is a ceiling.** Against the standard "LOC is a
meaningless productivity metric," he argues LOC becomes meaningful precisely because human output was
hard-capped: "In the before-times, a software engineer could produce a few hundred lines of
production-ready code per day — and 200 lines of working, debugged, production-level code is an
incredibly good day. Most days you'd produce 50 or 60." So "if agents let you produce a thousand lines
of debugged code, that really is a very meaningful improvement — **as long as the code is the same
quality: maintainable, tested, all of that.** You can get to that point with agents, but it takes a
huge amount of skill and knowledge and experience."

Then the constraint that matters for this batch. Asked why a company would need more than one
engineer:

> "the new limiting factor is **cognitive capacity**. I can churn out code a hundred times faster. **I
> don't have the cognitive capacity to stay on top of 100 times the amount of code.** So you still
> need a team of engineers, so you can **load balance that cognitive capacity across the team**."

**2. Conceptual integrity erodes because features got cheap.** Invoking *The Mythical Man-Month*:
well-designed software "has an integrity to it: there are no surprises in it, it covers exactly the
right domain of things, everything fits together and makes sense. That's so much harder with coding
agents, where you can have an idea for a feature, run a prompt, and five minutes later you've got the
feature. **Your software grows little weird bumps in funny different directions.**"

Giordano's analogy — which he then tells at length — is the **Winchester Mystery House**, 140 rooms
added for 40 years. "It's very easy to keep adding new rooms, because the cost of adding those rooms is
so much cheaper. What you end up with is something where the conceptual integrity falls apart — and
then it's harder to make decisions about it."

The diagnosis he lands on is **lost friction as lost discipline**: "It used to be that the discipline
was enforced on you by the amount of time it took. You'd come up with an idea for a crazy feature and
think 'yeah, but that would take me a week — I cannot justify that, so I'll forget about it.' If it
takes an hour, it's so much easier to justify."

## Key points

- **"Cognitive capacity" is named as the new limiting factor**, and it yields a *structural* remedy no
  one else in this batch proposes: **keep a team in order to distribute the understanding**. That is a
  third answer to the verification burden — not "read less" (Tornhill), not "move review earlier"
  (Laycock), but **spread the reading across more heads**.
- **The bus-factor aside is the counterpart**: "a team of one is a very badly designed team" — which
  is exactly the configuration in
  [[willison-brewster-cannot-review-180000-lines|Brewster's 180,000 unreviewed lines]].
- **LOC is rehabilitated only under a quality proviso** ("as long as the code is the same quality:
  maintainable, tested") and an experience proviso ("takes a huge amount of skill"). Quoting the LOC
  defence without both provisos misrepresents it.
- **Conceptual integrity is a distinct failure mode from unread code.** Comprehension debt is code
  nobody has read; conceptual-integrity loss is a *shape* nobody chose — each individual room
  justified, the house incoherent. Agent speed produces both, by the same mechanism (removed cost), and
  no amount of per-diff review catches the second, since every diff is individually defensible.
- **Friction was doing governance work.** The pre-AI schedule was an implicit filter on feature scope;
  it is gone, and nothing has replaced it. Cf. [[tornhill-compressed-cognition-cost-of-faster-coding|
  Tornhill's "manual coding had a built-in pacing mechanism… and it's now gone"]] — the same
  observation about the same lost friction, one about scope discipline and one about cognitive recovery.

## Limits

- **A lightly edited podcast transcript** (his prompt to Claude: "very minor edits to remove
  disfluencies") — conversational argument, not a written thesis.
- **All numbers are practitioner rules of thumb, not measurements**: a few hundred lines per day, 200
  as an incredibly good day, most days 50 or 60, a thousand lines with agents, "a hundred times faster."
  No source, no dataset, no definition of "production-ready." **IMPRESSION NOT MEASUREMENT** — none of
  these may be promoted to figures on any page.
- "A hundred times faster" is rhetorical emphasis inside an argument about *cognitive* limits; it is
  not a productivity claim and directly contradicts the felt-vs-measured gap relayed in
  [[tornhill-compressed-cognition-cost-of-faster-coding]]. Hold both.
- Conceptual integrity is asserted as an observed trend with **no example, project or measurement** —
  Brooks's concept applied by analogy.
- He notes himself that the Winchester psychic story is disputed by credible sources; the analogy is
  Giordano's, not evidence.

## Connections / contrast

- **[[attention-bottleneck]]** — the KB's primary for the phrase *cognitive capacity as the limiting
  factor*, and the load-balance-across-the-team remedy. Sits directly beside
  [[laycock-the-conductor-developer|Laycock's "human attention is now the bottleneck"]] (same
  fortnight, unrelated authors, near-identical premise) and
  [[tornhill-compressed-cognition-cost-of-faster-coding|Tornhill's decision-density mechanism]].
  Willison distributes the scarce resource; Laycock re-skills the individual to spend it better;
  Tornhill protects it by refusing parallelism.
- **[[verification-burden]]** — the *distribute it* position. Also the only place in the batch where
  team size is treated as a verification instrument.
- **[[comprehension-debt]]** — "I don't have the cognitive capacity to stay on top of 100 times the
  amount of code" is the debt stated as a hard personal ceiling, and the conceptual-integrity half
  adds a **design-coherence** face that page did not carry before this source. Worth a section there
  (and, if a
  second source arrives, its own page).
- **[[willison-more-than-just-code-review]]** — three days later, the same argument narrowed to
  verification. Read the pair as one position.
- **[[ai-readable-code]] / [[tornhill-clear-design-principles-agentic-age]]** — "no surprises in it…
  everything fits together and makes sense" is conceptual integrity; *Conceptual alignment* is the C in CLEAR. Two vocabularies
  for one property, one from Brooks and one from design-for-agents.
  [[tornhill-beyond-lambdas-raising-the-abstraction-level]] is the code-level version of the same
  instinct.
- **[[software-factory]] / [[loop-engineering]]** — the cheap-features mechanism is the dark factory's
  engine; this is the argument that the factory erodes *design coherence* even when every unit of
  output passes. Also [[fitness-functions]], the standing candidate for replacing the lost friction
  with a deliberate constraint.
- Note for the metrics thread: [[adam-tornhill]] has publicly jabbed at "productivity mistaken for
  lines of code produced" ([[tornhill-five-programming-books-that-changed-how-i-think]]). Willison's
  hard-ceiling defence of LOC is the KB's counter-position, and the two have never engaged.

## Links

Entities: [[simon-willison]] · [[adam-tornhill]] · [[rachel-laycock]]. Concepts:
[[attention-bottleneck]] · [[verification-burden]] · [[comprehension-debt]] · [[ai-readable-code]] ·
[[agentic-coding]] · [[software-factory]] · [[fitness-functions]]. Related sources:
[[willison-more-than-just-code-review]] · [[willison-brewster-cannot-review-180000-lines]] ·
[[laycock-the-conductor-developer]] · [[tornhill-compressed-cognition-cost-of-faster-coding]] ·
[[tornhill-clear-design-principles-agentic-age]].

_Raw source: `raw/articles/willison-conceptual-integrity-and-counting-lines-of-code.md`._
