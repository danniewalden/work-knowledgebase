---
title: Software Factory
type: concept
created: 2026-07-27
updated: 2026-09-04
sources: [dilger-lights-off-software-factory-dead-end, dilger-trust-needs-to-be-engineered, addyosmani-software-factories-light-and-dark, stripe-minions-one-shot-coding-agents, fowler-agentic-programming, prefect-loops-vs-graphs, jwilger-agent-skills-factory-pipeline, addyosmani-human-judgment-relocates, macmanus-prs-not-welcome-software-factories, addyosmani-agentic-code-quality, miracle-my-loop-engineering-workflow, voss-what-the-hell-is-a-loop-anyway, willison-brewster-cannot-review-180000-lines]
tags: [loop-engineering, software-factory, harness-engineering, comprehension-debt, focus]
---

# Software Factory

**The top rung of the loop → harness → factory stack.** A software factory is **many harnessed
[[loop-engineering|loops]] running at once, fed by a queue of work and drained through a review gate into
production, with humans owning it from above** ([[addyosmani-software-factories-light-and-dark|Osmani]]).
"The loop is the atom; the factory is the loop at scale" — and crucially it is **"not a bigger agent; it is
an org chart made of loops."** The paradigm shift is from writing code to **building and running the factory
that writes it** — the unit of work moves up from the diff to the loop, the [[agent-harness|harness]], and
the flow between them. (The dream is old — Bob Bemer's 1968 "economics of program production" — and mostly
failed on "the difficulty of stamping out ideas"; the last two years made it worth a fresh look.)

## The wiring diagram

Intent (leadership + engineers) and signals (incidents, user requests) feed a **queue** → the harness picks
an item and builds a change → **automated checks** (CI, tests, static analysis, scanning) → the **review
gate** → deploy → monitoring feeds back into signals. Every box is near-zero-cost **except the review gate** —
the "judgment" box that stubbornly resists scaling. That gate is the whole argument.

## Do you actually need a factory yet? ([[addyosmani-human-judgment-relocates|Osmani, 2026-08-21]])

The prior question this page never asks. *"**In my experience, you can get surprisingly far with your
stock coding harness!**"* — Claude Code or Codex, multiple sessions, good SPECs with verification baked
in, constraints, *"you can even throw a batch of GitHub issues at them with implementation and
human-involvement criteria."* And the blunt version: *"You may be fine. Your work may actually be totally
fine without needing a factory."*

**The threshold:** *"Add a software factory when you need an **event-driven queue of work** (e.g. Slack
triggers, GitHub issues, Linear, a backlog) to run in an **isolated cloud environment** to handle triage,
implementation and testing with some explicit human babysitting."* I.e. the trigger is **repeatability +
event-driven-ness**, not scale or ambition.

**And what it actually buys, which is unglamorous:** *"The factory becomes useful when the hard part is
making your different runs behave consistently, handing work off between agents and **avoiding different
sessions from claiming the same issue**, preserving evidence and **stopping production when human review
is falling behind**."* Note the last clause: **throttling itself against reviewer capacity is part of the
factory's job**, not an external control.

**The factory's real interface is a mutable label on a work item.** Warp triages every incoming issue
into **ready-to-implement / ready-to-spec / needs-info / wait-to-implement**, *"and the label is what
fires the next agent."* Osmani: *"This label does a few jobs in one go: **it's the queue, the lock** and
since a session only picks up what's marked ready, it's **where a human can park stuff without saying no
permanently**."* Queue, mutual exclusion and deferral in one field — and
[[macmanus-prs-not-welcome-software-factories|Astro's and Flue's]] PR-to-issue conversion is that parking
spot made mandatory.

**Four ways a human participates**, beyond approving a final diff: **shape** (early), **steer**
(mid-implementation redirect), **handoff** (move task + state + context between cloud factory, another
agent, or a human reviewer — *"Good handoffs will keep track of what happened, whats left to be done and
why the handoff is needed"*), **approve/stop**. Plus **notifications** as *"how the factory says it's
blocked."*

Building is not the only option: *"Standing up the infra to scale a factory can be a lot of work and you
may want to consider buying vs. building"* — Factory, Warp and HumanLayer are named.

*(Practitioner essay; no measurement. The **82-minute factory run** and its per-task timings — 7 minutes
for one feature, 56 for another — are **IMPRESSION NOT MEASUREMENT**, one unoptimized run of a movies demo
app by the reference repo's own author. All Vercel and Warp figures are **VENDOR SELF-REPORT**, cited
second-hand.)*

## Light vs dark

- **Dark factory:** code ships that **no human has read**, verified only by machines (the lights-out
  manufacturing image — FANUC/Xiaomi; "in software, the floor is the diff"). Easy at first — removing review
  makes throughput feel like breaking the sound barrier — but it doesn't pay down
  [[comprehension-debt|comprehension debt]], it "takes it on as fast as it can, with the tests green the
  whole way." The reckoning is "quiet and late." [[dex-horthy|Dex Horthy]] ran one ~4 months (no human
  reading the code) and needed painstaking manual debugging to recover.
- **Lit factory:** the *same* pipeline "with the lights left on where judgment lives" — agents build, but a
  human reads what ships **and** the point of judgment moves **upstream** to product/design/architecture
  (review a 200-line plan, not 2,000 lines after the fact). The safety net is ordinary architecture doing a
  second job (types, test seams, legible layout, short call stacks, small blast radius, DI) — and it must
  live **outside the model**, because capable coding agents are RL-trained for tool fluency, not long-term
  maintainability.

## Back pressure — the governing rule

**"You can only hand a loop as much autonomy as you can cheaply and reliably verify, and not one inch more.
Verification, not generation, is the real constraint."** Generation is a wide mouth, verification the narrow
neck; speeding the mouth just deepens the pile at the neck. **What earns a loop the dark:** a check that's
cheap, high-frequency, and hard to fake (green/red oracle, type gates, property tests, review-agent + rubric),
immediate and non-drifting; short loops (Horthy: an agent holds 3–10 steps, loses the thread past ~20). Keep
the lights on where a wrong answer is expensive and only a person can catch it. "The hard, skilled job is
deciding where to put each switch" — all-dark self-destructs in months, all-lit is a review bottleneck.

The formal underpinning arrived from [[miracle-my-loop-engineering-workflow|Miracle (2026-08-10)]]:
*"**Generation parallelized; verification did not.** So generation ≈ max(task time), but delivery ≈
generation + verification. Fork-join doesn't eliminate the serial work. It concentrates it at the join."*
Back pressure is Amdahl's law with the serial fraction sitting in the review gate. *(Practitioner
self-report; nothing measured.)*

## Classifying runs — and the two things classification misses ([[addyosmani-human-judgment-relocates|Osmani, 2026-08]])

Vercel marks every agent run **success / flawed / blocked / manual**, and *"only 'success' ships to
production. The rest re-enter the system."* Osmani's reading: **flawed** = wrong thing implemented, or it
lacked context; **blocked** = the environment was missing a credential; **manual** = *"a boundary the
factory may not be allowed to cross it yet."* *"Two of the three things here may have mechanical fixes and
**the last one is about trust**."* *(**VENDOR SELF-REPORT** — Vercel's own scheme for its own factory,
cited second-hand.)*

**Gap 1 — the taxonomy has no cost term.** *"While this is great, what sorting doesn't show you is cost…
So I'd **pair the taxonomy with per-stage timing**, otherwise you know a run came back flawed without
knowing what finding out cost you."* This is the measurable form of his own **"number of checks !=
quality"** rule, and the missing metric behind
[[dilger-real-cost-of-ai-is-second-order|Dilger's second-order cost]]. He also proposes **cost per merged
PR** and **code shelf life** as [[comprehension-debt]] metrics (proposals, not results).

**Gap 2 — a blocked run has no named re-entry point, and this is a design defect nobody else raises.**
*"My sample factory stopped [at] the first issue and moved it to `factory:needs-info`, which was right,
**but I didn't know where to put my answer**. **A manual run isn't finished when the factory stops but
when the human knows what to do next.**"* Not a verification problem and not an autonomy problem — an
**interface** problem. It is the same requirement
[[wong-graph-engineering-wiring-agents-into-an-organization|Wong]] states as *"make failure an explicit
edge"* and *"turn human approval steps into real graph nodes with defined edges in and out, not a
side-channel Slack message."*

**And a security requirement specific to factories: the queue is untrusted input.** *"If your factory
reads untrusted input like a GitHub issue/Slack message it might be adversarial and include problems like
supply chain attacks."* Vercel's mitigation is per-task least privilege — *"run their agents in isolated
sandboxes holding just the secrets a task needs. That way a compromised run can't reach what the job
doesn't need"* — the same shape as QM's per-project credential scoping in
[[breunig-harnesses-are-situated-agents]] and [[prefect-loops-vs-graphs|Lowin's]] per-node tool grants.
See [[prompt-injection]].

## Provenance-based trust — a third acceptance mechanism ([[macmanus-prs-not-welcome-software-factories|MacManus, 2026-09-01]])

Four AI-native open source projects — **Vercel's AI SDK, Astro, Flue, tldraw** — are replacing drive-by
community PRs with maintainer-owned factories; **Flue and tldraw automatically close every external PR**
and convert it to an issue or discussion. The interesting claim is **why**, and it is not code quality.

Vercel engineer Lars Grammel: *"If we have a very specific agent with a very specific prompt that we
optimized — and we know that, over history, it was very successful in fixing a certain category of bugs —
then **we develop trust in that particular agent configuration**… For open-source projects, it's worth
considering having your own agents and your own setup, and **not necessarily trusting the community**,
because it can actually cut down your time to review."*

**That is the maker-checker argument reframed as a PROVENANCE argument, and it is a mechanism the KB has
not named.** The KB's acceptance vocabulary has two moves — *check the artifact* (tests, sensors, gates)
and *use a different checker than the maker*. This is a third: **accept a change because of what produced
it**, on the strength of a per-bug-category track record. It is the logic of a signed build or a trusted
CI runner, applied to an agent configuration. Steve Ruiz (tldraw) states the condition it rests on:
*"It just makes less sense to have people contributing code **if the issue is decently well-specified and
the code can be written by agents**"* — so the mechanism is parasitic on
[[spec-driven-development|spec quality]]. [[mitchell-hashimoto|Hashimoto]] pushes it further: *"the future
is that large open source projects will close contributions completely."*

**The failure mode nobody in the piece raises:** a configuration's track record is **retrospective**, and
the thing being trusted is a prompt that can be edited. Provenance trust with no versioning of the
configuration, and no re-validation after an edit, is trust in a moving target. Note also that tldraw's
stated drivers are broader than agent quality — *"changes in how we're coding (more discussion, more
agents), **the social practices around public contribution**, and **the changing landscape around code
security**"* — only one of the three is about agents being good.

**The cost, conceded by a participant.** PRs were how maintainers were grown: *"pull requests have been
reviewed by maintainers not only for the code, **but to teach contributors and assess them as future
maintainers**."* Fred Schott: *"It still leaves this open hole of, well, if you just keep narrowing the
project, at a certain point, you and I go on vacation — what happens?"* The partial answer both projects
offer is that issues and discussions stay open, so trust-building moves to conversation — Ruiz: *"it's
better to limit community contribution to the places it still matters: **reporting, discussion,
perspective, and care**."* See [[comprehension-debt]] for this as the institutional level of the
skill-decay problem.

*(**VENDOR SELF-REPORT, four weeks in, unaudited:** Vercel's claim that the factory *"authors between 25
and 35% of PRs we merge and closes 70-80% of issues."* **IMPRESSION NOT MEASUREMENT:** Schott's *"totally
shifted in the last six months"* and *"never seen that in my entire decade-plus."* Journalism about four
self-selected, commercially backed projects; no comparison case, no contributor-count data.)*

## Loops vs graphs

"Owning your control flow is really just walking the graph back around the loop" — a predefined directed
graph (nodes = steps, edges = conditions) is **back pressure drawn as a diagram**: trade agent freedom for
mandatory checks and legible failure points. The "throw the diagram away, let the model pick the path
tool-call by tool-call" move "felt like liberation right up until it met a ten-year-old codebase." Seen in
LangGraph, LlamaIndex Workflows, David Khourshid's "state machines in new clothes"; adjacent to
[[nick-tune-graphs-memory-skills-agents|Nick Tune's graph substrate]].

This is the same move [[jeremiah-lowin|Lowin]]/[[prefect|Prefect]] ([[prefect-loops-vs-graphs]]) name as
**[[graph-engineering|directed agentic graphs]]** — macro orchestration across many agents, one node per
full agentic invocation, control returning to the orchestrator at each edge. A factory's "org chart made
of loops" *is* such a graph; Osmani's back-pressure and Lowin's node-level capability scoping ("don't
hand your agent a bazooka") are the same governing instinct drawn at different altitudes. See
[[graph-engineering]] for the full treatment.

**A dissent about where the factory sits at all:** [[voss-what-the-hell-is-a-loop-anyway|Voss]] classifies
the software factory **as** a loop — his *product loop*, iterating on a codebase-plus-backlog — against
this page's placement of it as the rung *above* loops. Recorded, not resolved.

## Relationship to neighbours

- **[[loop-engineering]]:** the factory is loop engineering's largest unit; back-pressure and the
  inner/outer-loop split ([[addyosmani-own-the-outer-loop]]) are its governing rules.
- **[[harness-engineering]]:** "harness engineering is not enough" ([[dex-horthy|Horthy]]) — a good harness
  makes one loop reliable but doesn't decide *which* loops earn autonomy; that's the factory-level judgment.
- **[[unattended-coding-agents]] / [[stripe-minions-one-shot-coding-agents]]:** Stripe's minions (*Stripe's own figure*, 1,000+
  merged PRs/week behind deterministic shift-left gates) are a lit-leaning factory in production.
- **[[ahe-agentic-harness-engineering]] / [[harness-evolution]]:** the measured cousin — an agent evolving
  the harness inside the factory's improvement loop. *(Its headline gain is **contested** — see
  [[harness-evolution]].)*
- **vs. [[event-modeled-agent-design]]:** the EM seam is now partly *worked* —
  [[john-wilger|Wilger's]] factory pipeline ([[jwilger-agent-skills-factory-pipeline]]) is a
  software factory whose **work-items are event-model slices and whose review-gate oracle is each
  slice's [[given-when-then|GWT]]** (rejected unless it hits an external boundary), with the event model
  as the upstream human-authored spec driving the whole line ([[dilger-event-modeling-agent-harness]] is
  the harness-side counterpart).

## The named dissent — "the lights-off factory is a dead end" (Dilger, 2026-08-16)

The dark-factory section above had no practitioner arguing against it by name. It has one now, and from
someone otherwise maximally bullish on agentic engineering
([[dilger-lights-off-software-factory-dead-end]]):

> "Every single team I know who went down that route circled back. I don't practice it either, even
> though I'm all in on agentic engineering."

His failure mode is specifically an **incident** failure mode — "production burning and no one there to
navigate the code base ( as no one has ever seen it )" — i.e. [[comprehension-debt]] coming due at the
worst moment. And he states the bind this page circles: *"you can't do full code reviews - it'll not be
sustainable with the increased output - you just moved the bottleneck. But you can't do no code-reviews
either."*

His answer is **layers of trust** rather than more review: model-as-spec with GWT guard rails →
executable specs written before any code → static gates with defined consequences (*files changed outside
the Slice Under Development = immediate fail*) → a **2–3 minute structural** review that is explicitly
not functional, "at this point we already know it works." Failures are disposed of, not repaired — the
slice goes back to "planned" and a learning is recorded.

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

Two things this contributes that the page lacked:

- **The reason to keep a human in the loop is comprehension, not correctness.** "I keep connected to the
  code base… If something goes wrong, I roughly know where to look." That is a different justification
  from back-pressure, and a stronger one against the dark factory.
- **A stated asymmetry about what is reversible.** He does not much care how a slice is implemented
  internally — "any bad implementation can be easily replaced" — but cares a great deal about system
  structure and *the shape of the persisted events*. Compare the reversibility axis on
  [[autonomy-ladder]]: the irreversible decision here is the event schema.

The paired post two days earlier ([[dilger-trust-needs-to-be-engineered]]) gives the general form:
constrain what the agent may decide, and there is less to verify — *"not by doing more reviews, but by
making most of them obsolete."*

*Caveat: "every single team I know" is unattributed hearsay, and the pipeline described is the one his
own platform supports.*

_Sources: [[addyosmani-software-factories-light-and-dark]] · [[stripe-minions-one-shot-coding-agents]] · [[fowler-agentic-programming]] · [[prefect-loops-vs-graphs]] · [[jwilger-agent-skills-factory-pipeline]] · [[addyosmani-human-judgment-relocates]] · [[macmanus-prs-not-welcome-software-factories]] · [[addyosmani-agentic-code-quality]] · [[miracle-my-loop-engineering-workflow]] · [[voss-what-the-hell-is-a-loop-anyway]] · [[willison-brewster-cannot-review-180000-lines]]._
