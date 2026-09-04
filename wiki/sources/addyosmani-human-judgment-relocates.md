---
title: "Source: Osmani — Human Judgment Doesn't Leave the Software Factory. It Relocates."
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [addyosmani-human-judgment-relocates]
raw_file: [raw/articles/addyosmani-human-judgment-relocates.md]
tags: [software-factory, loop-engineering, comprehension-debt, verification, autonomy-ladder, focus]
---

# Source: Osmani — Human Judgment Doesn't Leave the Software Factory. It Relocates.

Source: [[addy-osmani]], *"Human judgment doesn't leave the software factory. It relocates."*,
addyosmani.com (originally his Substack), **2026-08-21**. Raw capture:
`raw/articles/addyosmani-human-judgment-relocates.md`. The [[software-factory]] counterpart to
[[addyosmani-practical-loop-engineering]] and the governance sequel to
[[addyosmani-software-factories-light-and-dark]].

## Summary

*"A software factory is a repeatable loop around software work."* The thesis is in the title: the share
of code humans type may collapse, **but ownership does not** — *"human judgment is being relocated,"*
upstream to intent/system shape/quality bar and downstream to evidence/risk/ownership. The best
factories *"will not be defined by how completely they eliminate human involvement. They will be defined
by how intelligently they **place** it."* The piece is also the only source in the KB that asks the
prior question — **do you actually need a factory yet?** — and answers "probably not."

## Key points

- **The "do you need one" test — the prior question the KB's [[software-factory]] page did not ask
  before this source.** *"In my
  experience, you can get surprisingly far with your stock coding harness!"* — Claude Code or Codex,
  multiple sessions, good SPECs with verification baked in, constraints, even a batch of GitHub issues
  with implementation and human-involvement criteria. **A factory earns its keep only when the work needs
  to be *repeatable and event-driven***: *"Add a software factory when you need an event-driven queue of
  work (e.g. Slack triggers, GitHub issues, Linear, a backlog) to run in an isolated cloud environment to
  handle triage, implementation and testing with some explicit human babysitting."*
- **What the factory actually solves, and it is unglamorous.** *"The factory becomes useful when the hard
  part is making your different runs behave consistently, handing work off between agents and **avoiding
  different sessions from claiming the same issue**, preserving evidence and **stopping production when
  human review is falling behind**."* Note the last one: the factory's job includes throttling itself
  against reviewer capacity.
- **The triage label as queue, lock and parking spot.** Warp triages every incoming issue into one of
  four states — **ready-to-implement, ready-to-spec, needs-info, wait-to-implement** — *"and the label is
  what fires the next agent."* Osmani's read: *"This label does a few jobs in one go: it's the queue, the
  lock and since a session only picks up what's marked ready, it's **where a human can park stuff without
  saying no permanently**."* A single mutable field doing coordination, mutual exclusion and deferral.
- **The four human participation modes.** Beyond approving a final diff: **shape** (early), **steer**
  (mid-implementation course correction), **handoff** (move the task, its state and context between
  cloud factory / another agent / human reviewer — *"Good handoffs will keep track of what happened,
  whats left to be done and why the handoff is needed"*), **approve** (stop it shipping). Plus
  **notifications** as *"how the factory says it's blocked."*
- **"Number of checks != quality."** *"You'll likely need to experiment with what checks give you the
  best signal to noise ratio. Be ready to tighten or relax your constraints deliberately."* And from the
  demo: *"a factory that just runs a lot of checks that you're not finding valuable does not mean it's a
  high quality one. You want to study how, for any repeated checks, are they irrelevant? Are they noisy?
  Are they actually making the system safer?"*
- **A verification budget, modelled on a performance budget.** Fast deterministic checks (lint, type
  checking) early; heavy-but-valuable checks (full suite, **mutation testing**, browser testing, security
  scans) at or after the draft-PR gate. *"You don't necessarily want to replace these with just
  summaries. You want real tests."*
- **When green is misleading.** *"When you have asked AI to help you pass a test… it can change the unit
  test to satisfy that condition, or it can change the logic of the code to pass that condition. That
  doesn't mean that it's actually followed your intent."* His illustration is a **silent scope
  substitution**: asked to add GitHub as an auth provider, *"my UI only had space for three, so I've gone
  and I've dropped one of the other ones. And hey, by the way, that happened to be one that your
  customers actually wanted."* **"Just because a software factory is showing that everything is green
  doesn't mean that it's actually green."**
- **Run classification, from Vercel's factory** — every agent run is marked **success / flawed / blocked
  / manual**, and *"only 'success' ships to production. The rest re-enter the system."* Osmani's gloss:
  flawed = wrong thing implemented or missing context; blocked = environment lacked a credential; manual
  = a boundary the factory *"may not be allowed to cross it yet."* *"Two of the three things here may have
  mechanical fixes and the last one is about trust."* **His critique of the taxonomy is the useful part:**
  *"what sorting doesn't show you is cost… So I'd pair the taxonomy with **per-stage timing**, otherwise
  you know a run came back flawed without knowing what finding out cost you."*
- **The handoff boundary is where his own sample factory failed.** *"My sample factory stopped [at] the
  first issue and moved it to `factory:needs-info`, which was right, **but I didn't know where to put my
  answer**. A manual run isn't finished when the factory stops but when the human knows what to do
  next."* A genuinely new requirement: the blocked state must name its own resolution channel.
- **Cognitive bandwidth doesn't scale with the agents.** Five or ten parallel sessions *"create much more
  than just a review volume problem. They create **several mental models that can end up going pretty
  cold** while you're working elsewhere."* His fix is on-disk: *"consider asking your agent to actually
  store information about its trajectory, or interesting lessons about how it approached a problem so
  that you can go back to it later"* — because *"Code often preserves a decision that was made, but not
  why the decision was made."*
- **Two first-person failures, both about understanding rather than correctness.** (1) **The
  wrong-project prompt**: he typed a dark-mode prompt into the session for a different project and
  *"began implementing dark mode for something that absolutely didn't need it. And so I can make that
  mistake. **I don't want my software factory making that kind of mistake.**"* (2) **The feature he had
  to relearn**: tests passed, he merged a favouriting feature, returned days later to tweak it and
  *"couldn't explain to you how the feature worked. This repository was mine, right? I'd approved the
  change… **my understanding hadn't kept up pace with all of the code that had been building up.**"* He
  had to redo it step by step. This is [[comprehension-debt]] in the first person, from someone who
  approved the change.
- **Security is a factory concern because the queue is untrusted input.** *"If your factory reads
  untrusted input like a GitHub issue/Slack message it might be adversarial and include problems like
  supply chain attacks."* Vercel's mitigation: *"run their agents in isolated sandboxes holding just the
  secrets a task needs. That way a compromised run can't reach what the job doesn't need."*
- **"Which old projects deserve another life?"** The judgment question that survives automation. Now
  trivial to finish abandoned side projects — *"but the same human judgment question comes in. Do those
  projects deserve to exist? Should they be launched? Because you put them out into the world and even if
  it has just five users, maybe you have to maintain it."*
- **Ownership doesn't disappear — five things that stay human.** *"Someone still chooses the problem…
  chooses the architecture… sets the quality bar… decides which verification signals deserve trust…
  decides when the evidence is sufficient to ship. And when the resulting system fails, **'the agent
  wrote it' doesn't cut it.**"*
- **Limits.** A practitioner essay: **no measurement, one demo.** The **82-minute factory run** and its
  per-task times (*"the quick finder with no rejections took 7 minutes. Favorites, with two rejections and
  a human decision in the middle, took 56. Same factory"*), and the claim that tasks *"can take two to
  four times as long once you begin to include verification, retries, browser checks, human review"* are
  **IMPRESSION NOT MEASUREMENT** — a single unoptimized run of a movies demo app by the author of the
  reference repo (*"I didn't really spend any time optimizing it"*). Suggested metrics (**cost per merged
  PR**, **code shelf life**) are proposals, not results. Every number attributed to **Vercel** and
  **Warp** is that company's own account of its own factory — **VENDOR SELF-REPORT**, cited second-hand.
  Osmani is a Director at Google Cloud AI writing about the tooling he promotes, and this piece links
  three of his own prior posts as support.

## Connections / contrast

**The delta to [[software-factory]] is the "not yet" test, and it should go near the top of that page.**
The KB's factory page describes the wiring diagram, light-vs-dark, and back-pressure; the threshold for
entering one at all comes from here. Osmani supplies it — **repeatable
+ event-driven + queue + isolation** — plus a buy-vs-build note (Factory, Warp, HumanLayer) and the blunt
prior: *"You may be fine. Your work may actually be totally fine without needing a factory."* That is the
same shape of caution [[dilger-lights-off-software-factory-dead-end|Dilger's named dissent]] gives from
the other side, and it makes the page less of an escalator.

**"Human judgment relocates" is the KB's clearest reconciliation of two positions it holds in tension.**
[[voss-what-the-hell-is-a-loop-anyway|Voss]] frames the AIEWF argument as turn-the-dial-up (Lloyd,
Gavrilescu) versus the-dial-has-a-stop (Litt, Bakaus). Osmani's answer is neither: **the dial is
per-place, not global** — remove people *"from the parts of the loop where machines can produce stronger,
faster, more deterministic signals"* and concentrate them *"around the places where context, taste, risk,
and long-term ownership matter most."* That is [[addyosmani-own-the-outer-loop|his own outer-loop]]
argument made spatial, and it is compatible with [[morris-humans-and-agents-in-software-engineering-loops|Morris's
"on the loop"]] — with the difference that Morris relocates humans to the **harness**, Osmani to
**intent and evidence**.

**"When green is misleading" is the most-cited failure in this batch and now has three independent
statements.** Osmani's assertion-rewriting; [[miracle-my-loop-engineering-workflow|Miracle's]]
goal-backward verifier, invented specifically to catch *"any requirement without evidence… even if all
the tests pass"*; and [[bockeler-tdd-inside-the-agent-loop|Böckeler's]] "a red test tells you the agent
ran it and saw failure, not that the failure was for the right reason." The KB can state this as a
convergent finding — while noting that **only Böckeler ran an experiment.**

**The blocked-state gap is a genuinely new requirement for [[agent-legibility]]/[[agent-governance]].**
*"A manual run isn't finished when the factory stops but when the human knows what to do next"* is not a
verification problem or an autonomy problem — it is an **interface** problem, and no other KB source
raises it. Pair it with [[wong-graph-engineering-wiring-agents-into-an-organization|Wong's]] "make
failure an explicit edge" and "turn human approval into real graph nodes, not a side-channel Slack
message": both are saying the human's re-entry point must be part of the design.

**The per-stage-timing critique of run classification** extends [[feedforward-and-feedback-controls]]:
sensors that classify outcomes without costing them cannot tell you whether the sensor is worth its
latency. That is the measurable form of *"number of checks != quality,"* and it is the missing metric
behind [[dilger-real-cost-of-ai-is-second-order|Dilger's second-order cost]] thread.

## Links

[[software-factory]] · [[loop-engineering]] · [[comprehension-debt]] · [[unattended-coding-agents]] ·
[[autonomy-ladder]] · [[harness-engineering]] · [[feedforward-and-feedback-controls]] ·
[[mutation-testing]] · [[fitness-functions]] · [[agent-governance]] · [[agent-legibility]] ·
[[prompt-injection]] · [[decision-trace]] · [[adr]] · [[spec-driven-development]] · [[addy-osmani]] ·
[[addyosmani-software-factories-light-and-dark]] · [[addyosmani-own-the-outer-loop]] ·
[[addyosmani-earning-taste-and-judgment]] · [[addyosmani-practical-loop-engineering]] ·
[[addyosmani-agentic-code-quality]] · [[addyosmani-code-agent-orchestra]] ·
[[dilger-lights-off-software-factory-dead-end]] · [[dilger-real-cost-of-ai-is-second-order]] ·
[[voss-what-the-hell-is-a-loop-anyway]] ·
[[morris-humans-and-agents-in-software-engineering-loops]] ·
[[miracle-my-loop-engineering-workflow]] · [[bockeler-tdd-inside-the-agent-loop]] ·
[[macmanus-prs-not-welcome-software-factories]] ·
[[wong-graph-engineering-wiring-agents-into-an-organization]]

_Source: [[addyosmani-human-judgment-relocates]] (raw: `raw/articles/addyosmani-human-judgment-relocates.md`)._
