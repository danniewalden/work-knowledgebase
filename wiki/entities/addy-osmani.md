---
title: Addy Osmani
type: entity
created: 2026-06-28
updated: 2026-09-04
sources: [addyosmani-loop-engineering, addyosmani-own-the-outer-loop, addyosmani-earning-taste-and-judgment, addyosmani-software-factories-light-and-dark, addyosmani-code-agent-orchestra, addyosmani-agentic-code-quality, addyosmani-practical-loop-engineering, addyosmani-human-judgment-relocates, osmani-ai-wont-teach-you-the-lesson-unless-you-force-it, osmani-agentic-code-review-skill-five-axes]
tags: [person, loop-engineering, harness-engineering, agentic-coding, accountability, verification-burden]
---

# Addy Osmani

Engineering leader at Google (Chrome / web-platform DevRel background) and prolific author on software
engineering and, increasingly, AI-assisted development. In the KB he is the author of the **definitional
primary** for [[loop-engineering]] ([[addyosmani-loop-engineering]], 2026-06-07): loop engineering as
"replacing yourself as the person who prompts the agent," sitting one floor above
[[harness-engineering|the harness]], built from five primitives + on-disk memory.

His writing forms a connected series the source page references — agent harness engineering, the
"factory model," the "orchestration tax," "intent debt," "comprehension debt," and "code review in the
age of AI" — making him a recurring practitioner voice on the [[harness-engineering]] /
[[unattended-coding-agents]] thread. Stance is notably **skeptical-optimist**: build the loop, but
"stay the engineer," watch token costs, and read what the loop produces.

His follow-on **[[addyosmani-own-the-outer-loop|"Own the Outer Loop"]]** (2026-07-09) completes the arc:
if the loop-engineering primary industrialized the *inner* loop, this names the **outer loop** as the
human's irreducible **accountability** boundary — **Quality → Verdict → Answerability**, humans in the
constraints/sampling/audit/ownership loops but never the inner one, and an "accountability contract" per
codebase ("the bottleneck moves from 'can we build this?' to 'should this exist, can we answer for it?'").

Two July-2026 pieces extend the arc further. **[[addyosmani-earning-taste-and-judgment|"Earning taste and
judgment"]]** (2026-07-14) is the *positive* complement to "stay the engineer": since agents automate the
"reps" that used to produce taste, the durable, ungradeable human contribution is **choosing what to build
and judging whether it's any good** ("anything gradeable by someone else is getting automated") — with seven
concrete habits (read more code than you write, a "wrong log," specify-and-verify-separately, build a
personal eval/rubric and run it on 50 real AI PRs). **[[addyosmani-software-factories-light-and-dark|"Software
Factories, Light and Dark"]]** (2026-07-20) adds the top rung of the stack — the [[software-factory]] as "an
org chart made of loops" — and the KB's anchor for **light vs dark factories**, **back pressure**
(verification, not generation, is the constraint), and the **loops-vs-graphs** question; it leans on
[[dex-horthy|Dex Horthy]]'s "Harness Engineering is not Enough" talk.

## The 2026 arc, in order

[[addyosmani-code-agent-orchestra|The Code Agent Orchestra]] (03-26) — **earlier than anything else on
this page and the antecedent to the whole loop-engineering arc**: conductor → orchestrator, the
multi-agent patterns, and the discipline argument (*"The human bottleneck was a feature, not a bug"*);
[[addyosmani-loop-engineering|Loop Engineering]] (06);
[[addyosmani-own-the-outer-loop|Own the Outer Loop]] (07-09);
[[addyosmani-earning-taste-and-judgment|Earning taste and judgment]] (07-14);
[[addyosmani-software-factories-light-and-dark|Software Factories, Light and Dark]] (07-20);
[[addyosmani-agentic-code-quality|Agentic Code Quality]] (08-08) — quality lives in the constraints, and
the four capacity levers when verification can't keep up;
[[addyosmani-practical-loop-engineering|Practical Loop Engineering]] (08-14) — what the primitives are
actually used for, and what loops are **not** for;
[[addyosmani-human-judgment-relocates|Human Judgment Doesn't Leave the Software Factory. It Relocates.]]
(08-21) — *"do you really need a factory yet?"* and the five things that stay human;
[[osmani-agentic-code-review-skill-five-axes|the agentic review skill]] (08-28, below);
[[osmani-ai-wont-teach-you-the-lesson-unless-you-force-it|"AI won't teach you the lesson unless you
force it to"]] (09-02) — skill decay and three countermeasures.

## The review skill, and the dispute it lands in (2026-08-28)

[[osmani-agentic-code-review-skill-five-axes]] is his `code-review-and-quality` skill in the public
`addyosmani/agent-skills` pack: review on **five axes** (correctness, readability, architecture,
security, performance), **severity labels** ("Critical" blocks the merge; "Nit"/"FYI" optional),
findings **ordered by leverage** ("if there is one structural problem and ten nits, the structural
problem *is* the review"), and each finding **proposing the move** rather than naming a smell. His
justification for going beyond tests is the sharp part: *"Most automated reviews collapse to 'do the
tests pass?' Tests are necessary, but **they don't catch a leaking module boundary**"* — an unintended
rebuttal to [[tornhill-controlling-the-uncertainty-machine|Tornhill's]] test-suite-as-review-boundary
method. His framing, *"The review is your quality gate… Run /review before you merge,"* is the
**automate-the-gate** position on [[verification-burden]], and is precisely what [[rachel-laycock]]
calls *"automating the ceremony"* five days later
([[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]]) — neither names the other. **Author's own
tool: no evaluation, benchmark or comparison against other review skills**, and the skill's own content
is not in `raw/`. Worth reading against his [[addyosmani-own-the-outer-loop|Answerability]] argument,
which the post leaves unstated: an agent may produce the review, but the merge decision is still the
human's — and against his own [[comprehension-debt]] coinage, of which this is the tooling answer.

## Standing caveats for citing him

He is a **Director at Google Cloud AI** (his earlier Chrome / web-platform DevRel work is the background
described above) writing about a practice he also promotes commercially — an O'Reilly book, a reference
`factory` repo — and his posts routinely cite his own earlier posts as support. **NOT INDEPENDENT** for
the agentic-engineering framing generally.

His quantities are **practitioner impressions and demo observations, never measurements.** Three that
must carry their markers wherever they travel:

- The `AGENTS.md` percentages in *The Code Agent Orchestra* — LLM-generated "~3% success reduction,
  20%+ inference cost"; developer-written "~4% improvement" — are **UNCITABLE**. They are presented as
  research and **no study is named or linked anywhere in the page.** The *practice* (human-curated
  `AGENTS.md` only) may be carried; the three figures may not.
- "Parallelism (3x throughput)", "3–5 teammates is the sweet spot", "three focused agents outperform one
  generalist working 3x as long", "substantially cuts stuck agents", token budgets 180k/280k, "roughly
  220k tokens total" — **IMPRESSION NOT MEASUREMENT**: practitioner judgement plus four demo videos on a
  toy bookmarks app.
- The review skill above has **no evaluation of any kind**.

He is also candid about his own failures (the wrong-project prompt, the feature he had to relearn, the
near-miss where he *"delegated the task, but I was close to delegating the judgment as well"*), which is
much of what makes him worth citing.

_Sources: [[addyosmani-loop-engineering]] · [[addyosmani-own-the-outer-loop]] ·
[[addyosmani-earning-taste-and-judgment]] · [[addyosmani-software-factories-light-and-dark]] ·
[[addyosmani-code-agent-orchestra]] (03-26 — the antecedent; **its `AGENTS.md` figures are UNCITABLE**) ·
[[addyosmani-agentic-code-quality]] · [[addyosmani-practical-loop-engineering]] ·
[[addyosmani-human-judgment-relocates]] ·
[[osmani-agentic-code-review-skill-five-axes]] (author's own tool, no evaluation) ·
[[osmani-ai-wont-teach-you-the-lesson-unless-you-force-it]]._
