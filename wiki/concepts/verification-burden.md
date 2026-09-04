---
title: The Verification Burden
type: concept
created: 2026-09-04
updated: 2026-09-04
sources: [willison-brewster-cannot-review-180000-lines, laycock-maybe-we-shouldnt-be-reviewing-all-this-code, tornhill-controlling-the-uncertainty-machine, tornhill-task-uncertainty-decides-what-code-you-read, willison-more-than-just-code-review, willison-conceptual-integrity-and-counting-lines-of-code, tune-no-rapport-with-a-model-you-didnt-code, osmani-agentic-code-review-skill-five-axes, tornhill-compressed-cognition-cost-of-faster-coding, tornhill-ai-induced-code-smells-codehealth-mcp, khononov-value-of-90-percent-done-never-lower, dilger-lights-off-software-factory-dead-end]
tags: [verification-burden, comprehension-debt, code-review, agentic-coding, live-dispute, focus]
---

# The Verification Burden

**Agents made producing code cheap and left the cost of *believing* it exactly where it was.** This
page holds the resulting argument — *who reads the code, and what replaces reading when nobody can* —
as a **live dispute**, not a settled position. Five practitioner answers arrived between May and
September 2026, from authors who do not cite one another. **Nothing on this page is resolved, and no
position here should be quoted as the KB's view.**

It is the operational face of [[comprehension-debt]]: that page prices what unread code costs; this one
holds the fight about what to do instead of reading it. [[martin-dilger]] states the bind most plainly
(recorded on [[software-factory]]): *"you can't do full code reviews - it'll not be sustainable with the
increased output - you just moved the bottleneck. But you can't do no code-reviews either."*

## The pivot everyone turns on: verification ≠ review

[[simon-willison]] gives the cleanest form ([[willison-more-than-just-code-review]], 2026-08-22): the
key skill is to *"confidently instruct"* an agent and then *"confidently verify"* the result —
*"Sometimes this involves reviewing every line of code they have written, but there are other ways to
achieve that goal. **Eyeballing every line of code has never been the most effective way to validate a
change.**"* Note the claim is about software engineering generally; agents merely removed the option of
pretending line-by-line review was the instrument.

[[adam-tornhill]] reaches the same place independently, six days later
([[tornhill-task-uncertainty-decides-what-code-you-read]]): *"I never read all AI-generated code. But,
and this is important, **make the code you do read count**."* Two unrelated practitioners converging is
the strongest thing this dispute contains; everything after it is disagreement about the substitute.

## The five positions

**1. Accept the debt** — [[rick-brewster]], relayed by Willison
([[willison-brewster-cannot-review-180000-lines]], 2026-09-02). Paint.NET's maintainer shipped ~180,000
agent-written lines (a clean-room Direct2D rewrite) into a ~700,000-line codebase he has maintained for
20+ years, and says: *"it has not been thoroughly reviewed, it's more 'trust me bro' style. **I cannot
possibly review 180,000 lines of code**, it's just way way *way* too much."* No substitute instrument is
offered. **Practitioner self-report about his own unreviewed code; all three counts are his own, from a
forum post — IMPRESSION NOT MEASUREMENT.** Two things keep it from being pure abdication: he *did* spot
inspect the risky seams ("I had to babysit Claude quite a bit… the COM equivalent of `AddRef()`"), and
the task had a **cheap external oracle** — a documented API, reimplemented behind a `/wine` flag. So his
*practice* was closer to triage than his rhetoric; what he lacked was a **systematic instrument** for it,
not the instinct. He is also a team of one, which forecloses two of the four other answers.

**2. Relocate what review is for, then review by exception** — [[rachel-laycock]]
([[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]], 2026-09-02). Her diagnosis is that review is
**over-loaded**: *"quality gate, security check, architecture review, mentoring mechanism,
knowledge-sharing system, ownership model. It worked, sort of, while humans could only produce code so
quickly. That constraint is disappearing."* So each function moves to where it belongs — alternatives
explored before implementing, knowledge transfer by **pairing**, collective ownership by team structure,
architectural alignment by designing together and then **encoding constraints as
[[fitness-functions]]**, and everything deterministic automated. What remains is **review by
exception**: architectural changes, sensitive security boundaries, huge blast radius, unfamiliar
critical code, or *"simply something where the team says, 'I'm not confident about this.'"* Her summary:
**"We need engineers to understand systems, not diffs."** **NOT INDEPENDENT** — Thoughtworks' CTO on
Thoughtworks' own channel (martinfowler.com), prescribing Thoughtworks-originated practices; no data of
her own. See the numbers note below.

**3. Triage by task uncertainty, and enforce what you don't inspect** — Tornhill
([[tornhill-controlling-the-uncertainty-machine]], 2026-08-20). The most operational answer.
*"Human attention should follow uncertainty."* Uncertainty means how much of the intended behaviour and
structure is **already represented in the existing system**, and it sets *two* dials at once: the
autonomy granted the agent, and the review effort spent. Bug fix → inspect the evidence, not the code.
First iteration of a novel feature → inspect structure and patterns, still not details. The substitute
instrument is a **human-reviewed end-to-end test suite** written *before* the implementation — *"a
strong test suite serves as a boundary between the code I do inspect and the code I give the AI autonomy
to develop"* — with the inversion that AI application code is "usually decent" while *"the test code?
Not so much,"* so the human effort goes into refactoring tests toward the domain. Review findings are
then converted into **forward-looking SKILLs**, and what goes uninspected is held by **deterministic**
tooling (linters, vulnerability scanners, custom architectural checks, and CodeScene's CodeHealth MCP).
*"The point is that these rules and constraints need to be enforced. Deterministically."*
**VENDOR SELF-REPORT on the remedy — Tornhill is founder/CTO of CodeScene, which sells the automated
safeguards he prescribes**, and his companion product post
([[tornhill-ai-induced-code-smells-codehealth-mcp]]) states the bargain's promise exactly: there are
smells *"that I - as the human in the loop - **never need to see**"*. **IMPRESSION NOT MEASUREMENT** on
the payoff: personal adaptation after ~40 years of hand-coding and ~1 year agentic, with no defect data.
The unexamined risk is what tests cannot see — cf. Brewster's `AddRef()` bug, which a rendering-level
e2e test would plausibly pass.

**4. Automate the gate** — [[addy-osmani]]
([[osmani-agentic-code-review-skill-five-axes]], 2026-08-28). Keep review exactly where it is and put an
agent in the chair: a published skill reviewing on five axes (correctness, readability, architecture,
security, performance), severity-labelling findings, ordering by leverage, and proposing the fix.
*"Most automated reviews collapse to 'do the tests pass?' Tests are necessary, but **they don't catch a
leaking module boundary**."* — a direct, unintended rebuttal to position 3's test boundary. His framing:
*"The review is your quality gate… Run /review before you merge."* **Author's own tool; no evaluation,
benchmark or comparison.** And it is the precise thing Laycock calls *"automating the ceremony"* five
days later — **neither names the other**. Two caveats cut the other way, though:
[[tornhill-cannot-trust-agent-codescene-mcp]] argues on separate evidence that an LLM cannot reliably
judge code health, while Anthropic's own practice (below) is this position with a trust ladder attached.

**5. Distribute the reading** — Willison again
([[willison-conceptual-integrity-and-counting-lines-of-code]], 2026-08-19). Asked why a company needs
more than one engineer: *"the new limiting factor is cognitive capacity. I can churn out code a hundred
times faster. **I don't have the cognitive capacity to stay on top of 100 times the amount of code.** So
you still need a team of engineers, so you can **load balance that cognitive capacity across the
team**."* The only answer in which **team size is itself a verification instrument** — and the one
Brewster, a team of one, cannot use ("a team of one is a very badly designed team").

## Where the positions actually agree — read this before the four-corner version

The five-way framing overstates the distance, and the overlap is where the useful engineering is.

- **Laycock and Tornhill agree more than their rhetoric implies.** Both **reject line-by-line reading of
  everything** as the instrument, and both **push everything deterministic into automation** — her
  "we really shouldn't still be arguing about whitespace in 2026" and constraints encoded as
  [[fitness-functions]], his "these rules and constraints need to be enforced. Deterministically." Their
  real split is narrower and sharper: **what carries knowledge transfer once review stops doing it.** She
  moves it into **people, earlier** — pairing, mobbing, team design sessions; he moves it into
  **artifacts** — a human-reviewed test suite, accumulated SKILLs, deterministic checks. People-earlier
  versus artifacts, not automation versus humanity.
- **Willison and Tornhill converge on the pivot itself** (verification ≠ review), from unrelated
  starting points and with no citation between them.
- **Brewster's practice is closer to Tornhill's than his sentence is.** He babysat the risky seams and
  leaned on a cheap external oracle; the difference is that Tornhill's triage is *systematic* and
  Brewster's was ad hoc, so his case reads as the same instinct without an instrument.
- **Osmani is the genuine outlier on principle**, because his answer keeps the review *ceremony* and
  changes only who sits in the chair — which is exactly Laycock's target.

## The dissent: the loss isn't in review at all

[[nick-tune]] ([[tune-no-rapport-with-a-model-you-didnt-code]], 2026-08-28) relocates the whole problem
upstream. Refining a domain model with an agent *"is not the same as writing the lines of code
yourself. I don't feel as connected… And that means the domain model is going to be worse because I'm
clearly missing some nuances that could lead to big modelling breakthroughs."* And: *"I'm struggling to
see how to get the same level of rapport with the model without actually writing the code. **Maybe it's
not even possible.**"*

If he is right, none of the five positions helps: the damage happens **before** there is code to read,
review never carried that function, and the cost is **unobservable** — a modelling breakthrough that
didn't happen leaves no failing test and no diff. It is the KB's only suggestion that this debt may be
*unpayable* rather than merely unpaid. **Thin capture; an inference from a stated feeling — a hypothesis
with a named mechanism, not a finding.** Note he and Laycock share the diagnosis ("understand systems,
not diffs") and split on whether her earlier-and-collaborative practices can supply what typing did.

## Why reading doesn't scale: the cost side

The dispute is a resource argument, not a discipline argument, and
[[tornhill-compressed-cognition-cost-of-faster-coding|Tornhill's *Compressed Cognition*]] (2026-05-07)
supplies the mechanism: agents **compress the decision timeline** ("complexity and decisions that used
to be spread over days in a single coding session"), working memory holds "3-4 things," and agent work
is an invitation to **self-interruption** — each question, diff, failed test or almost-right change
"pulls you into a new review-verify-steer decision." His conclusion is this page's premise:
*"Don't review details, verify them."* See [[attention-bottleneck]] for the budget being spent.

That page's numbers discipline applies here too: the trial he relays found developers **estimated a 20%
speedup and were 19% slower** — but **he names no study, date or link**, so it is an *unnamed controlled
trial as relayed by Tornhill*, and the felt-vs-measured gap is the point. **No page in this KB may
attribute it to a named study, lab or set of authors**, however tempting the guess; and the two figures
must stay distinct, because collapsing them destroys the finding.

## What the KB already had, and what it says to this page

- **Anthropic, in production** ([[willison-fireside-chat-claude-code-team]], on [[loop-engineering]]):
  code review **moved off humans over months** by finding files where automated review "catches 100% of
  the issues," then adding every incident's causing PR to an eval set so the metric cannot regress.
  **This directly contradicts Laycock's position and the KB does not resolve it.** She rejects
  *"an AI agent pretending to be the human reviewer so we can preserve exactly the same process at
  higher speed"* **on principle** — "automating the ceremony rather than questioning why the ceremony
  exists" — while Anthropic's version is that same move **with a measured trust ladder**, which is
  precisely the evidence her objection would demand. Both stand: it is a vendor team reporting on its
  own tool, and she is Thoughtworks' CTO on Thoughtworks' own channel with no data at all. The
  contradiction is recorded, not adjudicated, here and on [[loop-engineering]].
- **[[dilger-lights-off-software-factory-dead-end|Dilger's layers of trust]]** (on
  [[software-factory]]): executable specs before code → static gates with defined consequences (files
  changed outside the slice = immediate fail) → a **2–3 minute structural** review that is explicitly
  not functional, "at this point we already know it works." Independently close to position 3, from the
  Event-Modeling side, and the most detailed *ladder* anyone in the KB has published.
- **[[addyosmani-own-the-outer-loop|Answerability]]** and
  [[willison-directly-responsible-individuals|the DRI rule]]: whatever instrument you choose, the
  accountable party is human. Every position here is a claim about *instruments*, none about
  responsibility.
- **[[dudycz-fork-can-you-own-it|Dudycz]]**: LLMs changed the cost of producing code, not of owning it.
- **[[khononov-value-of-90-percent-done-never-lower|Khononov]]**: *"The value of being 90% done, or even
  99% done, has never been lower than in the AI era."* A slogan for the problem — an 86-character
  unargued post, and no position in the dispute.

## The seam to the focus area

Every "other way to verify" in this dispute is, structurally, an **executable specification agreed
before the code exists**: Tornhill's e2e-tests-first, Dilger's specs-before-code, Wilger's
[[given-when-then]] acceptance gates per [[slice]]. [[event-modeling]] has been producing exactly that
artifact for a decade, which makes it a candidate answer to the verification burden rather than a
neighbour of it — and, per Tune, possibly the answer to the modelling-rapport problem too: the human
keeps the modelling act and delegates the typing ([[model-as-code-vs-model-as-language]],
[[event-modeled-agent-design]]). That inference is the KB's, not any author's.

## What would settle any of this

Nothing in this batch measures anything. The quantity nobody reports is the one Tornhill's product post
gestures at and does not supply: **the intervention rate** — how often reading the code would actually
have caught something the other instruments missed, and of what severity. Until someone publishes that,
all five positions are calibrated guesses by people with different jobs (a solo maintainer, a CTO of a
consultancy, a tool vendor, a DevRel author, a blogger-practitioner), and the differences track the jobs
at least as well as they track the evidence.

## Related

[[comprehension-debt]] · [[attention-bottleneck]] · [[loop-engineering]] · [[software-factory]] ·
[[fitness-functions]] · [[autonomy-ladder]] · [[given-when-then]] · [[ai-readable-code]] ·
[[agent-governance]] · [[guardian-agents]] · [[agentic-coding]] · [[spec-driven-development]] ·
[[agent-observability-and-evals]] · [[rachel-laycock]] · [[adam-tornhill]] · [[simon-willison]] ·
[[nick-tune]] · [[addy-osmani]] · [[rick-brewster]] · [[martin-dilger]]
