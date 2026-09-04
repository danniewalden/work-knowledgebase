---
title: Rick Brewster
type: entity
created: 2026-09-04
updated: 2026-09-04
sources: [willison-brewster-cannot-review-180000-lines]
tags: [person, agentic-coding, comprehension-debt, verification-burden, self-report]
---

# Rick Brewster

Author and maintainer of **Paint.NET**, the Windows raster image editor, which he has worked on for
**20+ years** (~700,000 lines by his own count). He is in this KB for one reason: the bluntest primary
statement anywhere in it of the [[verification-burden]] at the point where it becomes impossible.

To get Paint.NET running under WINE — where Direct2D "will never be completed enough for Paint.NET's
use" — he shipped an internal, from-scratch, **clean-room reverse-engineered rewrite of Direct2D**
(`PaintDotNet.Windows.Direct2D1.Managed.dll`, behind a `/wine` flag), *"written by our good friend
Claude, without whom this would NOT have been possible and would NEVER have happened."* And then, on the
Paint.NET forums (quoted by [[simon-willison]],
[[willison-brewster-cannot-review-180000-lines]], 2026-09-02):

> *"Most of this code is, as they say, 'vibe coded.' By that I mean that it has not been thoroughly
> reviewed, it's more 'trust me bro' style. **I cannot possibly review 180,000 lines of code**, it's
> just way way *way* too much."*

He is not describing abdication so much as unmethodical triage: he babysat resource management ("for
awhile it just wasn't doing the COM equivalent of `AddRef()`"), "slapped it a few times" over bad
architecture decisions, and was impressed by the agent's reverse-engineering of Direct2D's effect
formulas — a task with a cheap external oracle. What he offers no substitute for is *systematic*
verification: no executable spec, no test boundary, no deterministic enforcement — which is what
separates his position from [[adam-tornhill]]'s on [[verification-burden]], and what makes him the
extreme case on [[comprehension-debt]] and [[software-factory]].

**Marker.** Everything the KB has about him is a **practitioner self-report about his own project and
his own unreviewed code**: the line counts (180k / 700k / 20 years) are his, from a forum post, with no
tooling or audit cited, and "it has not been thoroughly reviewed" is stated by the author of the
unreviewed code. **IMPRESSION NOT MEASUREMENT**, and the marker travels with the figures. His case is
also unusually shaped — solo maintainer, opt-in experimental target, and a reimplementation of a
*documented* API, so the behavioural spec lives outside the code. Not a watch target; one capture.

## Related

[[verification-burden]] · [[comprehension-debt]] · [[software-factory]] · [[attention-bottleneck]] ·
[[vibe-modeling]] · [[agentic-coding]] · [[simon-willison]] · [[anthropic]]

_Source pages: [[willison-brewster-cannot-review-180000-lines]]._
