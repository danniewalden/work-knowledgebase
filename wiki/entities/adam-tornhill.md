---
title: Adam Tornhill
type: entity
created: 2026-06-14
updated: 2026-09-04
sources: [tornhill-five-programming-books-that-changed-how-i-think, tornhill-codescene-unhealthy-code-agentic-token-cost, borg-tornhill-code-for-machines-not-just-humans, tornhill-clear-design-principles-agentic-age, tornhill-hidden-design-decisions-control-coupling, tornhill-merge-conflicts-agentic-bottleneck, tornhill-ai-readable-code-series, tornhill-opinionated-guide-to-naming, tornhill-cannot-trust-agent-codescene-mcp, tornhill-why-human-level-ai-wont-be-enough, tornhill-controlling-the-uncertainty-machine, tornhill-task-uncertainty-decides-what-code-you-read, tornhill-compressed-cognition-cost-of-faster-coding, tornhill-beyond-lambdas-raising-the-abstraction-level, tornhill-ai-induced-code-smells-codehealth-mcp, tornhill-blast-from-the-past-sdd-illusion-of-known-scope]
tags: [person, code-health, technical-debt, agentic-coding, harness, agent-legibility, verification-burden]
---

# Adam Tornhill

**Founder and CTO of CodeScene**, and author of *Your Code as a Crime Scene* / *Software Design X-Rays* —
known for **behavioral code analysis** (mining version-control history to find hotspots, coupling, and
technical debt).

> **Standing marker for this whole page.** He is CodeScene's founder/CTO, and the remedies he prescribes
> — deterministic code-health sensors, the CodeScene MCP, the CodeHealth MCP, "intention-revealing design
> plus automated safeguards" — **are his own product's category**. Every prescription below is therefore
> **VENDOR SELF-REPORT / NOT INDEPENDENT** at the point of use, and the marker is repeated inline where
> each one appears rather than being spent once here. His *diagnoses* are a separate matter and often
> cut against his interest; the one peer-reviewed item ([[borg-tornhill-code-for-machines-not-just-humans]])
> is the strongest thing on the page.

His 2026 angle relevant to this KB is **code health as a lever on AI-agent cost and
reliability**: CodeScene research he shares claims unhealthy code raises agent token spend 35–45% and
that agents perform worst in high-technical-debt legacy code
([[tornhill-codescene-unhealthy-code-agentic-token-cost]] — **VENDOR SELF-REPORT**: CodeScene's own
research on CodeScene's own metric, and the figures must carry that marker wherever they travel). That
thesis is now grounded in a
peer-reviewed study he co-authored with **[[markus-borg]]** et al.,
[[borg-tornhill-code-for-machines-not-just-humans]] (FORGE 2026): healthier code yields a 15–30% lower
AI-refactoring break rate, and CodeHealth predicts refactoring correctness better than perplexity or
SLOC.

Beyond the CodeScene company blog he writes a personal Substack, **"Code for Humans and Machines"**
(adamtornhill.substack.com), on *AI-readable code* — practical refactoring patterns and design
principles for codebases that agents can safely evolve. Its flagship piece introduces
**[[tornhill-clear-design-principles-agentic-age|CLEAR]]** (Conceptual alignment, Local reasoning,
Explicit intent, Avoid search luck, Reduce the edit surface): a re-framing of design for agents around
limiting *reconstruction work* and the change blast-radius, explicitly positioned against SOLID's
human-maintainability target.

The Substack is a running **[[ai-readable-code|AI-Readable Code]]** series
([[tornhill-ai-readable-code-series]]): CLEAR distilled from concrete refactoring walkthroughs, of
which **[[tornhill-hidden-design-decisions-control-coupling|Hidden Design Decisions]]** (boolean flag →
Strategy + domain type) is the latest. He also extends the argument to the multi-agent scale —
**[[tornhill-merge-conflicts-agentic-bottleneck|merge conflicts as a socio-technical signal]]**, where
his behavioral-code-analysis lineage (*Your Code as a Crime Scene*) meets parallel agents — and adds two
useful counter-weights:
**[[tornhill-compressed-cognition-cost-of-faster-coding|*Compressed Cognition*]]** (speed paid for in
decision density) and
**[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|*SDD and the Illusion of Known Scope*]]** —
not merely a caution against spec-first optimism but a **positive argument** from requirements explosion
and lived MDA/Executable-UML/RUP experience (see the SDD section below).

> **Citation repair (2026-09-04).** *SDD and the Illusion of Known Scope* used to be named in prose here
> with no link, and elsewhere in this wiki it was piped onto
> `tornhill-merge-conflicts-agentic-bottleneck` — **a different article**. Its own source page,
> [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]], now exists and is the only correct
> target. `tornhill-merge-conflicts-agentic-bottleneck` is the merge-conflict piece and nothing else.
> If you find the old pipe on another page, it is the same bug.

Two further 2026-06 pieces sharpen the thread: **[[tornhill-opinionated-guide-to-naming|a naming guide]]**
(Jun 23) — naming as cognitive compression, the highest-leverage AI-readable-code move, with a cited LLM
result that identifier-name improvements "yielded the largest returns"; and
**[[tornhill-cannot-trust-agent-codescene-mcp|"you cannot trust your coding agent to produce maintainable
code"]]** (Jun 22) — an LLM can't reliably self-assess code health, so the fix is a **deterministic
external sensor** (the CodeScene MCP) rather than "follow SOLID" prompts or LLM self-review; he's coded
100% agentically for nine months.

A 2026-06-30 essay steps up from tactics to thesis:
**[[tornhill-why-human-level-ai-wont-be-enough|"Why Human-Level AI Won't Be Enough"]]** argues that even
best-human-expert-level coding agents won't suffice, because AI *raises its own quality bar* through
**scale** (Lehman's laws; defect opportunities grow with code + change volume) and **speed**
(orders-of-magnitude faster generation → higher churn/fault risk = "wrong at scale"), while the
stochastic core guarantees rare errors recur across millions of decisions. He rejects chasing
"superhuman code quality" and prescribes the opposite — **"create environments where unreliable agents
reliably produce acceptable outcomes."** This is the load-bearing *why* under his code-health tooling:
the value is in the environment, not a better model — the KB's environment-over-model through-line.

In the KB he connects the **code-health / technical-debt** angle to [[harness-engineering]] (a
cost/quality argument adjacent to [[fowler-bockeler-maintainability-sensors]]), [[agentic-coding]], and
now [[agent-legibility]] / [[locality-of-reference]] / [[ai-readable-code]] (via CLEAR and the series).
Watched in `watch-config.json` (the Substack is his on-thread personal primary; the LinkedIn feed mixes
on-thread items with off-thread LLM-culture commentary).

## The reading position, and its cost (2026-05 → 2026-09)

His 2026 second theme is no longer only *how code should be shaped* but **how much of it a human should
read** — a named position in the [[verification-burden]] dispute.

**[[tornhill-controlling-the-uncertainty-machine|Controlling the Uncertainty Machine]]** (2026-08-20,
restated in his own words in [[tornhill-task-uncertainty-decides-what-code-you-read|a LinkedIn post]])
gives the rule: *"Human attention should follow uncertainty… I never read all AI-generated code. But,
and this is important, **make the code you do read count**."* Task uncertainty — how much of the
intended behaviour and structure is already represented in the system — sets **two dials at once**, the
agent's autonomy *and* the human's review depth ([[autonomy-ladder]]). The substitute instrument is a
**human-reviewed e2e suite written before the implementation** ("a strong test suite serves as a
boundary between the code I do inspect and the code I give the AI autonomy to develop"), with review
findings converted into forward-looking **SKILLs**, and everything uninspected held by **deterministic**
tooling. His stated cost of the change is the honest part: after "almost 40 years" of hand-coding,
"becoming comfortable with *not* reading code was a large mental shift." **VENDOR SELF-REPORT travels
with the remedy** — the deterministic layer he prescribes includes **CodeScene's own CodeHealth MCP**,
and [[tornhill-ai-induced-code-smells-codehealth-mcp|his product post for it]] (2026-09-03) states the
bargain's promise exactly: complexity-inducing smells *"that I - as the human in the loop - never need
to see."* **That post's statistics are in an unread screenshot — the page itself carries no figures, and
no page in this wiki may cite a figure from it, because there is none to cite.**

[[addy-osmani|Osmani's]] shipped review skill supplies the unintended rebuttal to the test-boundary half
of the method — *"they don't catch a leaking module boundary"*
([[osmani-agentic-code-review-skill-five-axes]]) — and neither names the other; the KB holds both on
[[verification-burden]].

**[[tornhill-compressed-cognition-cost-of-faster-coding|Compressed Cognition]]** (2026-05-07) is the
cognitive justification underneath that method, now a full page rather than a line in the series index:
agents **compress the decision timeline**, working memory holds "3-4 things," self-interruption is worse
than external interruption, and *"manual coding had a built-in pacing mechanism… and it's now gone."*
Two things to carry forward. First, **the batch's only hard measurement**: a controlled trial in which
developers **estimated a 20% speedup** and were **19% slower** — but he **names no study, date or
link**, so cite it as *an unnamed controlled trial as relayed by Tornhill* and **never** as "Tornhill
cites METR"; keep the felt and measured figures distinct, since the gap is his point. Second, his flat
refusal of human-side parallelism — *"one long-running agentic maintenance task… and one focus task.
**Never more**"*, and "it is the parallelisation of human attention that does not scale" — which puts
him **against [[laycock-the-conductor-developer|Laycock's 8-to-12-agent conductor]]** on
[[attention-bottleneck]] (both anecdote-grade; the KB holds both).

**[[tornhill-beyond-lambdas-raising-the-abstraction-level|Beyond Lambdas]]** (2026-09-01) is the newest
series walkthrough and the code-level companion: lambdas "optimize for writing code… at the expense of
reading code, which is arguably a much more frequent activity," so name them after the domain —
**"anonymous functions are anonymous thoughts."** He accepts more lines of code to get it
("**lines of code are not a finite resource**"; abstractions "don't have to be re-used to motivate
their existence"), which is a direct if unengaged counter to
[[willison-conceptual-integrity-and-counting-lines-of-code|Willison's]] hard-ceiling defence of LOC as
a productivity indicator. The purpose is his standing one: **limit reconstruction work** — which is
also what makes the *selective* reading his triage rule depends on affordable.

## On spec-driven development (2026-05-28)

His fullest statement on [[spec-driven-development|SDD]]
([[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]]) scopes itself to the **strong form**
(spec as ground truth, per [[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler's]] ladder) and
explicitly **declines the waterfall argument** others make: *"Not due to waterfall thinking — many SDD
practitioners evolve their systems iteratively — but rather due to the nature of problem solving."* The
argument is **requirements explosion** — Robert Glass's "for every 10-percent increase in problem
complexity, there is a 100-percent increase in the software solution's complexity", **relayed by
Tornhill, attributed to no specific work and measured by nobody in the citation chain; never write
"research shows"** — plus lived MDA/Executable-UML/RUP experience, where hand-drawn UML plus a design
review *worked* until the vendors closed the loop with an action language and "the first victim was the
documented design." It closes on *"the moment a model becomes the implementation, it ceases to be a good
model."*

**NOT INDEPENDENT for the alternative he prescribes** — *"intention-revealing software design, automated
safeguards for our code and its behavior"* is CodeScene's category — and the piece contains **no figures
at all**. He was also programmed at **GOTO Copenhagen 2026** one day after [[martin-dilger]]'s Event
Modeling masterclass ([[dilger-goto-cph-2026-event-modeling-ai-native-software-design]]) — the KB's
advocate and its sharpest sceptic on the same programme.

Not everything he writes is on this thread. **[[tornhill-five-programming-books-that-changed-how-i-think|Five
Programming Books That Changed How I Think]]** (2026-08-11) is a pre-2015 reading list — SICP, Beck's
*Smalltalk Best Practice Patterns*, Norvig's *PAIP*, Glass, *Thinking Forth*, Shiffman — filed for
completeness rather than evidence. Two asides connect: his jab at "AI adoption metrics… back to
productivity mistaken for lines of code produced," and his endorsement of Coplien's **commonality /
variability analysis** as "the foundation of great software design" — an ancestor of the
[[business-capabilities]] boundary-finding the KB tracks. Also worth noting for taste calibration: he
declines to recommend *Clean Code* ("too narrow and a bit too dogmatic"), consistent with his
[[tornhill-clear-design-principles-agentic-age|CLEAR-over-SOLID]] argument.

_Source pages: [[tornhill-codescene-unhealthy-code-agentic-token-cost]] ·
[[borg-tornhill-code-for-machines-not-just-humans]] ·
[[tornhill-clear-design-principles-agentic-age]] · [[tornhill-hidden-design-decisions-control-coupling]] ·
[[tornhill-merge-conflicts-agentic-bottleneck]] · [[tornhill-ai-readable-code-series]] ·
[[tornhill-opinionated-guide-to-naming]] · [[tornhill-cannot-trust-agent-codescene-mcp]] ·
[[tornhill-why-human-level-ai-wont-be-enough]] ·
[[tornhill-five-programming-books-that-changed-how-i-think]] (off-thread reading list, 2026-08-11) ·
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]] (SDD and the Illusion of Known Scope, 2026-05-28 — **the correct target for that title**) ·
[[tornhill-compressed-cognition-cost-of-faster-coding]] (2026-05-07) ·
[[tornhill-controlling-the-uncertainty-machine]] (2026-08-20) ·
[[tornhill-task-uncertainty-decides-what-code-you-read]] (2026-08-28 — one argument split across two captures with the above; **never cite the pair as corroboration**) ·
[[tornhill-beyond-lambdas-raising-the-abstraction-level]] (2026-09-01) ·
[[tornhill-ai-induced-code-smells-codehealth-mcp]] (2026-09-03 — **contains no figures**)._
