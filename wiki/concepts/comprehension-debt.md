---
title: Comprehension Debt
type: concept
created: 2026-07-27
updated: 2026-08-16
sources: [addyosmani-software-factories-light-and-dark, addyosmani-earning-taste-and-judgment, willison-understand-to-participate, dilger-real-cost-of-ai-is-second-order, dilger-describing-without-solving-burns-you-out, ng-spec-driven-development-is-waterfall-in-markdown]
tags: [loop-engineering, comprehension-debt, ai-readable-code, focus]
---

# Comprehension Debt

**The widening gap between how much code exists and how much any human still understands**
([[addy-osmani|Osmani]]). Coined in his "Comprehension Debt" essay (2026-03) and load-bearing across the
[[loop-engineering]] thread: the faster an agentic loop ships code you didn't write, the larger the gap
between what exists and what anyone can still reason about — unless someone reads what the loop made.

Distinct from ordinary technical debt: tech debt is code that's *hard to change*; comprehension debt is code
that's *unread*. A [[software-factory|dark factory]] "doesn't pay it down; it takes it on as fast as it can,
with the tests green the whole way" ([[addyosmani-software-factories-light-and-dark]]). The reckoning is
"quiet and late" — three-to-six months into a fully automated project you're "already drowning in unread
code," and [[dex-horthy|Dex Horthy]]'s ~4-month dark-factory run needed painstaking manual debugging to
recover.

The underlying tradeoff: maximizing **token utilization** (the number we treat as progress) quietly
*minimizes* the amount of the system any human still understands. The defenses are the same ones that answer
the [[loop-engineering|"stay the engineer"]] caveats — read the diffs, move judgment upstream (a lit
factory), and keep enough fluency to remain "an active participant with the model"
([[willison-understand-to-participate|Litt's "understand to participate"]]). Osmani frames it as one of "two
debts: cognitive surrender and comprehension" ([[addyosmani-earning-taste-and-judgment]]); it is the
comprehension side of the same coin as [[ai-readable-code]] (design code the agent — and the next human — can
actually read) and the reason [[addyosmani-own-the-outer-loop|Answerability]] can't be delegated.

## It shows up on the ledger, not the tooling invoice (Dilger, 2026-07)

[[dilger-real-cost-of-ai-is-second-order]] is the KB's most concrete field anecdote for this debt: a CTO's
engineering costs rose **~30% at flat headcount**, and the increase wasn't the AI tooling bill — it was
**second-order costs nobody assigned an owner to**: more incidents, each slower to diagnose "because the
code involved was less understood"; longer onboarding; senior engineers converted "from asset to
overhead" by firefighting; and features that took three attempts "because the first two collided with
things nobody knew were there." That collision-with-the-unknown *is* comprehension debt, priced. It's the
cost-accounting face of the [[dora-roi-ai-assisted-software-development-2026|DORA]] **J-Curve /
verification + instability taxes** — the "productivity dip" is exactly these hidden costs.

## The requirements-side variant (Dilger, 2026-08-14)

Comprehension debt is usually framed as *code you didn't read*. [[dilger-describing-without-solving-burns-you-out]]
adds the upstream form: **problems you didn't solve**. Teams doing spec-driven development can "stop
solving problems and just describe them, and then hand it to AI and hope it figures out the solution" —
and "describing a problem without solving it leaves a hole that keeps growing." Same debt, incurred one
stage earlier: the artifact exists, the understanding behind it doesn't. His reported symptom is the
affective one — "describing your way through a day can feel just as hollow as mindlessly typing through
one," plus burnout from supervising parallel agent sessions — which makes it a *felt* signal rather than
a measurable one, unlike the [[fowler-bockeler-maintainability-sensors|sensor]]-style detection the code
side is getting. See [[spec-driven-development]].

## Reviewer, not builder — the role version (Ng, 2026-03)

[[ng-spec-driven-development-is-waterfall-in-markdown]] arrives at the same debt from the critique side
and states the mechanism as a **change of role**: "When you write a spec and hand it to an agent, you've
removed yourself from the process. When the code comes back, you're auditing someone else's work. You're
a reviewer, not a builder." That is comprehension debt described at the moment it is *taken on* rather
than when it is paid — the handoff itself is the transaction.

His diagnostic complaint is the same one Osmani's "quiet and late" reckoning predicts, applied to
requirements: at incident time, "You open the spec. You compare it to the implementation. You try to
figure out where they diverged." — which he sums up as "comparing a fantasy document to reality and
wondering which one lied."
The proposed instrument — a [[decision-trace]] running meeting → ticket → prompt → decision log — is an
explicit attempt to make the debt *legible* rather than to avoid incurring it, and is worth reading
against the [[fowler-bockeler-maintainability-sensors|sensor]] approach on the code side: both give up on
prevention and invest in detection.

## Related

[[loop-engineering]] · [[software-factory]] · [[ai-readable-code]] · [[willison-understand-to-participate]] ·
[[spec-driven-development]] · [[decision-trace]] · [[dilger-describing-without-solving-burns-you-out]] ·
[[ng-spec-driven-development-is-waterfall-in-markdown]] ·
[[tornhill-ai-readable-code-series]] · [[addyosmani-own-the-outer-loop]] · [[addy-osmani]] ·
[[dilger-real-cost-of-ai-is-second-order]] · [[dora-roi-ai-assisted-software-development-2026]].
