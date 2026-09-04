---
title: "Source: Adam Tornhill — Beyond Lambdas: Raising the Abstraction Level of Functional Code"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [tornhill-beyond-lambdas-raising-the-abstraction-level]
raw_file: [raw/articles/tornhill-beyond-lambdas-raising-the-abstraction-level.md]
tags: [ai-readable-code, agent-legibility, refactoring, naming, focus]
---

# Source: Adam Tornhill — Beyond Lambdas: Raising the Abstraction Level of Functional Code

Refactoring walkthrough by **[[adam-tornhill]]** on *Code for Humans and Machines* (**2026-09-01**).
Raw capture: `raw/articles/tornhill-beyond-lambdas-raising-the-abstraction-level.md`. Standfirst:
*"Good software design raises the abstraction level until the code communicates the domain rather than
the mechanics."* The newest instalment of the walkthrough series indexed at
[[tornhill-ai-readable-code-series]] — and the code-level companion to the review-burden argument he
makes the same fortnight.

## Summary

**The asymmetry he builds on:** "The nice thing about lambdas is that they optimize for **writing**
code… The *bad* thing about lambdas is that they optimize for writing code. They do so at the expense
of **reading** code, which is arguably a much more frequent activity."

The worked example, in Java. Before:

```
rolls.stream().map(roll -> roll + 2).filter(roll -> roll >= 15).sum();
```

"It's a mere 3 lines of code, and the mechanics of each one is trivial. Yet the purpose, intent, and
business rules remain opaque. It could be anything." After — the lambdas named as domain methods:

```
rolls.stream().map(AttackRoll::applyStrengthModifier).filter(AttackRoll::isSuccessfulHit).sum();
```

"no longer a stream of seemingly random operations. Instead it communicates the concepts and rules from
the domain." (Dungeons & Dragons.) The new methods are "trivial one-liners" — private static methods,
or a private class if related abstractions cluster; module-level functions in Python or Clojure.

**On the cost:** more lines of code, and he accepts it — "Abstractions can be simple. Ridiculously
simple. Abstractions **don't have to be re-used** to motivate their existence. Lines of code are not a
finite resource." His test: **"if it elevates the level of the code, then it has earned its rights."**
He notes the personal reversal: 20 years of functional programming, style "gradually migrated away from
lambdas," because "naming functions — even those trivial one-liners — makes a large difference when
returning to code you wrote months or years earlier."

**The Clojure step further** — name the *pipeline elements*, not just the lambdas:

```
(->> rolls with-strength-modifier successful-hits ->damage)
```

"the code now reads like a story, telling the rules of the domain." The line the piece will be quoted
for: **"Anonymous functions are anonymous thoughts."**

**Why it matters, in his framing:** *"Optimize for reconstruction work."* New tasks arrive "within the
context of an existing codebase. This is where proper abstractions pay off by **limiting the necessary
reconstruction work**. And the closer our abstractions reflect the problem domain, the easier that will
be." Explicitly extended to agents via [[tornhill-clear-design-principles-agentic-age|the CLEAR
principles]]: "We will all do a better job when the code's purpose is expressed structurally. Small
abstractions add up, so make them a habit."

## Key points

- **Naming is the intervention, again** — consistent with [[tornhill-opinionated-guide-to-naming]]
  (naming as cognitive compression, the highest-leverage move). Here the target is a construct that
  *by design* has no name.
- **"Anonymous functions are anonymous thoughts"** — the memorable form of the claim that unnamed
  structure is unrecorded intent, i.e. the *Explicit intent* leg of CLEAR at expression level.
- **LOC is explicitly not the cost function.** "Lines of code are not a finite resource" is a direct,
  probably unintended, counterpoint to
  [[willison-conceptual-integrity-and-counting-lines-of-code|Willison's]] hard-ceiling defence of LOC
  as a productivity indicator. Two on-thread authors, opposite stances on what LOC measures, no
  engagement between them.
- **Reuse is not the justification for an abstraction** — a small but load-bearing break with the
  DRY-first reflex, and the reason his rule ("does it elevate the level?") is about *reading*, not
  economy.
- **"Reconstruction work" is the through-line to the batch's main thread.** Every remedy for the
  [[verification-burden]] assumes a human or agent can cheaply reconstruct intent from a fragment of
  code. This is the practice that makes that assumption affordable — the *supply* side of the reading
  budget whose *demand* side he treats in
  [[tornhill-compressed-cognition-cost-of-faster-coding|Compressed Cognition]].

## Limits

- **A style argument with a toy example.** One three-line D&D snippet in two languages; no codebase, no
  measurement, no comparison of comprehension time or defect rate. Assertion plus taste, offered as
  such.
- **IMPRESSION NOT MEASUREMENT** for the payoff claim ("makes a large difference when returning to
  code you wrote months or years earlier") — personal experience over 20 years of FP.
- **The agent claim is by reference, not evidence.** "That's also true for coding agents as captured in
  the CLEAR principles" links to his own earlier post; nothing here tests whether named lambdas improve
  agent performance. The nearest actual evidence is
  [[borg-tornhill-code-for-machines-not-just-humans]] (peer-reviewed) and the LLM identifier-name
  result relayed in [[tornhill-opinionated-guide-to-naming]] — neither is about lambdas.
- **NOT INDEPENDENT in the general case** — CodeScene's founder/CTO arguing that code health is
  measurable and worth tooling — though this particular post sells nothing and cites no CodeScene
  product or figure.
- The cost he waves away (more indirection, more names to keep consistent, private helpers accreting)
  is not examined.

## Connections / contrast

- **[[ai-readable-code]] / [[agent-legibility]]** — a concrete expression-level lever, below the
  design-level [[tornhill-clear-design-principles-agentic-age|CLEAR]] principles and beside
  [[tornhill-hidden-design-decisions-control-coupling]] and [[tornhill-opinionated-guide-to-naming]] in
  the same series.
- **[[verification-burden]]** — the cheap-reading precondition. If you only read *some* code
  (his own position in [[tornhill-controlling-the-uncertainty-machine]]), the code you read has to
  yield its intent fast; naming is how. The two September pieces are one argument split across two
  levels.
- **[[willison-conceptual-integrity-and-counting-lines-of-code]]** — "the code communicates the domain
  rather than the mechanics" is conceptual integrity at the smallest scale, and the LOC clash noted
  above.
- **[[domain-driven-design]] / [[event-modeling]]** — "bringing the code closer to the domain" is
  ubiquitous language at expression level, and the same instinct
  [[tune-no-rapport-with-a-model-you-didnt-code|Tune]] says is degraded when you don't write the code
  yourself. Read together: Tornhill supplies the mechanism for encoding domain insight *into* code an
  agent typed; Tune doubts the insight arrives in the first place.
- **[[locality-of-reference]] / [[balanced-coupling]]** — limiting reconstruction work is the same
  target from the coupling side ([[khononov-golden-age-of-modularity]]).
- Also: [[open-closed-principle]], [[slice]], [[comprehension-debt]] (cheaper reading is cheaper
  interest payments).

## Links

Entities: [[adam-tornhill]] · [[markus-borg]] · [[simon-willison]] · [[nick-tune]]. Concepts:
[[ai-readable-code]] · [[agent-legibility]] · [[verification-burden]] · [[locality-of-reference]] ·
[[domain-driven-design]] · [[balanced-coupling]] · [[comprehension-debt]]. Related sources:
[[tornhill-clear-design-principles-agentic-age]] · [[tornhill-opinionated-guide-to-naming]] ·
[[tornhill-hidden-design-decisions-control-coupling]] · [[tornhill-ai-readable-code-series]] ·
[[tornhill-controlling-the-uncertainty-machine]] ·
[[willison-conceptual-integrity-and-counting-lines-of-code]].

_Raw source: `raw/articles/tornhill-beyond-lambdas-raising-the-abstraction-level.md`._
