---
title: Comprehension Debt
type: concept
created: 2026-07-27
updated: 2026-09-04
sources: [addyosmani-software-factories-light-and-dark, addyosmani-earning-taste-and-judgment, willison-understand-to-participate, dilger-real-cost-of-ai-is-second-order, dilger-describing-without-solving-burns-you-out, ng-spec-driven-development-is-waterfall-in-markdown, khononov-ai-doesnt-fix-your-real-bottleneck, osmani-ai-wont-teach-you-the-lesson-unless-you-force-it, addyosmani-human-judgment-relocates, addyosmani-code-agent-orchestra, macmanus-prs-not-welcome-software-factories, zalando-agentic-engineering-snapshot, voss-what-the-hell-is-a-loop-anyway, willison-brewster-cannot-review-180000-lines, tune-no-rapport-with-a-model-you-didnt-code, willison-conceptual-integrity-and-counting-lines-of-code, laycock-maybe-we-shouldnt-be-reviewing-all-this-code, tornhill-task-uncertainty-decides-what-code-you-read, tornhill-controlling-the-uncertainty-machine, tornhill-blast-from-the-past-sdd-illusion-of-known-scope, tornhill-compressed-cognition-cost-of-faster-coding]
tags: [loop-engineering, comprehension-debt, ai-readable-code, verification-burden, balanced-coupling, focus]
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
the [[loop-engineering|"stay the engineer"]] caveats — read the diffs (**but see the ceiling below**), move judgment upstream (a lit
factory), and keep enough fluency to remain "an active participant with the model"
([[willison-understand-to-participate|Litt's "understand to participate"]]). Osmani frames it as one of "two
debts: cognitive surrender and comprehension" ([[addyosmani-earning-taste-and-judgment]]); it is the
comprehension side of the same coin as [[ai-readable-code]] (design code the agent — and the next human — can
actually read) and the reason [[addyosmani-own-the-outer-loop|Answerability]] can't be delegated.

## Derived, not just observed — the Theory-of-Constraints version (Khononov, 2026-02)

[[khononov-ai-doesnt-fix-your-real-bottleneck]] reaches this concept from design theory rather than from
watching a loop run, which is worth having because everything else on this page is observation. His
argument: throughput is set by the single bottleneck, so **improving a non-bottleneck makes the system
worse** — more work-in-progress piled in front of the constraint, "more inventory. More cost. More
waste." The bottleneck in software is **"our ability to comprehend systems"**, capped by working memory.
Therefore AI-accelerated code production is textbook over-production upstream of the constraint, and "the
Theory of Constraints predicts exactly what happens next: the system degrades."

Two things this adds:

- **Comprehension debt becomes a predicted consequence rather than an observed surprise.** Osmani's
  reckoning is "quiet and late"; Khononov says it is *inevitable* given the queue shape — which is why
  [[dilger-real-cost-of-ai-is-second-order|Dilger's]] ~30%-at-flat-headcount anecdote and the
  [[dora-roi-ai-assisted-software-development-2026|DORA]] J-curve are what the model expects, not
  anomalies.
- **A different remedy.** The page's defences are read-the-diffs, move judgment upstream, stay fluent.
  Khononov's is **modularity** — reduce the cognitive load the system *induces*, by balancing
  [[balanced-coupling|shared knowledge × distance × volatility]] so that "when you need to make a change,
  you know exactly which components are affected, and the outcome." Reading pays the debt down;
  modularity slows the rate at which it is incurred. His P.S. blocks the obvious shortcut: "generating
  code that *looks* modular and designing a system that *is* modular are two very different things…
  **that's not a prompting problem.**"

**Markers:** **NOT INDEPENDENT** (his own model and book, affiliate-linked) and **IMPRESSION NOT
MEASUREMENT** — the argument is analytical throughout, and the 4±1 / 7±2 working-memory figures are cited
as "studies" **with no reference on the page**. Do not promote them to citable findings.

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

**The mechanism version, and it is not about discipline (Tornhill, 2026-05-28).** Dilger's variant is a
choice — teams that *"stop solving problems and just describe them."*
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]] argues the debt accrues even when nobody
checks out, via **requirements explosion**: invoking Robert Glass — *"for every 10-percent increase in
problem complexity, there is a 100-percent increase in the software solution's complexity"* — he
concludes *"each requirement in the spec will lead to tens of implicit design requirements that need to
be resolved. We cannot leave that as guesswork for an agent to figure out."* *(**Glass's assertion as
relayed**; Tornhill names no specific work and measures nothing. Never write "research shows".)*

The debt-shaped consequence is his second obstacle: if agents resolve those implicit requirements for
you, recovering them later is *"like reverse engineering a legacy codebase. **That's the position we'd
be in. Constantly.**"* That is comprehension debt stated as a **structural property of delegated
implementation**, not as a failure to read the diff — and it is why he insists *"implementation is an
essential part of the discovery process itself."* Pair with his own
[[tornhill-compressed-cognition-cost-of-faster-coding]] for the cognitive-load half.

*(**NOT INDEPENDENT** for the remedy he prescribes — *"intention-revealing software design, automated
safeguards for our code and its behavior"* is the category CodeScene, his own company, sells. The piece
contains **no figures at all**.)*

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

## Two first-person failures, from someone who approved the change ([[addyosmani-human-judgment-relocates|Osmani, 2026-08-21]])

The KB's most concrete instances of this page's thesis, both about *understanding* rather than
correctness, both from the author's own repos.

**The feature he had to relearn.** Tests passed, he merged a favouriting feature, returned days later to
tweak it and *"couldn't explain to you how the feature worked. **This repository was mine, right? I'd
approved the change.** I understood how a lot of it worked, a lot of the repo worked, but **my
understanding hadn't kept up pace with all of the code that had been building up.**"* He had to redo it
step by step. Note that approval was not comprehension.

**The wrong-project prompt.** He typed a dark-mode prompt into the session for a different project and
*"began implementing dark mode for something that absolutely didn't need it. And so I can make that
mistake. **I don't want my software factory making that kind of mistake.**"*

**Why parallel work amplifies it, and it is not just review volume.** *"My cognitive bandwidth does not
scale with the agents… When you're doing five or 10 sessions, they create much more than just a review
volume problem. **They create several mental models that can end up going pretty cold** while you're
working elsewhere."* Plus the record problem: *"as compaction has been happening, you're not going to have
everything there… **Code often preserves a decision that was made, but not why the decision was made.**"*
His mitigation is on-disk and cheap: *"consider asking your agent to actually **store information about
its trajectory**, or interesting lessons about how it approached a problem so that you can go back to it
later"* — commit it, keep it local, or share it with the team, but write it down. (Same instinct as
[[adr|ADRs]], [[decision-trace]], and [[miracle-my-loop-engineering-workflow|Miracle's]] *"decision log
for the calls you never want re-litigated."*)

**The mechanism, stated best in [[addyosmani-code-agent-orchestra|his earliest piece]] (2026-03):**
*"When humans write code slowly, you feel the pain early… **Pain is immediate, so you fix as you go.**
With an orchestrated army of agents, there's no natural bottleneck. Small harmless mistakes — a code smell
here, a duplication there, an unnecessary abstraction — compound at a rate that's unsustainable. **You have
removed yourself from the loop, so you don't feel the pain until it's too late.** Then one day you try to
add a feature, and the architecture doesn't allow it. **Your tests are equally untrustworthy because
agents wrote those too.**"* That last sentence is the sharpest statement in the KB of why maker ≠ checker
cannot be satisfied by agent-written tests — cf. [[bockeler-tdd-inside-the-agent-loop]].

**Proposed metrics** (proposals, not results): **cost per merged PR** and **code shelf life**.
*(All of the above is practitioner self-report; no measurement.)*

## The ceiling on "read the diffs" (2026-08/09)

The defence above assumes reading is a choice you can keep making. Three sources arriving within a
fortnight say it has a hard limit, and one of them is past it. Osmani's "cognitive bandwidth does not
scale with the agents" is the same ceiling stated from inside one person's week.

**Past it:** [[rick-brewster]], Paint.NET's maintainer, on ~180,000 agent-written lines added to a
~700,000-line codebase he has maintained 20+ years ([[willison-brewster-cannot-review-180000-lines]]):
*"it has not been thoroughly reviewed, it's more 'trust me bro' style. **I cannot possibly review
180,000 lines of code**, it's just way way *way* too much."* This is the debt announced by the debtor at
the moment of taking it on — and the counter-example that shows "read the diffs" can stop being
available rather than merely being hard. (His own counts, in a forum post: practitioner self-report, not
measurement. He is also a team of one, and the task was a spec-defined reimplementation behind a
feature flag.)

**Bounded by cognition:** [[simon-willison]] states the ceiling as a personal limit —
*"I don't have the cognitive capacity to stay on top of 100 times the amount of code"*
([[willison-conceptual-integrity-and-counting-lines-of-code]]) — and proposes the remedy the page
lacked: **load-balance the reading across a team**. See [[attention-bottleneck]].

**Replaced, deliberately:** [[adam-tornhill]] — *"I never read all AI-generated code. But, and this is
important, make the code you do read count"* — triages by task uncertainty and substitutes a
human-reviewed test boundary plus deterministic enforcement
([[tornhill-task-uncertainty-decides-what-code-you-read]],
[[tornhill-controlling-the-uncertainty-machine]]; **VENDOR SELF-REPORT** — his prescribed enforcement
includes CodeScene's own CodeHealth MCP and he is its founder/CTO). His name for what happens if you
don't triage is the debt's endgame stated as a role: read all agent output the old way and *"we'll
effectively turn ourselves into legacy code maintainers."*

And [[rachel-laycock]] accepts the debt is real (Houck's *"cognitive and intent debt"* — a vocabulary
arrived at independently of Osmani's coinage) while denying the usual defence:
*"I just don't think mandatory pull requests are a particularly strong defence against it… **We need
engineers to understand systems, not diffs.**"* (**NOT INDEPENDENT** — Thoughtworks CTO on
martinfowler.com.) The whole argument about what to do instead is now on [[verification-burden]].

**None of this deletes the defence.** Reading the diffs still pays the debt down where it is available;
what these sources establish is that availability is bounded — by codebase size, by one person's
cognitive capacity, and by team size — so "read the diffs" is a defence with a budget rather than a rule.

## The modelling-side variant — models you didn't build (Tune, 2026-08-28)

The page holds code you didn't read and, via Dilger, problems you didn't solve. [[nick-tune]] adds a
third face, one step further upstream ([[tune-no-rapport-with-a-model-you-didnt-code]]): refining a
domain model with an agent *"is not the same as writing the lines of code yourself. I don't feel as
connected, I don't feel that the model is as deeply embedded in my mind as it would be if I wrote the
code. **And that means the domain model is going to be worse** because I'm clearly missing some nuances
that could lead to big modelling breakthroughs."*

Two things make this the hardest version of the debt. It is **unobservable** — a modelling breakthrough
that didn't happen leaves no failing test, no diff and no metric — and it may be **unpayable**: *"I'm
struggling to see how to get the same level of rapport with the model without actually writing the code.
**Maybe it's not even possible.**"* No amount of later reading recovers it, because the loss is of
insight that would have been generated by the act of writing. (Thin capture: an inference from a stated
feeling — a hypothesis with a named mechanism, not a finding.) The KB's candidate answer, which he does
not offer, is to keep the modelling act and delegate only the typing — [[event-modeling]],
[[model-as-code-vs-model-as-language]].

## Conceptual integrity — the design-coherence face (Willison, 2026-08-19)

A failure mode this page has been treating as the same thing, and shouldn't. Comprehension debt is code
**nobody has read**; conceptual-integrity loss is a **shape nobody chose**. Invoking *The Mythical
Man-Month*, [[simon-willison]] ([[willison-conceptual-integrity-and-counting-lines-of-code]]) notes that
well-designed software has "an integrity to it: there are no surprises in it, it covers exactly the
right domain of things, everything fits together" — and with agents, "you can have an idea for a
feature, run a prompt, and five minutes later you've got the feature. **Your software grows little weird
bumps in funny different directions**" (his interviewer's analogy: the Winchester Mystery House, 140
rooms added over 40 years).

The mechanism is **lost friction**: "It used to be that the discipline was enforced on you by the amount
of time it took… If it takes an hour, it's so much easier to justify." Note that **no amount of
per-diff review catches this** — every room is individually defensible — which is an argument for
[[fitness-functions]] and design constraints rather than for more reading, and the same lost-friction
observation Tornhill makes about cognitive recovery ("manual coding had a built-in pacing mechanism…
and it's now gone"). Asserted as an observed trend with no example or measurement. **If a second
independent source arrives on this, promote it to its own page** (`conceptual-integrity`); one source
does not warrant one yet.

## Skill decay is a different debt from comprehension debt

[[osmani-ai-wont-teach-you-the-lesson-unless-you-force-it|Osmani, 2026-09-02]]: *"AI can build the
feature, but it won't teach you the lesson unless you force it to… Early in my career, I built my
engineering intuition by spending thousands of hours debugging failures, reading diffs, and wrestling
with abstractions. Today, AI agents can short-circuit that entire journey. **You get the completed task,
but you miss the reps.**"* And the risk: *"If we treat agents/loops/software factories purely as **code
vending machines**, we risk severe skill decay. We might become incredibly fast at prompting, but lose
the deep expertise required to actually **verify the output** when assumptions no longer fit the system."*
His epigram: **"Verification is the floor. Imagination is the ceiling."**

**Keep the two debts apart, because they are paid down differently.** Comprehension debt is local — a gap
between what exists in *this* repo and what you understand of it, and **reading the code pays it down**
(as Osmani's own relearned-feature story shows), within the ceiling established above. **Skill decay is
portable** — a gap between what you can do and what you could once do; it travels across codebases,
**reading the diff does not repair it**, because the missing thing is the reps, and it shows up as
degraded **verification capability**. That last part is the operational sting: the loss of reps eventually
undermines the very verification the whole [[loop-engineering]] discipline depends on — and every remedy
on [[verification-burden]] presumes it intact.

**His three countermeasures are all placed *around* the loop, not inside it:** **form a hypothesis
first** (*"Before prompting, predict what the solution should look like or where an architecture might
fail"* — a pre-registration habit, which is what turns a task back into a rep); **anchor on explanation**
(*"Instead of just generating net-new features, actively use agents to **analyze and explain existing
codebases**"* — the agent as comprehension instrument rather than producer); and **codify the lessons**
(*"Turn corrected assumptions into **linting rules, documentation, or tests** in your repo so both you and
the next agent can benefit"* — the hill-climbing loop aimed at the human's learning as much as the
harness's).

**The same problem appears at three scales, and none of the three has evidence.**

| Scale | Source | The mechanism |
| --- | --- | --- |
| **Individual** | [[osmani-ai-wont-teach-you-the-lesson-unless-you-force-it]] | "you miss the reps" — asserted as a **risk**, not measured |
| **Career** | Geoffrey Litt, relayed in [[voss-what-the-hell-is-a-loop-anyway]] | *"those who delegate understanding get replaced by the agent"* |
| **Institution** | [[macmanus-prs-not-welcome-software-factories]] | PRs were how maintainers were taught and assessed; close them and the pipeline closes — *"you and I go on vacation — what happens?"* |

**The closest thing to organizational evidence** comes from [[zalando-agentic-engineering-snapshot]],
running ~6 training sessions for 120–150 people: *"We have observed that the temptation of participants to
use coding agents as a shortcut to achieve results is high. **Yet, using coding agents usually inhibits
learning.**"* It is an observation, not a study — but it produced a **policy change** (*"state explicitly
when manual coding is expected"*), and it is the only such report in the KB.
*(**VENDOR SELF-REPORT** in the sense that it is Zalando's account of its own programme; there is no
control group and no measurement of learning outcomes.)*

*(If further evidence accrues, this section is a candidate to be promoted to its own `skill-decay`
concept page. Not yet — three assertions and one training observation do not carry a page.)*

## Related

[[loop-engineering]] · [[software-factory]] · [[ai-readable-code]] · [[willison-understand-to-participate]] ·
[[spec-driven-development]] · [[decision-trace]] · [[dilger-describing-without-solving-burns-you-out]] ·
[[ng-spec-driven-development-is-waterfall-in-markdown]] ·
[[tornhill-ai-readable-code-series]] · [[addyosmani-own-the-outer-loop]] · [[addy-osmani]] ·
[[dilger-real-cost-of-ai-is-second-order]] · [[dora-roi-ai-assisted-software-development-2026]] · [[verification-burden]] · [[attention-bottleneck]] ·
[[willison-brewster-cannot-review-180000-lines]] ·
[[tune-no-rapport-with-a-model-you-didnt-code]] ·
[[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]] ·
[[willison-conceptual-integrity-and-counting-lines-of-code]] · [[rick-brewster]] · [[nick-tune]] ·
[[khononov-ai-doesnt-fix-your-real-bottleneck]] · [[vlad-khononov]] ·
[[osmani-ai-wont-teach-you-the-lesson-unless-you-force-it]] · [[addyosmani-human-judgment-relocates]] ·
[[balanced-coupling]] · [[fitness-functions]].
