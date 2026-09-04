---
title: "Ingest deltas — Batch D: the verification burden (13 captures)"
type: output
created: 2026-09-04
updated: 2026-09-04
sources: [willison-brewster-cannot-review-180000-lines, laycock-maybe-we-shouldnt-be-reviewing-all-this-code, tornhill-controlling-the-uncertainty-machine, tornhill-compressed-cognition-cost-of-faster-coding, tune-no-rapport-with-a-model-you-didnt-code, willison-more-than-just-code-review, willison-conceptual-integrity-and-counting-lines-of-code, laycock-the-conductor-developer, osmani-agentic-code-review-skill-five-axes, tornhill-task-uncertainty-decides-what-code-you-read, tornhill-ai-induced-code-smells-codehealth-mcp, tornhill-beyond-lambdas-raising-the-abstraction-level, khononov-value-of-90-percent-done-never-lower]
tags: [ingest-deltas, verification-burden, work-order]
---

# Ingest deltas — Batch D: the verification burden (13 captures)

**Scope.** 13 raw captures ingested; **13 new pages in `wiki/sources/`**, all written, one per capture,
`raw_file:` keys exact and verified by the CLAUDE.md backlog query. I touched nothing in
`wiki/entities/`, `wiki/concepts/`, `index.md`, `overview.md`, `log.md` — this file is the work order
for those, applied serially by the orchestrator. **21 items**, most-important-first.

**Source pages created** (for `index.md` / `log.md` housekeeping — item 21):
`willison-brewster-cannot-review-180000-lines` ·
`laycock-maybe-we-shouldnt-be-reviewing-all-this-code` ·
`tornhill-controlling-the-uncertainty-machine` ·
`tornhill-compressed-cognition-cost-of-faster-coding` ·
`tune-no-rapport-with-a-model-you-didnt-code` · `willison-more-than-just-code-review` ·
`willison-conceptual-integrity-and-counting-lines-of-code` · `laycock-the-conductor-developer` ·
`osmani-agentic-code-review-skill-five-axes` ·
`tornhill-task-uncertainty-decides-what-code-you-read` ·
`tornhill-ai-induced-code-smells-codehealth-mcp` ·
`tornhill-beyond-lambdas-raising-the-abstraction-level` ·
`khononov-value-of-90-percent-done-never-lower`

## The live disputes this batch introduces — do not resolve any of them

1. **Does code review scale, and if not, what replaces it?** Five positions, all from 2026-05→09, none
   citing another: **accept the debt** (Brewster: "I cannot possibly review 180,000 lines of code");
   **relocate what review is for, then review by exception** (Laycock); **triage by task uncertainty and
   substitute tests + deterministic enforcement** (Tornhill); **automate the gate with an agent
   reviewer** (Osmani); **distribute the reading across a team** (Willison, "load balance that cognitive
   capacity"). → items 1, 3.
2. **Laycock vs Osmani, head-on.** Osmani ships an agentic review skill — *"The review is your quality
   gate… Run /review before you merge"* (08-28). Laycock, five days later: *"I don't think the answer is
   an AI agent pretending to be the human reviewer so we can preserve exactly the same process at
   higher speed. That's automating the ceremony rather than questioning why the ceremony exists."*
   Neither names the other. → items 1, 15.
3. **Laycock vs an existing KB page.** `loop-engineering` records Anthropic's own practice of **moving
   code review off humans** onto automated review that "catches 100% of the issues" in selected files,
   with an eval set added after every incident ([[willison-fireside-chat-claude-code-team]]). That is
   the automate-the-gate position *with* a measured trust ladder — i.e. the best counter to Laycock's
   principle, already in the wiki. → items 1, 10.
4. **Laycock vs Tornhill on parallelism.** She reports engineers running **8 / 10 / 12** agents in
   parallel and treats conducting at that width as the emerging job; he runs **"one long-running
   maintenance task and one focus task. Never more,"** and calls the twenty-agent ambition "exactly the
   wrong thing to even consider" because "it is the parallelisation of human attention that does not
   scale." Both anecdote-grade; they agree on the premise (attention is scarce) and split on the
   response. → items 2, 19.
5. **Laycock vs Laycock (unreconciled, five weeks apart).** `The Conductor Developer` (07-31): human
   attention is the bottleneck. `Maybe We Shouldn't Be Reviewing All This Code` (09-02): the remedy is
   pairing, mobbing and team design sessions — which spend *more* attention per unit of code. She never
   addresses the tension. → items 1, 2, 4.
6. **Is LOC meaningful?** Willison defends it (a hard human ceiling makes it an indicator, under a
   quality proviso); Tornhill's *Beyond Lambdas*, same fortnight: "lines of code are not a finite
   resource," and he has elsewhere jabbed at "productivity mistaken for lines of code produced." → items
   6, 8.
7. **Where is the loss located — review, or modelling?** Tune says the other four are answering the
   wrong question: rapport with a domain model comes from writing the code, review never carried it, and
   *"maybe it's not even possible"* to get it otherwise. The only claim in the batch that the debt may
   be **unpayable**. → items 1, 3, 13.
8. **Is the existing `comprehension-debt` defence still tenable?** That page currently prescribes "read
   the diffs." Brewster, Tornhill and Willison all say line-by-line reading has a hard ceiling. The page
   needs the ceiling, not a deletion of the defence. → item 3.

## Numbers this batch does NOT promote (carry these refusals forward)

- **20% estimated speedup vs 19% measured slowdown** (Tornhill, *Compressed Cognition*): the batch's
  only hard measurement, and **the study is never named, dated or linked** by him ("one of my favourite
  studies"). **Never write "Tornhill cites METR."** Cite as *an unnamed controlled trial as relayed by
  Tornhill*; keep the two figures distinct (one felt, one measured) — collapsing them destroys the
  finding.
- **Meta: significant LOC per human-landed diff +106% in a year** — double-relayed (Meta → Houck/DX →
  Laycock) and hedged "reportedly" by Laycock herself.
- **Median PR size +64%** — **DX's own data**, and DX sells developer-productivity measurement:
  VENDOR SELF-REPORT on its own market.
- **"If an agent can produce ten times the code"** (Laycock) — a rhetorical conditional, not a datum.
- **8 / 10 / 12 parallel agents** (Laycock) — one unnamed engineer plus "similar numbers from others";
  IMPRESSION NOT MEASUREMENT, and "beyond that, they become the bottleneck" is her inference.
- **180,000 agent-written lines / 700,000 existing / 20 years** (Brewster) — his own counts in a forum
  post; practitioner self-report about his own unreviewed code, no tooling or audit cited.
- **"50–60 lines a day / 200 is an incredibly good day / a thousand lines / a hundred times faster"**
  (Willison) — practitioner rules of thumb, no source or definition; his LOC defence also carries two
  provisos (same quality; huge skill) that must travel with it.
- **CodeHealth MCP AI-induced-smell statistics** — **the capture contains no figures at all**; the stats
  are in an unread screenshot. No page may attribute a smell frequency, ranking or safeguard-trigger
  rate to it.
- **Osmani's five-axis review skill** — author's own tool, no evaluation, benchmark or comparison.
- **"3-4 things" in working memory / Danziger et al. / Sweller** — cited by author name only, no links;
  borrowed psychology, not measurements of programmers.
- **Khononov's "90% done"** — an 86-character unargued aphorism (the whole post). A slogan, never a
  finding, never a corroborating second voice.
- Tune's *"the domain model is going to be worse"* — an inference from a stated feeling; hypothesis with
  a named mechanism, not a finding, and unfalsifiable as stated (a missed breakthrough leaves no trace).

---

## 1. `wiki/concepts/verification-burden.md` — **CREATE**

*Why:* the batch's centre of gravity. Five named positions on one question, from the same few weeks,
none citing another — and the KB currently has nowhere to hold the dispute: `comprehension-debt` holds
the *cost* of not reading, `loop-engineering` holds the *verify seam* of the loop, `agent-governance`
holds the *gate*, but no page holds the argument about **who reads the code and what replaces reading**.
Without it the dispute smears across nine source pages. Slug names the *problem*, so the page can carry
positions that contradict each other. `code-review` was rejected as a slug: the batch's whole point is
that review is one instrument, not the category.

Paste as the whole file:

```markdown
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
September 2026, from authors who do not cite one another.

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
the task had a **cheap external oracle** — a documented API, reimplemented behind a `/wine` flag. He is
also a team of one, which forecloses two of the four other answers.

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
days later. Two caveats cut the other way, though: [[tornhill-cannot-trust-agent-codescene-mcp]] argues
on separate evidence that an LLM cannot reliably judge code health, while Anthropic's own practice
(below) is this position with a trust ladder attached.

**5. Distribute the reading** — Willison again
([[willison-conceptual-integrity-and-counting-lines-of-code]], 2026-08-19). Asked why a company needs
more than one engineer: *"the new limiting factor is cognitive capacity. I can churn out code a hundred
times faster. **I don't have the cognitive capacity to stay on top of 100 times the amount of code.** So
you still need a team of engineers, so you can **load balance that cognitive capacity across the
team**."* The only answer in which **team size is itself a verification instrument** — and the one
Brewster, a team of one, cannot use ("a team of one is a very badly designed team").

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
trial as relayed*, and the felt-vs-measured gap is the point. Nothing in this KB may render it as
"Tornhill cites METR."

## What the KB already had, and what it says to this page

- **Anthropic, in production** ([[willison-fireside-chat-claude-code-team]], on [[loop-engineering]]):
  code review **moved off humans over months** by finding files where automated review "catches 100% of
  the issues," then adding every incident's causing PR to an eval set so the metric cannot regress.
  This is position 4 with a **measured trust ladder** — and therefore the strongest existing answer to
  Laycock's objection in principle. Vendor-team self-report about their own tool.
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
```

---

## 2. `wiki/concepts/attention-bottleneck.md` — **CREATE**

*Why:* three sources in this batch state the same premise in almost the same words — Laycock *"Human
attention is now the bottleneck,"* Willison *"the new limiting factor is cognitive capacity,"* Tornhill
*"it is the parallelisation of human attention that does not scale"* — and then give **three different
remedies** (widen the individual's span; distribute across a team; narrow the span). That is a
concept, and it is the *budget* every remedy on `verification-burden` draws down. Keeping it separate
from `verification-burden` matters: one page is about what to do with code, this one about the scarce
input, and the Laycock↔Tornhill parallelism collision lives here.

Paste as the whole file:

```markdown
---
title: Attention as the Bottleneck
type: concept
created: 2026-09-04
updated: 2026-09-04
sources: [laycock-the-conductor-developer, willison-conceptual-integrity-and-counting-lines-of-code, tornhill-compressed-cognition-cost-of-faster-coding, laycock-maybe-we-shouldnt-be-reviewing-all-this-code, tune-no-rapport-with-a-model-you-didnt-code]
tags: [attention-bottleneck, verification-burden, comprehension-debt, agentic-coding, live-dispute, focus]
---

# Attention as the Bottleneck

**Agents moved the constraint off code production and onto the human's attention.** Three independent
authors state that premise within six weeks of each other in 2026 — and then disagree about what to do
with it. This page holds the premise, the mechanism, and the three-way split on the remedy.

## The premise, three times

- **[[rachel-laycock]]** ([[laycock-the-conductor-developer]], 2026-07-31): *"AI didn't change what
  great software looks like. It changed what's scarce. **Human attention is now the bottleneck**."* She
  records a failed prediction of her own — she had expected the bottleneck to march down the lifecycle
  (coding → design → architecture → verification) — *"I was wrong."*
- **[[simon-willison]]** ([[willison-conceptual-integrity-and-counting-lines-of-code]], 2026-08-19):
  *"the new limiting factor is **cognitive capacity**. I can churn out code a hundred times faster. I
  don't have the cognitive capacity to stay on top of 100 times the amount of code."*
- **[[adam-tornhill]]** ([[tornhill-compressed-cognition-cost-of-faster-coding]], 2026-05-07): *"It is
  the **parallelisation of human attention** that does not scale."*

## The mechanism (Tornhill, 2026-05)

Why attention, and not time, is the binding constraint:

- **The timeline collapses.** Pre-2025 work "unfolded at human speed, which meant the decisions were
  naturally spaced out. Today, agents compress the timeline" — "complexity and decisions that used to be
  spread over days in a single coding session." His phrase: **"a lot more architecture per minute."**
- **Decision fatigue.** Decision quality decays across a session and recovers after breaks — and
  *"manual coding had a built-in pacing mechanism. That was our implicit recovery break. And it's now
  gone."*
- **Working memory is smaller than folklore says.** "Seven plus or minus two… was over-optimistic…
  we can, at best, hold **3-4 things** in our head at once and still be able to reason effectively."
- **Self-interruption, which he says is worse than external interruption.** The agent "asks a question,
  produces a diff, gets blocked by a missing tool, fails a test, or suggests a change that looks
  *almost* right but touches too much. **Each event pulls you into a new review-verify-steer
  decision.**"

*Sourcing discipline:* the psychology is cited **by author name only, unlinked** (Danziger et al. on
judicial rulings, Sweller on cognitive load, the "3-4 things" revision) and is analogy, not measurement
of programmers. His own pace claims ("I can usually sustain the pace for a couple of hours… based on
conversations with other engineers") are **IMPRESSION NOT MEASUREMENT**. And **NOT INDEPENDENT** on the
prescription — "automation and safeguards are the mechanisms for delivering trust, not manual
inspection" is argued by CodeScene's founder/CTO, who sells them.

## The one relayed measurement, and how to cite it

The same essay relays a controlled trial of experienced open-source developers: the AI-assisted group
**estimated a 20% speedup** and were **19% slower**. *"Even expert developers overestimate the AI impact
on developer productivity."* **Keep the two figures apart — one is felt, one is measured, and the gap is
the finding.** Tornhill **names no study, authors, date or link** ("one of my favourite studies"), so
this KB cites it as *an unnamed controlled trial as relayed by Tornhill* and **never** as
"Tornhill cites METR." It is the strongest available caution against the self-reported-speedup claims
that fill [[agentic-coding]] and [[loop-engineering]].

## Three remedies for one constraint — unresolved

| | Remedy | Source | Status |
|---|---|---|---|
| **Widen the span** | Become a conductor: orchestrate 8–12 agents; re-skill for attention, energy and decision management | Laycock | Anecdote + analogy |
| **Distribute it** | Keep a team so cognitive capacity can be load-balanced across people | Willison | Assertion |
| **Narrow it** | "One long-running agentic maintenance task… and one focus task. Never more" | Tornhill | Personal rule |

**The collision worth keeping visible.** Laycock reports an engineer "who regularly have eight AI agents
running in parallel. I've heard similar numbers from others. Ten. Twelve. Beyond that, they become the
bottleneck," and treats conducting at that width as the emerging shape of the job. Tornhill: *"I cannot
even think about twenty meaningful things to build, and even less so about the resulting cognitive
tax… It's exactly the wrong thing to even consider."* He pre-empts the obvious objection — "yes, I
understand sub-agents and machine parallelisation. That is not what I'm objecting to." **Both are
anecdote-grade: her 8/10/12 is hearsay from one unnamed engineer plus "others"; his ceiling of two is a
personal rule.** The KB has no measurement that settles it, and should not pick.

## The conductor model (Laycock, 2026-07)

The image, via Jacob Collier: a conductor "is first and foremost a great musician. They could play the
instruments themselves. That's not why they're standing on the podium… **It needs the conductor because
someone has to hold the whole system in their head.**" Agents are the musicians; the developer decides
which agent takes which problem, supplies context, evaluates what comes back, spots subtle mistakes, and
decides what deserves another iteration.

Its real payload is a **career** claim, not a metaphor: eight parallel streams "sounded like my job" as
CTO, and what she had to learn was **energy management, not time management** — "the challenge wasn't the
hours. It was the constant context switching. The endless stream of decisions." Hence the transferable
curriculum (*protect your attention; manage your energy; reduce unnecessary decisions; create systems
that help your brain, not just your calendar*) and the line the page exists for: **"We're redesigning
the tools, but we haven't started redesigning the job."** Her closing question — *"How do we redesign
engineering careers when human attention becomes the scarce resource?"* — is open in this KB.
**NOT INDEPENDENT** (Thoughtworks' CTO on Thoughtworks' own channel) and evidence-free by her own
framing. Note "a conductor must still be a musician" is the analogy's load-bearing constraint against
the "nobody needs to read code any more" reading.

## Consequences elsewhere in the KB

- **[[verification-burden]]** — this is the budget. Every proposed substitute for reading code (pair,
  mob, review tests, spot-check, run twelve agents) is a claim on the same scarce input, which is why
  Laycock's own two 2026 essays are unreconciled: attention is the bottleneck (July), and the remedy is
  attention-expensive pairing and team design sessions (September).
- **[[comprehension-debt]]** — attention is the currency the debt is denominated in; the cognitive
  ceiling is *why* the "read the diffs" defence has a limit.
- **[[multi-agent-orchestration]]** — the human-side ceiling on fan-out, next to CEAD's
  machine-side ceiling (~32 agents).
- **[[context-rot]] / [[token-budget-quality-cliff]]** — the machine analogues; "3-4 things" is the
  human context window.
- **[[tune-no-rapport-with-a-model-you-didnt-code|Tune]]** — the same scarce attention, spent upstream:
  the modelling insight that typing used to buy.
- **[[loop-engineering]]** — the "stay the engineer" caveats now have a stated resource limit rather
  than only a discipline argument.

## Related

[[verification-burden]] · [[comprehension-debt]] · [[multi-agent-orchestration]] ·
[[loop-engineering]] · [[agentic-coding]] · [[context-rot]] · [[token-budget-quality-cliff]] ·
[[team-topologies]] · [[software-factory]] · [[rachel-laycock]] · [[adam-tornhill]] ·
[[simon-willison]]
```

---

## 3. `wiki/concepts/comprehension-debt.md` — **UPDATE** (4 edits)

*Why:* this batch supplies the debt's **ceiling** (Brewster), its **third face** (Tune: models you
didn't build), and a **second failure mode** the page does not carry (conceptual integrity). It also
makes the page's current prescription — "read the diffs" — a claim that three sources in this batch
say has a hard limit. Do not delete the defence; bound it.

**3a. Frontmatter.** Add to `sources:` (keep existing entries):

```
willison-brewster-cannot-review-180000-lines, tune-no-rapport-with-a-model-you-didnt-code, willison-conceptual-integrity-and-counting-lines-of-code, laycock-maybe-we-shouldnt-be-reviewing-all-this-code, tornhill-task-uncertainty-decides-what-code-you-read
```

and set `updated: 2026-09-04`.

**3b. Bound the "read the diffs" defence.** Find this exact text in the third paragraph:

> caveats — read the diffs, move judgment upstream (a lit

Replace with:

> caveats — read the diffs (**but see the ceiling below**), move judgment upstream (a lit

**3c.** Insert this section immediately **before** the `## Related` heading:

```markdown
## The ceiling on "read the diffs" (2026-08/09)

The defence above assumes reading is a choice you can keep making. Three sources arriving within a
fortnight say it has a hard limit, and one of them is past it.

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
```

**3d.** In the `## Related` line, append:

```
· [[verification-burden]] · [[attention-bottleneck]] · [[willison-brewster-cannot-review-180000-lines]] ·
[[tune-no-rapport-with-a-model-you-didnt-code]] ·
[[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]] ·
[[willison-conceptual-integrity-and-counting-lines-of-code]] · [[rick-brewster]] · [[nick-tune]].
```

---

## 4. `wiki/entities/rachel-laycock.md` — **UPDATE** (3 edits)

*Why:* both remaining Laycock captures are now ingested (one of them the page explicitly names as
un-ingested — that note is stale and must go), and her two new pieces give her a second and third role
in the KB: the review-scaling position, and the attention-bottleneck premise. The unreconciled tension
between her own two essays is worth stating on her page, not hiding.

**4a. Frontmatter.** `sources:` becomes:

```
sources: [laycock-citizens-build-agents-execute-experts-govern, laycock-maybe-we-shouldnt-be-reviewing-all-this-code, laycock-the-conductor-developer]
```

and `updated: 2026-09-04`.

**4b. DELETE the now-stale paragraph** (the capture is ingested as of this batch). Remove in full:

> **One capture still un-ingested:** `raw/articles/laycock-the-conductor-developer.md` (2026-07-31), the
> earlier of her two pieces in `raw/`. It is the obvious companion to this one — the individual-role view
> next to the organisational view — and is the remaining Laycock item in the queue.

**4c.** Insert in its place (before `## Related`):

```markdown
## Two further essays, and a tension she leaves open (ingested 2026-09-04)

**[[laycock-the-conductor-developer|The Conductor Developer]]** (2026-07-31) is the individual-role view
beside the organisational one, and it opens with a **prediction she records as failed**: she expected
the bottleneck to march down the lifecycle (coding → design → architecture → verification) and reports
*"I was wrong."* Instead: **"AI didn't change what great software looks like. It changed what's scarce.
Human attention is now the bottleneck."** The developer becomes a conductor — *"someone has to hold the
whole system in their head"* — and the analogy's constraint is that a conductor is first a musician.
Its real payload is a career claim: eight parallel work streams "sounded like my job," what she had to
learn as CTO was **energy management, not time management**, and *"we're redesigning the tools, but we
haven't started redesigning the job."* Her 8 / 10 / 12 parallel-agent figures are **hearsay** (one
unnamed engineer, plus "similar numbers from others") and must not be cited as a capacity finding. See
[[attention-bottleneck]], where her "widen the span" answer sits against
[[adam-tornhill|Tornhill's]] flat refusal of human-side parallelism.

**[[laycock-maybe-we-shouldnt-be-reviewing-all-this-code|Maybe We Shouldn't Be Reviewing All This Code]]**
(2026-09-02) is her sharpest and most consequential piece here — a named position in the KB's
[[verification-burden]] dispute, written as a response to Brian Houck (DX) after they disagreed on a
panel. She grants that AI outpaces review and that review carries knowledge transfer, mentoring,
ownership and architectural understanding — then asks *"why are we waiting until code review to do all
of those things?"* Each function moves earlier (pairing, mob programming, team design sessions,
[[fitness-functions]] for architectural constraints, automation for anything deterministic), leaving
**review by exception**. Two lines to keep: *"I don't think the answer is an AI agent pretending to be
the human reviewer so we can preserve exactly the same process at higher speed. That's automating the
ceremony rather than questioning why the ceremony exists"* — which lands squarely on
[[osmani-agentic-code-review-skill-five-axes|Osmani's shipped review skill]] and on Anthropic's own
practice recorded in [[loop-engineering]] — and **"We need engineers to understand systems, not
diffs."**

**The tension between her own two essays is unresolved and worth holding:** attention is the scarce
resource (July), and the remedy is pairing, mobbing and team design sessions (September) — practices
that spend *more* human attention per unit of code. She never addresses it. Her two relayed figures
(Meta LOC per human-landed diff **+106%**; median PR size **+64%**) come via **Houck at DX, a vendor
selling developer-productivity measurement**, the first double-relayed and hedged "reportedly" by her;
neither is a KB-grade number, and Houck's own piece is not in `raw/` — the KB holds one side of that
exchange.
```

**4d.** In `## Related` append `· [[verification-burden]] · [[attention-bottleneck]] ·
[[fitness-functions]] · [[comprehension-debt]]`, and extend the closing `_Source pages:_` line to list
all three source pages.

---

## 5. `wiki/entities/adam-tornhill.md` — **UPDATE** (3 edits)

*Why:* four new Tornhill captures, and one of them (*Compressed Cognition*) was previously known to the
KB only as a line item in the series index — it is now a full page carrying the batch's only
measurement. His August–September position (triage what you read; enforce the rest) is a substantive
addition to his entity profile and needs its vendor marker attached where the remedy is stated.

**5a. Frontmatter.** Append to `sources:`:

```
tornhill-controlling-the-uncertainty-machine, tornhill-task-uncertainty-decides-what-code-you-read, tornhill-compressed-cognition-cost-of-faster-coding, tornhill-beyond-lambdas-raising-the-abstraction-level, tornhill-ai-induced-code-smells-codehealth-mcp
```

and set `updated: 2026-09-04`. Add `verification-burden` to `tags:`.

**5b.** Insert this section immediately **before** the paragraph beginning *"Not everything he writes is
on this thread."*:

```markdown
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
to see."* That post's statistics are **in an unread screenshot — it carries no figures, and no page may
cite one from it.**

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
```

**5c.** Extend the closing `_Source pages:_` list with the five new pages.

---

## 6. `wiki/entities/simon-willison.md` — **UPDATE** (2 edits)

*Why:* three new Willison captures, two of them his own argument and one a relay. They give him a
distinct position in the verification dispute (**verification ≠ review**, plus "distribute the reading
across a team") and the KB's primary for *conceptual integrity*.

**6a. Frontmatter.** Append to `sources:`:
`willison-more-than-just-code-review, willison-conceptual-integrity-and-counting-lines-of-code, willison-brewster-cannot-review-180000-lines`;
set `updated: 2026-09-04`.

**6b.** Insert immediately **before** the `## Watch` heading:

```markdown
## Verification ≠ review, and the cognitive ceiling (2026-08/09)

Three August–September pieces make him a named voice in the [[verification-burden]] dispute.

**[[willison-more-than-just-code-review]]** (08-22, four sentences) is the pivot the whole dispute turns
on: the key skill is to *"confidently instruct"* an agent and *"confidently verify"* the result, and
*"**Eyeballing every line of code has never been the most effective way to validate a change**."* Note
the claim is about software engineering generally, not about agents — and that he keeps line-by-line
review on the shelf ("sometimes this involves reviewing every line"), which makes it a triage position
rather than an abolition. [[adam-tornhill]] arrives at the same claim six days later, independently:
the batch's strongest convergence.

**[[willison-conceptual-integrity-and-counting-lines-of-code]]** (08-19, from a *Talking Postgres*
transcript) adds two things. A **defence of lines of code** — meaningful only because human output was
hard-capped, and only under his own provisos ("as long as the code is the same quality: maintainable,
tested" and "it takes a huge amount of skill") — and the constraint that matters more: *"the new
limiting factor is **cognitive capacity**… I don't have the cognitive capacity to stay on top of 100
times the amount of code. So you still need a team of engineers, so you can **load balance that
cognitive capacity across the team**."* That is the only remedy in the KB where **team size is itself a
verification instrument** ([[attention-bottleneck]]). The second half is the KB's primary for
**conceptual integrity** (Brooks): with agents, "your software grows little weird bumps in funny
different directions," because the friction that used to enforce discipline — "that would take me a
week — I cannot justify that" — is gone. All his numbers here are practitioner rules of thumb
("50 or 60 lines… 200 is an incredibly good day… a hundred times faster") and must not be promoted to
figures.

**[[willison-brewster-cannot-review-180000-lines]]** (09-02) is a **quotation post**, and the entry
where his contribution is selection rather than argument: [[rick-brewster]] on ~180,000 agent-written
lines in Paint.NET — *"I cannot possibly review 180,000 lines of code."* Read against his own two
pieces, the pairing is pointed: Brewster is a **team of one** ("a team of one is a very badly designed
team") with no substitute instrument, which is what "there are other ways" looks like when nobody
supplies one.
```

Also extend the closing `_Sources:_` line with the three new pages.

---

## 7. `wiki/entities/nick-tune.md` — **UPDATE** (2 edits)

*Why:* his third contribution here, and the one that is a *problem statement* rather than a mechanism —
worth recording precisely because it is unlike his other two, and because it sits in tension with his
own enforcement work.

**7a. Frontmatter.** Append `tune-no-rapport-with-a-model-you-didnt-code` to `sources:`;
`updated: 2026-09-04`; add `comprehension-debt` to `tags:`.

**7b.** Insert immediately **before** the `## Related` heading:

```markdown
## The rapport problem — a stated open problem, not a mechanism (2026-08-28)

His third contribution is unlike the other two: no DSL, no substrate, no proposal.
[[tune-no-rapport-with-a-model-you-didnt-code]] reports that agents are *"not that good at [domain
modelling] by default (that's the nice way of putting it)"* — and then makes the sharper claim, which
survives the agents getting better: *"discussing and refining a domain model is not the same as writing
the lines of code yourself. I don't feel as connected… **And that means the domain model is going to be
worse** because I'm clearly missing some nuances that could lead to big modelling breakthroughs."*
Ending: *"I'm struggling to see how to get the same level of rapport with the model without actually
writing the code. **Maybe it's not even possible.**"*

This relocates the [[verification-burden]] from review to **modelling**: the loss happens before there
is code to read, so no review regime, test boundary or agent reviewer addresses it — and it is
**unobservable**, since a modelling breakthrough that didn't happen leaves no trace. It is the KB's only
suggestion that [[comprehension-debt]] may be **unpayable** rather than merely unpaid. Note the tension
with his own [[nick-tune-enforced-application-architecture-agents-humans|Rivière]] work: build
enforcement guarantees the *shape* of code nobody wrote, and nothing in a build enforces modelling
insight. **Thin capture**: a short LinkedIn post, no evidence, and a quality claim inferred from a
stated feeling — a hypothesis with a named mechanism, not a finding.
```

Add `· [[verification-burden]] · [[comprehension-debt]] · [[vibe-modeling]]` to `## Related` and the new
page to the closing `_Source pages:_` line.

---

## 8. `wiki/concepts/ai-readable-code.md` — **UPDATE** (2 edits)

*Why:* `Beyond Lambdas` is a new worked example at expression level (the series' newest), and the page
lacks the argument that ties this whole strand to the review dispute: cheap reading is the
*precondition* for reading selectively. Also settles the LOC clash inside the KB.

**8a. Frontmatter.** Append to `sources:`:
`tornhill-beyond-lambdas-raising-the-abstraction-level, tornhill-controlling-the-uncertainty-machine`;
`updated: 2026-09-04`.

**8b.** Insert immediately **before** the `## Open question` heading (so it sits with the other Tornhill
sections and above the synthesis question):

```markdown
## Name the nameless — abstraction level at expression scale (Tornhill, 2026-09-01)

[[tornhill-beyond-lambdas-raising-the-abstraction-level|Beyond Lambdas]] is the series' newest
walkthrough and its smallest-scale lever. The asymmetry it turns on: *"The nice thing about lambdas is
that they optimize for **writing** code… The bad thing about lambdas is that they optimize for writing
code. They do so at the expense of **reading** code, which is arguably a much more frequent activity."*
A three-line `map/filter/sum` stream over dice rolls is "trivial" in mechanics and opaque in purpose —
"it could be anything" — until the lambdas are named as domain operations (`AttackRoll::applyStrengthModifier`,
`AttackRoll::isSuccessfulHit`), and in Clojure a step further, naming the **pipeline elements**
themselves so "the code now reads like a story." His line: **"Anonymous functions are anonymous
thoughts."**

Three claims worth keeping beyond the refactoring:

- **Abstractions need not be reused to be justified.** "Abstractions can be simple. Ridiculously
  simple… **Lines of code are not a finite resource.**" His test is about reading, not economy: *"if it
  elevates the level of the code, then it has earned its rights."* A deliberate break with the DRY-first
  reflex, and — unengaged by either author — the opposite stance from
  [[willison-conceptual-integrity-and-counting-lines-of-code|Willison's]] hard-ceiling defence of LOC as
  a productivity indicator. Both are on-thread; the KB holds both.
- **The target is reconstruction work**, the same target as
  [[tornhill-clear-design-principles-agentic-age|CLEAR]]: new tasks arrive inside an existing codebase,
  and "the closer our abstractions reflect the problem domain," the less has to be reconstructed before
  a safe change.
- **This is the precondition for reading selectively.** Every remedy on [[verification-burden]] —
  Tornhill's own included — assumes a human or agent can cheaply recover intent from a fragment. Naming
  is how that stays affordable: the *supply* side of a reading budget whose *demand* side he prices in
  [[tornhill-compressed-cognition-cost-of-faster-coding|Compressed Cognition]].

A style argument with a toy example: one D&D snippet in two languages, no measurement, and the agent
claim is by reference to CLEAR rather than tested. The nearest actual evidence remains
[[borg-tornhill-code-for-machines-not-just-humans]] and the LLM identifier-name result relayed in
[[tornhill-opinionated-guide-to-naming]] — neither about lambdas.

## Enforce what you don't inspect (Tornhill, 2026-08-20)

The page's design advice acquires a *reason* here. If nobody reads all the code
([[verification-burden]]), then AI-readable code stops being a courtesy to future humans and becomes
the load-bearing guarantee: [[tornhill-controlling-the-uncertainty-machine]] argues "AI amplified the
need for maintainable code" because "successful features attract change," and answers the obvious
question — how do you keep uninspected code maintainable? — with a **multi-layered safety net**:
accumulated SKILLs capturing style and architecture rules, plus **deterministic** enforcement (linters,
vulnerability scanners, custom architectural and e2e checks, and CodeScene's CodeHealth MCP).
*"These rules and constraints need to be enforced. Deterministically."* **VENDOR SELF-REPORT** — the
prescription names his own company's product; the premise it rests on is his separate argument that an
LLM cannot reliably self-assess code health ([[tornhill-cannot-trust-agent-codescene-mcp]]). See also
[[fitness-functions]], where the same move appears as a build-time constraint.
```

Extend the closing `_Sources:_` line with both new pages.

---

## 9. `wiki/concepts/agentic-coding.md` — **UPDATE** (2 edits)

*Why:* the page's `## Caution` section carries vendor issue-rate claims and a peer-reviewed code-health
primary, but **nothing about the gap between felt and measured productivity** — the single most useful
caution available for a page whose "State of play" relays adoption percentages. Also the review-burden
dispute needs a pointer from the main practice page.

**9a. Frontmatter.** Append to `sources:`:
`tornhill-compressed-cognition-cost-of-faster-coding, willison-more-than-just-code-review, laycock-maybe-we-shouldnt-be-reviewing-all-this-code`;
`updated: 2026-09-04`.

**9b.** Insert at the **end of the `## Caution` section**, immediately before the
`## The ownership caveat — "LLM as a fork"` heading:

```markdown
**Felt speed is not measured speed, and the gap is measurable.** The strongest caution on this page is
not about code quality but about the productivity claim itself.
[[tornhill-compressed-cognition-cost-of-faster-coding|Tornhill]] relays a controlled trial of
experienced open-source developers in which the AI-assisted group **estimated a 20% speedup** and were
**19% slower** than the control group — "even expert developers overestimate the AI impact on developer
productivity." **Cite this carefully: he names no study, date or link** ("one of my favourite
studies"), so it is *an unnamed controlled trial as relayed*, **not** "Tornhill cites METR," and the two
figures must stay distinct — one is what developers felt, one is what was measured. His proposed
mechanism is **self-interruption**: agentic work is a stream of questions, diffs, failed tests and
almost-right changes, each of which "pulls you into a new review-verify-steer decision." Everything on
this page that reports a speedup as an impression (and most of the KB's practitioner speed claims are
impressions) should be read against it. See [[attention-bottleneck]].

**And the verification cost has its own dispute now.** Who reads agent-written code, and what replaces
reading, is an open five-way argument among Brewster, Laycock, Tornhill, Osmani and Willison — held on
[[verification-burden]] rather than resolved here. The short version: [[simon-willison]] —
*"eyeballing every line of code has never been the most effective way to validate a change"*
([[willison-more-than-just-code-review]]); [[rachel-laycock]] — don't automate review, move what review
is *for* earlier and review by exception ([[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]]).
```

---

## 10. `wiki/concepts/loop-engineering.md` — **UPDATE** (2 edits)

*Why:* the page's vendor-team instance (Anthropic moving code review off humans onto automated review
that "catches 100% of the issues") is now **directly contested on principle** by a named source in the
KB. That contest belongs on the page — per CLAUDE.md, when sources conflict, say so.

**10a. Frontmatter.** Append to `sources:`:
`laycock-maybe-we-shouldnt-be-reviewing-all-this-code, willison-more-than-just-code-review, tornhill-controlling-the-uncertainty-machine`;
`updated: 2026-09-04`.

**10b.** Insert at the **end of the `## A vendor-team worked instance ([[willison-fireside-chat-claude-code-team|Claude Code team]])`
section** (immediately before `## Relationship to neighbours`):

```markdown
**Contested on principle (2026-09).** "Code review moved off humans" is exactly the move
[[rachel-laycock]] rejects: *"I don't think the answer is an AI agent pretending to be the human
reviewer so we can preserve exactly the same process at higher speed. **That's automating the ceremony
rather than questioning why the ceremony exists**"*
([[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]]). Her alternative is to relocate what review
is *for* — knowledge transfer, architectural alignment, collective ownership — into pairing, team design
sessions and [[fitness-functions]], and then review by exception. Both belong here and the KB does not
pick: Anthropic's version is the automate-the-gate position **with a trust ladder** (per-file evidence
that the automated reviewer catches everything, plus an eval-set regression guard after each incident),
which is precisely the evidence Laycock's objection would demand — and it is also a **vendor team
reporting on its own tool**, while she is Thoughtworks' CTO on Thoughtworks' own channel and offers no
data at all. The full five-way argument, including
[[tornhill-controlling-the-uncertainty-machine|Tornhill's]] uncertainty triage and
[[willison-more-than-just-code-review|Willison's]] "eyeballing every line was never the best
verification," is on [[verification-burden]]; the resource ceiling under it is on
[[attention-bottleneck]].
```

---

## 11. `wiki/concepts/fitness-functions.md` — **UPDATE** (2 edits)

*Why:* the page has mechanism (Böckeler's sensors, Tune's Rivière) but no statement of **what fitness
functions are for once nobody reads every diff**. Laycock supplies exactly that, and it is the clearest
purpose statement available.

**11a. Frontmatter.** Append `laycock-maybe-we-shouldnt-be-reviewing-all-this-code` to `sources:`;
`updated: 2026-09-04`.

**11b.** Insert immediately **before** the `## Related` heading:

```markdown
## What they are *for* when nobody reads every diff (Laycock, 2026-09)

[[rachel-laycock]] gives the purpose statement this page implies but never states
([[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]]). Her argument is that code review has been
carrying six jobs at once — "quality gate, security check, architecture review, mentoring mechanism,
knowledge-sharing system, ownership model" — and that agent output volume breaks the arrangement. Each
job then moves to where it belongs, and fitness functions get one specific job: *"If we want
**architectural alignment**, design together… and then **encode the important constraints as fitness
functions**."* Everything deterministic (formatting, linting, known security problems) is automated
outright — "we really shouldn't still be arguing about whitespace in 2026" — and what is left for humans
is **review by exception**.

So on her account a fitness function is not a supplement to review but the **mechanism that carries
architectural intent forward when per-diff human inspection stops being the gate**. That is the same
role [[nick-tune]] builds machinery for above (make the violation fail the build) and the same role
[[adam-tornhill]] assigns to deterministic checks in [[tornhill-controlling-the-uncertainty-machine]]
("enforce what you don't inspect" — **VENDOR SELF-REPORT**, his stack includes CodeScene's own MCP).
It is also, as she says, useless against the classes of problem
[[fowler-bockeler-maintainability-sensors|Böckeler]] identifies and against
[[willison-conceptual-integrity-and-counting-lines-of-code|conceptual-integrity drift]], where each
individual change is defensible and the whole stops cohering — which is why her list keeps humans for
"a change with a huge blast radius" and for "simply something where the team says, 'I'm not confident
about this.'" **NOT INDEPENDENT**: Thoughtworks' CTO on martinfowler.com prescribing a
Thoughtworks-originated practice, with no data. See [[verification-burden]].
```

Add `· [[verification-burden]]` to `## Related` and the new page to the closing `_Sources:_` line.

---

## 12. `wiki/concepts/autonomy-ladder.md` — **UPDATE** (2 edits)

*Why:* the page models autonomy as one dial. Tornhill's rule moves **two dials with one judgement** —
autonomy *and* human review depth — which is a genuine refinement, and the coding-agent instance the
page currently lacks (its rungs are operations/data-quality shaped).

**12a. Frontmatter.** Append
`tornhill-controlling-the-uncertainty-machine, tornhill-task-uncertainty-decides-what-code-you-read`
to `sources:`; `updated: 2026-09-04`.

**12b.** Insert immediately **before** the `## Related` heading:

```markdown
## Task uncertainty moves two dials at once (Tornhill, 2026-08)

The ladders above stage **autonomy**. [[adam-tornhill]] adds a second dial moved by the same judgement
([[tornhill-controlling-the-uncertainty-machine]], stated compactly in
[[tornhill-task-uncertainty-decides-what-code-you-read]]): *"That task uncertainty drives both the
relative autonomy I grant a coding agent, **and the effort I spend reviewing the resulting code**."*

His **uncertainty** is defined operationally, and usefully: *how much of the intended solution's
behavior and structure is already understood and represented in the existing system.* That makes it a
property of the task-in-this-codebase rather than of the task in the abstract — a bug fix is
low-uncertainty because "the majority of bugs are local and contextual," so he inspects **the evidence
for the fix** (reproduce, fix, new tests pass) rather than the code; the first iteration of a novel
feature has no architectural home, so he inspects **structure and patterns** to establish one, and later
iterations on the same feature can then be more autonomous. Autonomy therefore *rises as uncertainty
falls*, and each completed high-uncertainty task lowers the uncertainty of its successors — a ratchet
the staged ladders on this page do not model.

Two notes. The gate is a **human-reviewed e2e test suite**, not a permission tier — the boundary is an
artifact, not a policy. And this is a **single practitioner's rule**: no defect data, no comparison
against reading the code, and the enforcement layer he relies on includes his own company's product
(**VENDOR SELF-REPORT**; he is CodeScene's founder/CTO). See [[verification-burden]].
```

Add `· [[verification-burden]] · [[agentic-coding]] · [[adam-tornhill]]` to `## Related` and both pages
to `_Source pages:_`.

---

## 13. `wiki/concepts/domain-driven-design.md` — **UPDATE** (2 edits)

*Why:* the page is a 30-line stub whose only content is the Event-Modeling relationship, and this batch
lands the sharpest available caution on **agent-assisted domain modelling** from a recognised DDD voice.
It is also where the "typing was doing epistemic work" claim belongs.

**13a. Frontmatter.** `sources:` becomes
`[semaphore-dymitruk-event-modeling, tune-no-rapport-with-a-model-you-didnt-code]`;
`updated: 2026-09-04`; add `agentic-ai` to `tags:`.

**13b.** Insert immediately **before** the `## Related` heading:

```markdown
## Can you model with an agent? The rapport problem (Tune, 2026-08-28)

The open question DDD faces in the agent era, stated by [[nick-tune]]
([[tune-no-rapport-with-a-model-you-didnt-code]]): agents are *"not that good at [domain modelling] by
default,"* and — the claim that outlives that — *"discussing and refining a domain model is not the same
as writing the lines of code yourself. I don't feel as connected, I don't feel that the model is as
deeply embedded in my mind as it would be if I wrote the code. **And that means the domain model is
going to be worse** because I'm clearly missing some nuances that could lead to big modelling
breakthroughs."* His conclusion: *"I'm struggling to see how to get the same level of rapport with the
model without actually writing the code. **Maybe it's not even possible.**"*

The implicit premise is worth naming: **writing the code was a mode of thinking about the domain**, not
a transcription step — which is precisely what [[spec-driven-development]] assumes away, and what
[[tornhill-ai-readable-code-series|Tornhill's "SDD and the Illusion of Known Scope"]] attacks from the
implementation side ("implementation was never just typing — it's discovery and learning").

Two counter-considerations the post does not raise. **DDD already had this problem**: [[event-storming]]
and [[domain-discovery]] exist because a *group* must reach rapport with a model no single member typed,
and ubiquitous language is the mechanism for transferring it. Whether those formats extend to a
human/agent pair is the open question — and the KB's candidate answer is to keep the modelling act and
delegate only the typing ([[event-modeling]], [[model-as-code-vs-model-as-language]],
[[event-modeled-agent-design]]). Second, [[tornhill-beyond-lambdas-raising-the-abstraction-level|naming
the domain into the code]] is the mechanism for encoding whatever insight you do have into code an agent
typed; it does not manufacture the insight. **Thin capture** — a short LinkedIn post; a quality claim
inferred from a stated feeling, and unobservable by construction (a missed breakthrough leaves no
trace). See [[comprehension-debt]] and [[verification-burden]].
```

Add `· [[vibe-modeling]] · [[comprehension-debt]] · [[verification-burden]] · [[nick-tune]] ·
[[domain-discovery]]` to `## Related` and the new page to `_Source pages:_`.

---

## 14. `wiki/concepts/software-factory.md` — **UPDATE** (2 edits)

*Why:* the page holds Dilger's *"you can't do full code reviews… but you can't do no code-reviews
either"* bind and his layers-of-trust answer. Brewster is the **empirical extreme** of the other horn
of that bind — the dark-factory outcome as a solo case, in public, at 180k lines — and belongs beside
it.

**14a. Frontmatter.** Append `willison-brewster-cannot-review-180000-lines` to `sources:`;
`updated: 2026-09-04`.

**14b.** Insert immediately **after** the paragraph ending *"Failures are disposed of, not repaired —
the slice goes back to 'planned' and a learning is recorded."* (i.e. before *"Two things this
contributes that the page lacked"*):

```markdown
**The other horn, taken in public.** Dilger's bind has an empirical extreme now:
[[rick-brewster]], Paint.NET's maintainer, shipped ~180,000 agent-written lines into a ~700,000-line
codebase he has maintained 20+ years and said so plainly — *"it has not been thoroughly reviewed, it's
more 'trust me bro' style. **I cannot possibly review 180,000 lines of code**"*
([[willison-brewster-cannot-review-180000-lines]]). That is "no code-reviews," chosen knowingly, with
none of the layers of trust above: no executable spec, no static gate, no structural review. Three
things make it survivable rather than reckless, and all three are absent from the general case — a
**documented external spec** (a clean-room reimplementation of Direct2D, so the oracle lives outside the
code and outside his head), an **opt-in path** behind a `/wine` flag, and **targeted babysitting** of
the risky seams ("the COM equivalent of `AddRef()`"). His own counts, in a forum post: practitioner
self-report, not measurement. Read it as the boundary case that shows what the ladder is *for*, and note
that Dilger's incident-shaped worry — "production burning and no one there to navigate the code base" —
is the exposure Brewster has accepted for a 20-year product.
```

Add the new page to the closing `_Sources:_` line.

---

## 15. `wiki/entities/addy-osmani.md` — **UPDATE** (2 edits)

*Why:* one new capture, and it puts him on the *opposite* side of a named dispute from Laycock — worth
recording on his page, because his profile currently reads as uniformly "stay the engineer" and this is
a concrete tooling bet with no evaluation behind it. (Note: his frontmatter `sources:` list is already
missing several of his source pages; adding this one is not a fix for that, and a lint pass should
reconcile the whole list.)

**15a. Frontmatter.** Append `osmani-agentic-code-review-skill-five-axes` to `sources:`;
`updated: 2026-09-04`.

**15b.** Insert immediately **before** the closing `_Sources:_` line:

```markdown
**The review skill, and the dispute it lands in (2026-08-28).**
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
```

Extend the closing `_Sources:_` line with the new page.

---

## 16. `wiki/entities/vlad-khononov.md` — **UPDATE** (2 edits)

*Why:* one thin new capture. Record it for **liveness** and for the position, with the "do not build on
this" marker attached, so a later sweep doesn't mistake a slogan for an argument.

**16a. Frontmatter.** Append `khononov-value-of-90-percent-done-never-lower` to `sources:`;
`updated: 2026-09-04`.

**16b.** Insert immediately **before** the `## In the KB` heading:

```markdown
## An aphorism on the last mile (2026-08-28)

One line, posted on LinkedIn, and the whole of the post:
*"The value of being 90% done, or even 99% done, has never been lower than in the AI era"*
([[khononov-value-of-90-percent-done-never-lower]]). **86 characters, no argument, no evidence, no
elaboration — a slogan, not a finding**, and it must never be counted as a corroborating voice for
another claim. The plausible last-mile reading (when the first 90% is nearly free, all the value sits in
finishing, hardening and verification) is *the KB's inference, not his words*; for the argued version
cite [[khononov-ai-doesnt-fix-your-real-bottleneck]] instead. Filed as a crisp position on the
[[verification-burden]] strand, and as a **liveness datum**: his own channels have been quiet since
2026-05-01, so LinkedIn is currently where he posts — relevant to `watch-config.json`.
```

Add the new page to the closing `_Source pages:_` line.

---

## 17. `wiki/entities/rick-brewster.md` — **CREATE**

*Why:* he is the subject of a batch source page, quoted at length, and now cited from at least four
concept pages (`verification-burden`, `comprehension-debt`, `software-factory`, `attention-bottleneck`).
A stub keeps those links resolving and keeps the self-report marker attached to his name rather than
only to the source page. Keep it short — the KB has one capture about him and he is not a watch target.

Paste as the whole file:

```markdown
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
```

---

## 18. `wiki/concepts/given-when-then.md` — **UPDATE** (2 edits)

*Why:* the page's strongest existing argument (Adaptech: the test predates the implementer) now has an
**independent arrival from outside the Event-Modeling world** — Tornhill reaches "generate the e2e
tests first, review *those*, let the agent make them pass" from code health, with no EM vocabulary at
all. That is the focus area's best corroboration in this batch.

**18a. Frontmatter.** Append `tornhill-controlling-the-uncertainty-machine` to `sources:`;
`updated: 2026-09-04`.

**18b.** Append at the very end of the
`## First-party: GWT as executable tests before implementation (Adaptech, 2026-08)` section (before the
closing `_Sources:_` line):

```markdown
**Arrived at from outside EM, from the code-health side (Tornhill, 2026-08-20).** The same structure
appears with none of this vocabulary in [[tornhill-controlling-the-uncertainty-machine]]: after
planning, he instructs the agent to *"generate the end-to-end (e2e) tests first,"* reviews and iterates
on **those** with the agent, and only then lets it write the implementation — *"a strong test suite
serves as a boundary between the code I do inspect and the code I give the AI autonomy to develop…
Starting with e2e tests solves the validation problem: how do I ensure that the AI generates the right
code?"* Test-before-implementation, human-reviewed, as the human/agent contract — i.e. what a slice's
given/when/then already is.

Three details sharpen the comparison. He designs the tests *"to optimize for ease of inspection"* and
refactors them toward the domain, adding "abstractions to document the intent" — the same legibility
requirement a GWT scenario satisfies by construction. He reports the quality inversion that EM
practitioners should expect too: AI application code is "usually decent," *"the test code? Not so
much,"* so the human effort is in the test refactoring. And his boundary is *movable* — it follows task
uncertainty ([[autonomy-ladder]]), where a model-derived GWT set is fixed before the work starts.

The difference from the Adaptech position remains the **provenance** condition this page already tracks:
Tornhill's tests are agent-generated and human-reviewed, not derived from a model agreed in the room,
so they inherit whatever the agent misunderstood about intent — the gap
[[bockeler-tdd-inside-the-agent-loop|Böckeler's]] eval warns about, only partly closed by his review
step. Still, an independent practitioner converging on *executable spec before implementation* as the
answer to the [[verification-burden]] is the strongest external support this seam has.
```

---

## 19. `wiki/concepts/multi-agent-orchestration.md` — **UPDATE** (2 edits)

*Why:* the page's ceiling on fan-out is entirely **machine-side** (CEAD: degradation past ~32 agents).
This batch supplies a **human-side** ceiling — and a live disagreement about where it is.

**19a. Frontmatter.** Append
`laycock-the-conductor-developer, tornhill-compressed-cognition-cost-of-faster-coding` to `sources:`;
`updated: 2026-09-04`.

**19b.** Append at the end of the page, before the closing `_Source pages:_` line:

```markdown
## The human-side ceiling on fan-out (2026-07/08) — disputed

CEAD's ~32-agent degradation above is a **machine-side** limit. There is a human-side one, and the KB's
two sources disagree about where it sits.

[[rachel-laycock]] ([[laycock-the-conductor-developer]]) puts it at eight to twelve: *"an engineer…
regularly have eight AI agents running in parallel. I've heard similar numbers from others. Ten. Twelve.
**Beyond that, they become the bottleneck**"* — and frames orchestration at that width as the emerging
shape of the job (the developer as conductor, *"someone has to hold the whole system in their head"*).
[[adam-tornhill]] ([[tornhill-compressed-cognition-cost-of-faster-coding]]) puts it at two:
*"I typically have one long-running agentic maintenance task that I just babysit, and then one focus
task. **Never more**"* — because *"it is the **parallelisation of human attention** that does not
scale."* He explicitly exempts machine parallelism ("yes, I understand sub-agents and machine
parallelisation. That is not what I'm objecting to"), so this is a claim about the *supervisor*, not the
topology.

**Both are anecdote-grade** — her 8/10/12 is hearsay from one unnamed engineer plus "others," his
ceiling of two is a personal rule — and the mechanism he offers (decision density, "3-4 things" in
working memory, self-interruption) is the only one on the table. Held open on
[[attention-bottleneck]]; the consequence for orchestration design is that fan-out has **two**
independent ceilings, and the human one may bind first.
```

---

## 20. `wiki/concepts/spec-driven-development.md` — **UPDATE** (2 edits)

*Why:* the page already carries Dilger's "describing without solving" failure mode and Ng's
"reviewer, not builder" critique. Tune adds the *modelling* version of the same objection from a DDD
voice, and it belongs next to them rather than only on the DDD stub.

**20a. Frontmatter.** Append `tune-no-rapport-with-a-model-you-didnt-code` to `sources:`;
`updated: 2026-09-04`.

**20b.** Insert immediately **before** the `## Open questions` heading:

```markdown
## The modelling version of the same objection (Tune, 2026-08-28)

Dilger's "describing without solving" and Ng's "reviewer, not builder" both say the artifact can exist
without the understanding behind it. [[nick-tune]] states the DDD form
([[tune-no-rapport-with-a-model-you-didnt-code]]): *"discussing and refining a domain model is not the
same as writing the lines of code yourself… **And that means the domain model is going to be worse**
because I'm clearly missing some nuances that could lead to big modelling breakthroughs."* And the
part that bites hardest on spec-first workflows: *"I'm struggling to see how to get the same level of
rapport with the model without actually writing the code. **Maybe it's not even possible.**"*

The premise this challenges is the one SDD needs to be true — that implementation is downstream of
understanding, so it can be delegated once the spec is right. Tune's claim is that implementation was
*generating* understanding, which is the same objection
[[tornhill-ai-readable-code-series|Tornhill's "SDD and the Illusion of Known Scope"]] makes from the
code side ("implementation was never just typing — it's discovery and learning"), now aimed at the
model rather than the scope. It is **thin** (a short LinkedIn post; a quality claim inferred from a
stated feeling, unobservable by construction), and the KB's candidate reply is the one this page's
Event-Modeling material already implies: a spec the human *models* rather than merely *writes* keeps the
thinking on the human's side — [[event-modeling]], [[model-as-code-vs-model-as-language]]. See
[[verification-burden]] and [[comprehension-debt]].
```

---

## 21. `wiki/index.md` · `wiki/log.md` · `wiki/overview.md` — **UPDATE** (orchestrator-owned; paste-ready)

**21a. `wiki/index.md` — 13 source lines + 2 concept lines + 1 entity line.**

Sources:

```markdown
- [[willison-brewster-cannot-review-180000-lines]] — Paint.NET's maintainer on 180k agent-written lines: "I cannot possibly review 180,000 lines of code" (self-report).
- [[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]] — don't automate review; move what review is *for* earlier and review by exception (Thoughtworks CTO; not independent).
- [[tornhill-controlling-the-uncertainty-machine]] — attention follows task uncertainty; e2e tests as the human/agent boundary, deterministic enforcement for the rest (vendor self-report on the remedy).
- [[tornhill-compressed-cognition-cost-of-faster-coding]] — agentic coding compresses the decision timeline; relays an *unnamed* trial where devs estimated +20% and were 19% slower.
- [[tune-no-rapport-with-a-model-you-didnt-code]] — you cannot get rapport with a domain model you didn't write; "maybe it's not even possible."
- [[willison-more-than-just-code-review]] — instruct confidently, verify confidently; "eyeballing every line has never been the most effective way to validate a change."
- [[willison-conceptual-integrity-and-counting-lines-of-code]] — cognitive capacity as the new limiting factor; conceptual integrity erodes when features get cheap.
- [[laycock-the-conductor-developer]] — "human attention is now the bottleneck"; the developer as conductor, and energy management as the missing curriculum.
- [[osmani-agentic-code-review-skill-five-axes]] — an agentic review skill on five axes, severity-labelled and leverage-ordered (author's own tool, no evaluation).
- [[tornhill-task-uncertainty-decides-what-code-you-read]] — "I never read all AI-generated code. But… make the code you do read count."
- [[tornhill-ai-induced-code-smells-codehealth-mcp]] — CodeHealth MCP product post; smells "I never need to see" (vendor self-report; **contains no figures**).
- [[tornhill-beyond-lambdas-raising-the-abstraction-level]] — name the lambdas after the domain; "anonymous functions are anonymous thoughts."
- [[khononov-value-of-90-percent-done-never-lower]] — one-line aphorism on the last mile (86 characters; a slogan, not a finding).
```

Concepts:

```markdown
- [[verification-burden]] — who reads agent-written code and what replaces reading: a live five-way dispute (Brewster / Laycock / Tornhill / Osmani / Willison), plus Tune's dissent that the loss is upstream.
- [[attention-bottleneck]] — attention as the scarce input: the mechanism (decision density, self-interruption) and three unresolved remedies (widen / distribute / narrow the span).
```

Entities:

```markdown
- [[rick-brewster]] — Paint.NET's author; the KB's bluntest primary on unreviewable agent output (self-report).
```

**21b. `wiki/log.md` — append:**

```markdown
## [2026-09-04] ingest   | Batch D "the verification burden" (13 captures: Laycock ×2, Tornhill ×5, Willison ×3, Tune, Osmani, Khononov) — touched: 13 new source pages + 2 new concepts (`verification-burden`, `attention-bottleneck`) + 1 new entity (`rick-brewster`) + 15 page updates. Work order: `outputs/ingest-deltas/batch-d-verification.md`. **Holds a live five-way dispute on whether code review scales — presented, not resolved.** Numbers refused: the 20%-felt / 19%-measured trial is **unnamed by Tornhill** (never write "Tornhill cites METR"); Meta +106% LOC-per-diff and DX median PR size +64% reach Laycock via Houck at **DX, a productivity-measurement vendor** (the 106% double-relayed and hedged "reportedly"); Laycock's "ten times the code" is rhetorical and her 8/10/12 parallel agents is hearsay; Brewster's 180k/700k/20yr are his own forum-post counts; Willison's lines-per-day figures are rules of thumb; the CodeHealth MCP post **carries no figures at all** (they are in an unread screenshot); Khononov's post is an 86-character slogan.
```

**21c. `wiki/overview.md` — the synthesis shift, if the orchestrator agrees it lands.** Two sentences,
placed wherever the loop/verification thread is discussed:

```markdown
**The verification burden is now the thread's open dispute (2026-09).** Comprehension debt has stopped
being a warning and become an argument about instruments: within one quarter, five practitioners
published incompatible answers to "who reads agent-written code" — accept the debt
([[willison-brewster-cannot-review-180000-lines|Brewster]]), relocate review's functions earlier and
review by exception ([[laycock-maybe-we-shouldnt-be-reviewing-all-this-code|Laycock]]), triage by task
uncertainty behind a test boundary ([[tornhill-controlling-the-uncertainty-machine|Tornhill]]), automate
the gate ([[osmani-agentic-code-review-skill-five-axes|Osmani]]), or distribute the reading across a
team ([[willison-conceptual-integrity-and-counting-lines-of-code|Willison]]) — with
[[tune-no-rapport-with-a-model-you-didnt-code|Tune]] arguing the loss was never in review at all. The
KB holds this on [[verification-burden]] as a live dispute; nobody has measured the one quantity that
would settle it (how often reading the code catches what the other instruments miss). Its resource
ceiling is on [[attention-bottleneck]], and the seam to this KB's focus area is that every "other way
to verify" turns out to be an **executable specification agreed before the code exists** — which is
what [[event-modeling]] has been producing all along.
```

---

## Noted, but not proposed as edits

- **`wiki/entities/thoughtworks.md`** — this batch adds **two more** martinfowler.com-published Laycock
  pieces, so the concentration problem that page documents is now materially worse: three of the KB's
  named positions on review, attention and governance come from one company's channel and its CTO. A
  one-line update there is warranted, but the page's own framing should decide the wording — flagging
  rather than drafting.
- **Missing side of the dispute.** Brian Houck's *"What are code reviews even for?"*
  (newsletter.getdx.com) is **not in `raw/`**, and the KB now holds Laycock's characterisation of it
  only. It is the highest-value capture to fetch next on this thread — and note DX is an interested
  party (they sell developer-productivity measurement), which is exactly why their argument for review's
  non-bug functions should be read first-hand.
- **Also worth capturing:** the *Talking Postgres* episode Willison quotes from (only two excerpts are
  in `raw/`), and Osmani's `addyosmani/agent-skills` review skill itself (the post describes it; the
  prompt content is the actual artifact).
- **`conceptual-integrity`** is a page-shaped idea with **one** source (Willison/Brooks). Filed as a
  section on `comprehension-debt` (item 3c) with an explicit promote-on-second-source note; do not
  create it yet.
- **The two Tornhill uncertainty pages** (`...controlling-the-uncertainty-machine` and
  `...task-uncertainty-decides-what-code-you-read`) are one argument split across two captures per the
  one-page-per-capture rule. **They must never be cited side by side as corroboration.**
- **The intervention rate** — how often reading agent-written code catches something the other
  instruments miss, and at what severity — is the quantity nobody in this batch reports and the one that
  would settle the dispute. Worth standing as an open question in `overview.md`.
