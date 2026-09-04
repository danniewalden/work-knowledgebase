---
title: "Source: Simon Willison — More than just code review"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [willison-more-than-just-code-review]
raw_file: [raw/articles/willison-more-than-just-code-review.md]
tags: [verification-burden, agentic-coding, agentic-engineering, code-review, definitions, focus]
---

# Source: Simon Willison — More than just code review

Short-form note post by **[[simon-willison]]** (simonwillison.net, **2026-08-22**), captured in full at
`raw/articles/willison-more-than-just-code-review.md`. Four sentences; tagged `code-review`,
`agentic-engineering`. The direct continuation of his Aug-19
[[willison-conceptual-integrity-and-counting-lines-of-code|conceptual-integrity / lines-of-code piece]],
narrowing that argument to the **verification** half of the loop.

## Summary

The whole post, in his words:

> "The key skill required to make productive use of coding agents is being able to **confidently
> instruct** them on how to make changes and then **confidently verify** that those changes have been
> applied in the correct way.
>
> Sometimes this involves reviewing every line of code they have written, but there are other ways to
> achieve that goal. **Eyeballing every line of code has never been the most effective way to validate
> a chance to a piece of software.**"

(The typo "a chance to a piece of software" is his; preserved verbatim in the capture.)

## Key points

- **A two-part definition of the core skill: instruct confidently, verify confidently.** Both halves
  are load-bearing, and the second is the one the KB was under-served on — most of the
  [[loop-engineering]] material is about the instruct half.
- **Line-by-line review is demoted to one instrument among several**, and — the sharper claim — it
  **never** was the best one: "has never been the most effective way to validate a chance [sic] to a
  piece of software." This is a
  claim about software engineering generally, not about agents. Agents merely removed the option of
  pretending otherwise.
- **"Sometimes this involves reviewing every line" keeps the instrument on the shelf** — he does not
  abolish reading code, he refuses to make it the definition of verification. That is a *triage*
  position, arrived at from first principles rather than from a workflow.
- The post names no alternative instruments. Tests, types, staged rollout, manual QA, preview
  environments and evals are all candidates from his own earlier writing
  ([[willison-vibe-engineering]], [[willison-designing-agentic-loops]]) — but this post does not list
  them, and the KB should not attribute a list he didn't give.

## Limits

- **A four-sentence note**: an assertion of principle with no argument, evidence, example or method.
  Its value is as a crisp, citable statement of a position, not as support for one.
- No definition of "confidently verify" and no criterion for when reading every line *is* required —
  the gap [[tornhill-controlling-the-uncertainty-machine|Tornhill's uncertainty rule]] fills.
- Practitioner assertion from a widely-read blogger, not measurement. He has a stake in the
  agentic-engineering vocabulary he is building (see the tag), though no commercial one.

## Connections / contrast

- **[[verification-burden]]** — the cleanest one-line statement of the position that *verification ≠
  review*, and the pivot the whole page turns on. Willison states it; Tornhill builds it; Laycock
  organises it; Brewster fails to do it.
- **Converges with [[tornhill-controlling-the-uncertainty-machine|Tornhill]] two days later**, with no
  cross-citation: "we don't need to read all AI-generated code" and "eyeballing every line has never
  been the most effective way to validate" are the same claim from a Substack code-health voice and a
  blog practitioner voice. Independent convergence is the strongest thing this batch has.
- **[[willison-directly-responsible-individuals]]** — the accountability floor under it: you may change
  the instrument, you may not move the responsibility. Same for
  [[addyosmani-own-the-outer-loop|Osmani's Answerability]].
- **Against [[osmani-agentic-code-review-skill-five-axes|Osmani's review skill]]**: Osmani's answer to
  the same problem is to make *the review* better and automated ("the review is your quality gate").
  Willison's is that the gate was never the right instrument. Both August 2026.
- **[[loop-engineering]]** — fills the verify seam of the loop, and pairs with the
  [[willison-fireside-chat-claude-code-team|Claude Code team's]] production practice of moving review
  onto automated reviewers plus eval sets: that is one concrete "other way."
- **[[given-when-then]] / [[slice]]** — the Event-Modeling seam the capture note flags: a slice's
  given/when/then is exactly an "other way" of verifying behaviour without eyeballing every line, and
  the reason this batch lands on the focus area rather than beside it.
- **[[willison-brewster-cannot-review-180000-lines]]** — published eleven days later by the same author
  and the reason both belong in the KB: Brewster is what "there are other ways" looks like when nobody
  supplies one.

## Links

Entities: [[simon-willison]] · [[adam-tornhill]] · [[addy-osmani]]. Concepts:
[[verification-burden]] · [[agentic-coding]] · [[loop-engineering]] · [[given-when-then]] ·
[[comprehension-debt]]. Related sources:
[[willison-conceptual-integrity-and-counting-lines-of-code]] ·
[[willison-brewster-cannot-review-180000-lines]] · [[willison-vibe-engineering]] ·
[[willison-agentic-engineering-patterns]] · [[tornhill-controlling-the-uncertainty-machine]] ·
[[osmani-agentic-code-review-skill-five-axes]].

_Raw source: `raw/articles/willison-more-than-just-code-review.md`._
