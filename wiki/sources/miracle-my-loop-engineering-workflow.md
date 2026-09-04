---
title: "Source: Miracle — My Loop Engineering Workflow"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [miracle-my-loop-engineering-workflow]
raw_file: [raw/articles/miracle-my-loop-engineering-workflow.md]
tags: [loop-engineering, harness-engineering, autonomy-ladder, trust, multi-agent-orchestration, focus]
---

# Source: Miracle — My Loop Engineering Workflow

Source: **Andrew Miracle** (Head of Product & Research, Tecmie), *"My Loop Engineering Workflow"*,
andrewmiracle.com, **2026-08-10**. Raw capture: `raw/articles/miracle-my-loop-engineering-workflow.md`.
Harness repo referenced throughout: `github.com/koolamusic/claudefiles`. The most **fully specified
single-practitioner rig** in the KB — and the only one with a quantified trust mechanism.

## Summary

*"I don't have a prompt. I have a triangle of loops."* Three nested loops on three time scales
(**session**/hours, **sprint**/days, **program**/weeks), all running **one grammar** —
*objective → execution → feedback → refined objective* — with **one start point** (a written
commission, never a chat message) and **one end point** (ship only what passes verification, then a
retro). Execution is **fork-join**; the join is a **gate, not a barrier** ("The join doesn't merge
output. It merges confidence"). Privilege is metered by a **trust ledger** scored on every tool call.
*"The prompt is maybe five percent of the outcome. The loops are the rest."*

## Key points

- **Why a triangle, not a stack.** Sessions nest in sprints nest in programs, but **every loop at every
  scale runs the same grammar with the same start and the same end.** The refinement step is what makes
  it converge: *"the retro's output is a refined objective, the next commission sharpened by what the
  feedback taught. That refinement step is why the loop converges instead of spinning."* And the
  criterion: **"Feedback that doesn't refine the next objective is just logging. The end point of one
  loop is the start point of the next. That is what makes it a loop and not a pipeline."**
- **The harness is a place, not a prompt.** `~/.claude` is a versioned repo with an auto-updating plugin
  marketplace, zipped and cloned alongside dotfiles on server migration — *"the agent kit has to be
  portable or it isn't real. Claude, Cursor, Kimi: the models swap, the harness stays."* `CLAUDE.md` is
  "an operating contract": **phased execution** (never a multi-file refactor in one pass), **forced
  verification** (forbidden to report complete before running the project's real checks — and if no
  checker is configured it **must say so instead of claiming success**), and **failure recovery** (if a
  fix fails twice, stop, re-read the section, find where the mental model was wrong, propose something
  fundamentally different — **no third attempt at the same idea**). ~18 hooks; `autoCompact` **disabled**
  deliberately.
- **Commissions, not conversations.** *"A new session doesn't get 'hey can you fix this.'"* A commission
  names the mission, points at the contract document, **separates what is settled from what is open**
  ("It is the contract; do not re-derive what it settles"), states standing rules, and assigns ownership
  — including "You OWN the workflow: decompose the mission into your own dynamic orchestration." A
  deliberate inversion: *"Most people hold the objective in their head and drip-feed it to the agent. I
  write the objective down once, hand over ownership, and spend my attention on the gates instead of the
  steering wheel."*
- **Three gates, in sequence, none advisory.** (1) A **plan-checker** agent audits the plan before
  execution — planner and checker never share a context. (2) A **Nyquist test gate**, named for
  Nyquist–Shannon: *"sample a signal too sparsely and you reconstruct the wrong one"* — sample the change
  surface densely enough to reconstruct what was actually built and catch where it **aliases away from
  what was asked.** (3) A **goal-backward verifier**: forward verification asks "does the code run?";
  goal-backward starts from the original intent and walks in reverse — *"for every requirement in the
  plan, where in the diff is it satisfied? Any requirement without evidence fails the audit, even if all
  the tests pass."* **A PR opens only on PASS.** `/spawn` verifies delivered work **by reading the git
  log, not by trusting what the children report.**
- **Bounded audit loops.** Two revisions on a plan, two attempts on a fix, then a human is pulled in.
  *"Unbounded loops are how agents burn hours polishing a wrong answer."*
- **Every handoff is a document, not a conversation.** *"Documents survive context windows.
  Conversations don't."* Durable memory is an explicit versioned context layer: a `status.md` that **is**
  the reference (not the chat), a `handoff.md` "session baton" (mission, repo state, locked decisions,
  open gates, a **"not your problem" scope boundary**, pickup checklist — travelling between machines
  over `scp`), a decision log "for the calls you never want re-litigated," dated sprint directories.
  *"If you copy one practice from this article, make it this one: give your harness explicit context
  layers."*
- **Orchestrator mode: the coordinator never writes code.** `/orchestrator on` makes the session
  coordination-only — "a chief of staff." Per-branch work routes to a **durable background child agent
  keyed by branch**, alive for the life of that branch so it **accumulates context instead of starting
  cold**, each in its own git worktree. The orchestrator keeps a **branch table and restates it at every
  status check** — *"restatement is how state survives context compaction. Anything that isn't restated
  or written down eventually evaporates."*
- **Fork-join, with four deliberate departures from the classic model** (Doug Lea's Java 7 Fork/Join,
  Cilk before it): the **fork is a dispatch plan, not a thread pool** (explicit file ownership,
  dependency waves, human approval before anything runs — "the fork is a decision, not a default");
  **workers are durable and named, not anonymous**, so *"the shared-state hazard that fork-join
  frameworks spend so much effort containing never materializes, because ownership is assigned at the
  fork instead of negotiated during execution"*; the **join is a gate, not a barrier**; and — the
  load-bearing one — **the serial part moved, it didn't shrink.** Amdahl's law still caps it:
  *"Generation parallelized; verification did not… Fork-join doesn't eliminate the serial work. It
  concentrates it at the join, which is exactly where my gates live."*
- **The trust ledger.** A hook on **every tool call** scores behaviour; every session starts at
  **50/100, level L2**. Levels gate tools: **L1** file edits, **L2** mutating bash + spawning agents,
  **L3** push/PR/deploy/external sends, **L4** destructive ops. Deductions are **Fibonacci-scaled**
  (2,3,5,8,13,21) "so small slips stay cheap while severe or repeated failures escalate super-linearly":
  delivery miss −5, **unverified claim −8**, **fabrication −13**, **tampering with the ledger itself
  −21**, and **self-reporting a violation a flat −3, "because disclosure should always be cheaper than
  discovery."** Only the operator awards points. **Below 20 the agent is terminated** — all mutating
  tools denied, fresh session. *"It works because it prices honesty into the system."*
- **The statusline is the instrument panel.** Two gauges permanently visible: **context** (ten-segment
  meter normalized against the autocompaction reserve, green→yellow→orange→blinking red skull) and
  **trust** (level + score). Notably the context metric is also written to a bridge file the
  context-monitor hook reads, **so warnings are injected into the agent** — *"The agent sees its own fuel
  gauge, not just me."* "A loop you can't observe is a loop you can't operate."
- **Nothing checks itself.** From a correctness design in one of his projects, generalised to the whole
  harness: engines → a verifier that proves the engines agree → **a separate evaluator with an
  independent ground truth that catches the case where both engines misread the same thing.** The
  principle: *"never trust a single source; nothing checks itself."*
- **Limits.** A single practitioner's self-report about his own rig, with **no measurement of outcomes**
  — no throughput figure, no defect rate, no before/after, no comparison against a simpler setup. All
  quantities in the piece are **configuration, not evidence**: the 50/100 start, the Fibonacci penalty
  schedule, the `MAX_ITERATIONS`-style bounds, "nine packets," "twenty plans across four phases." None
  of them is a result, and the trust ledger's efficacy claim (*"an agent that loses more trust by hiding
  a mistake than by admitting it will admit mistakes"*) is asserted from first principles, never tested.
  Project names in his examples are **changed** by his own note. Tool-specific to Claude Code's hook,
  worktree and statusline surfaces as of Aug 2026. Also: he does not report what the ledger costs — how
  often sessions terminate, or how much operator time the point-awarding consumes.

## Connections / contrast

**A third, incompatible answer to "what is a loop."** [[voss-what-the-hell-is-a-loop-anyway|Voss]] says
the word covers four *different* architectures with different exit conditions and different human roles.
[[wong-loop-engineering-teaching-ai-agents-how-to-think|Wong]] says a loop is *one* thing (task + check)
at one rung of a ladder. Miracle says the loops are **many but identical** — three time scales running
**one grammar**, which is precisely what makes it a triangle rather than a stack. Voss's taxonomy is
built on the loops being *unalike*; Miracle's is built on them being *alike*. Both cannot be the frame.
What all three do converge on is the **feedback criterion**: Voss's "a loop without feedback is just a
`for` statement" and Miracle's "feedback that doesn't refine the next objective is just logging… a loop
and not a pipeline" are the same test, independently stated.

**The trust ledger is new to the KB and belongs on [[autonomy-ladder]].** Every autonomy ladder the KB
holds is *staged by task class* — you decide up front how much rope this kind of work gets. Miracle's is
**continuously recomputed from scored behaviour within a session**, which is a different mechanism:
autonomy as a *revocable running balance*, not a *setting*. It is the concrete instance of
[[addyosmani-own-the-outer-loop|Osmani's]] back-pressure ("grant autonomy deliberately under the
maximum") with an actual meter, and of [[dilger-trust-needs-to-be-engineered|Dilger's]] "trust needs to
be engineered." The **−3 self-report discount** is the sharpest idea in the piece: an incentive design
aimed squarely at the "agent declares victory it hasn't earned" failure that
[[bockeler-tdd-inside-the-agent-loop|Böckeler]] and [[wong-loop-engineering-teaching-ai-agents-how-to-think|Wong]]
both identify — priced rather than policed.

**Goal-backward verification is a distinct verifier type the KB had not named before this source.** The KB's verification
vocabulary is *deterministic check* vs *LLM-as-judge* vs *maker ≠ checker*. Miracle adds a third axis:
**direction**. Forward = does it run; **backward = for each stated requirement, where is the evidence in
the diff.** That is a direct answer to [[addyosmani-human-judgment-relocates|Osmani's]] "when green is
misleading" (the agent changed the assertion instead of satisfying the intent) and to
[[dilger-markdown-is-a-suggestion-dressed-as-a-spec|Dilger's]] spec-drift worry, and it maps cleanly onto
[[given-when-then]] — a GWT set *is* a backward-verifiable requirement list.

**Amdahl at the join** is the most rigorous version in the KB of the claim
[[addyosmani-code-agent-orchestra|Osmani]] states as "the bottleneck has shifted… it's verification" and
[[addyosmani-human-judgment-relocates|"my cognitive bandwidth does not scale with the agents"]]: not a
lament but a structural bound — **you can only parallelize the parallel fraction, and verification did
not parallelize.** It gives [[software-factory]]'s back-pressure rule a formal underpinning.

**"The harness is a place, not a prompt"** and the portable versioned `~/.claude` repo corroborate
[[breunig-harnesses-are-situated-agents|Breunig's]] stickiness thesis from the individual's side —
Breunig argues org-level harness setup creates SaaS-like lock-in; Miracle shows the same lock-in
operating on one person, and treats portability as the countermeasure.

## Links

[[loop-engineering]] · [[harness-engineering]] · [[agent-harness]] · [[autonomy-ladder]] ·
[[software-factory]] · [[multi-agent-orchestration]] · [[unattended-coding-agents]] ·
[[long-running-agents]] · [[feedforward-and-feedback-controls]] · [[context-engineering]] ·
[[context-rot]] · [[token-budget-quality-cliff]] · [[given-when-then]] · [[agent-legibility]] ·
[[agent-observability-and-evals]] · [[comprehension-debt]] · [[decision-trace]] · [[adr]] ·
[[voss-what-the-hell-is-a-loop-anyway]] · [[wong-loop-engineering-teaching-ai-agents-how-to-think]] ·
[[addyosmani-own-the-outer-loop]] · [[addyosmani-practical-loop-engineering]] ·
[[addyosmani-human-judgment-relocates]] · [[dilger-trust-needs-to-be-engineered]] ·
[[bockeler-tdd-inside-the-agent-loop]] · [[breunig-harnesses-are-situated-agents]]

_Source: [[miracle-my-loop-engineering-workflow]] (raw: `raw/articles/miracle-my-loop-engineering-workflow.md`)._
