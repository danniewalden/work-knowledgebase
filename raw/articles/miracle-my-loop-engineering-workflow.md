---
source_url: https://www.andrewmiracle.com/2026/08/10/loop-engineering-with-an-agent-harness.html
title: My Loop Engineering Workflow
author: Andrew Miracle
publication: andrewmiracle.com (Essays / Artificial Intelligence)
published: 2026-08-10
retrieved: 2026-08-21
type: article
---

# My Loop Engineering Workflow

*Planted on August 10, 2026 | Last watered on August 10, 2026 | 11 minutes | 🌱 Seedling*

[Image: a desktop of terminal panes running concurrent agent loops — decryption progress bars, hexdumps, traceroute, and a process monitor, with the statusline showing trust level L2 at 50 points.]

People ask me how I get agents to ship real work. They usually expect a prompt.

I don't have a prompt. I have a triangle of loops.

Prompt engineering is about what you say to a model once. Loop engineering is about designing the cycles the model runs inside: how work enters, how it gets decomposed, how it executes, how it gets verified, and how the result feeds the next round. The prompt is maybe five percent of the outcome. The loops are the rest.

This is how my setup actually works today, from `~/.claude` (https://github.com/koolamusic/claudefiles) to a delivered pull request. No ideology. Just the machine I run every day.⊕

> Project names in the examples are changed; the mechanics are exactly as run.

## The triangle of loops

My work runs on three nested loops, each operating at a different time scale:

- **The session loop**: one agent session, measured in hours. It opens with a written commission and closes with a structured closeout or a handoff document.
- **The sprint loop**: one research → plan → execute → retro cycle, measured in days. My jira plugin defines a sprint as exactly that: one research, plan, execute cycle, with review and retro for closing the loop.
- **The program loop**: the long horizon, measured in weeks. A kickoff produces PROJECT.md and a phased ROADMAP.md; delivery programs decompose into packets.⊕

> My v1 program ran nine packets; the v2 delivery program carries twenty plans across four phases.

Session loops nest inside sprint loops. Sprint loops nest inside program loops. And here is the part that makes it a triangle instead of a stack: every loop, at every scale, runs the same grammar and shares the same start point and end point.

The grammar is a recursion:

**objective → execution → feedback → refined objective → execution → …**

The start point is always a written commission: that is the objective. The end point is always the same pair: ship only what passes verification, then a retro: that is the feedback. And the retro's output is a refined objective, the next commission sharpened by what the feedback taught. That refinement step is why the loop converges instead of spinning.

[Diagram: The triangle of loops — session (commission → closeout, hours), sprint (research → plan → execute → retro, days), program (roadmap → packets → delivery, weeks); sessions nest inside sprints, sprints nest inside programs; objective → execution → feedback → refined objective → execution → …; start: a written commission · end: ship on PASS + retro.]

*Three loops, three time scales, one grammar, one start and one end.*

Once you see the triangle, the rest of this article is just a tour of its parts: the harness the loops run on, the start point, the middle loop up close, the fork-join shape of execution, the gates at the end point, and the memory that makes nesting possible.

## The harness is a place, not a prompt

The loops run on infrastructure that lives in `~/.claude`, and it is a versioned system, not a text file I paste around.

At the top is `CLAUDE.md`, which I treat as an operating contract between me and any agent session. It encodes the rules I learned the hard way:

- **Phased execution.** Never attempt a multi-file refactor in a single pass. Finish phase one, run verification, wait for approval before phase two.
- **Forced verification.** An agent is forbidden from reporting a task complete until it has run the project's actual checks and fixed what they surface. If no checker is configured, it must say so instead of claiming success.
- **Failure recovery.** If a fix fails twice, stop. Re-read the whole section, find where the mental model was wrong, and propose something fundamentally different. No third attempt at the same idea.

Underneath the contract, `settings.json` tunes the machine: acceptEdits as the default permission mode,[1] pre-approved permissions for the tools I trust, and all AI attribution stripped from commits and PRs.

And autoCompact stays disabled,[2] because I manage context deliberately rather than letting it truncate silently.

Then there are the hooks.[3] Around eighteen of them fire on session start, prompt submit, and before and after every tool call: a context monitor, a read guard, a commit validator, a statusline, and a trust monitor I'll come back to. There are even audio cues, StarCraft-style WAVs on session start and stop. I can literally hear a session loop open and close.

The whole directory is versioned in its own repository with an auto-updating plugin marketplace. When I migrated to a new server recently, the harness got zipped and cloned alongside my dotfiles, because the agent kit has to be portable or it isn't real. Claude, Cursor, Kimi: the models swap, the harness stays.

## The start point: commissions, not conversations

Every loop at every scale begins the same way: the objective enters as a written commission, never as a chat message.

A new session doesn't get "hey can you fix this." It gets a commission document, modeled on a real one from a data-platform project of mine:

```
cat > PLAN.md <<'EOF'
You are the delivery agent for pulse.rs F4 to F8.
Your commission is the master plan at ~/.context/northstar/project/MASTERPLAN.md.
READ IT FULLY FIRST. It is the contract; do not re-derive what it settles.
You OWN the workflow: decompose the mission into your own dynamic orchestration.
Subagents default to the cheaper model tier; spend the expensive one on the critical path.
Close out with evidence: branch, PR url, tests, blockers, next owner.
EOF
```

A commission names the mission, points at the contract document, separates what is settled from what is open, states the standing rules, and assigns ownership. After that I get out of the way. My go-signals are one word: "yes, push it."

This is a deliberate inversion. Most people hold the objective in their head and drip-feed it to the agent. I write the objective down once, hand over ownership, and spend my attention on the gates instead of the steering wheel.

## The middle loop, up close: from jira to orchestrator

The sprint loop is where the triangle does its daily work, and it runs as a pipeline of skills, each with one job, each handing a verified artifact to the next:

- `/kickoff` turns an empty repo into a working project: PROJECT.md, a phased ROADMAP.md, jira and the project's context layer initialized. Kickoff is alignment, not automation.
- `/grill` is adversarial Q&A. In stress-test mode it attacks a plan one question at a time until the holes surface, ranked BLOCKER, RISK, or NITPICK. In shape mode it co-creates two or three approaches and converges to a decision log. Nothing enters a sprint un-grilled.
- `/jira:research` and `/jira:plan` turn a grilled idea into a sprint. A planner agent drafts the plan, an independent plan-checker[4] agent audits it, and the loop allows a maximum of two revisions before it escalates to me.
- `/jira:execute` fans the plan out to wave-parallel[5] executor agents with explicit file ownership.
- The first gate is a Nyquist test gate, named for the Nyquist–Shannon sampling theorem: sample a signal too sparsely and you reconstruct the wrong one. The gate samples the change surface with tests dense enough to reconstruct what was actually built, and catch where it aliases away from what was asked. Run against the executor output right after execution.
- The second is a goal-backward verifier[6] that checks the work against the original intent. A PR opens only on PASS.
- `/jira:retro` closes the loop and rolls the workflow lessons into the next commission.

A typical instruction from me looks like this:

> Spin all of these into a new /jira:research and sprint named pulse.rs.alpha, plan them, drop the user-facing issues for each, then implement a /loop to execute and deliver all of them.

[Diagram: The sprint loop — Commission → Research → Plan → wave-parallel executors → Verify gate → Ship; planner ⇆ plan-checker, max 2 revisions; FAIL: back to the work; PR only on PASS; /jira:retro · learnings feed the next commission.]

*The sprint loop. Nothing ships without the gate; nothing repeats without the retro.*

Two things to notice. First, the audit loops are bounded: two revisions on a plan, two attempts on a fix, then a human gets pulled in. Unbounded loops are how agents burn hours polishing a wrong answer. Second, every handoff between stages is a document, not a conversation. Documents survive context windows. Conversations don't.

## The orchestrator never writes code

Wrapped around the sprint loop is my longest-running session pattern: orchestrator mode.

`/orchestrator on` turns the current session into a coordination-only thread, a chief of staff. From that moment it never implements anything locally. It classifies every request, and per-branch work gets routed to a durable background child agent keyed by branch. The same child stays alive for the life of that branch, so it accumulates context instead of starting cold. Children that touch code run in isolated git worktrees — a git feature that checks out a second branch into a separate directory backed by the same repository. Two agents can edit two branches at the same time without ever seeing each other's files, and merging stays an ordinary git operation.

The orchestrator maintains a branch table: branch, child agent, status, next action. It restates that table at every status check, which looks redundant until you realize why: restatement is how state survives context compaction. Anything that isn't restated or written down eventually evaporates.

For one-shot fan-outs there is `/spawn`: parse a plan into units with explicit file ownership, group them into dependency waves, present the dispatch plan, wait for my approval, then execute each wave in parallel. Its hard rule is the same as the orchestrator's: you coordinate, you never write application code.

Every child closes out with a structured report: branch, PR URL, test results, blockers, next owner. That closeout is the end of one session loop and the raw material for my status checks.

[Diagram: Orchestrator routing — Operator (me) → Orchestrator session (coordinates · never implements) → commission; branch table, restated every check; children: pulse.rs / core-api / docs, each in its own worktree, each producing a PR; every child closes out: branch · PR url · tests · blockers · next owner.]

*One coordinator, durable branch-keyed children, isolated worktrees, structured closeouts.*

This scales further than you'd expect. A docs-site rewrite of mine ran as an orchestrator plus a seven-phase loop with named child agents, including an independent design-critic agent whose only job was reviewing screenshots for a second opinion. The orchestrator relayed each child's commits, verification results, and deviations back to me in tables, because I ask for evidence over prose.

## Execution is fork-join

The execution edge of the grammar has its own shape, and it comes straight out of parallel computing: the fork-join model. The fork-join model comes out of parallel computing. Doug Lea's Fork/Join framework in Java 7 is the canonical implementation, and Cilk popularized the pattern before it. The shape is universal: split, run concurrently, join. A program forks into parallel tasks, workers run concurrently, and a join barrier collects the results before the program continues. My harness runs the same pattern, with four distinctions that matter more than the similarity.

**The fork is a dispatch plan, not a thread pool.** Classic fork-join forks eagerly: split until the tasks are small enough, then let the runtime schedule them. I fork deliberately. `/spawn` parses a plan into units with explicit file ownership, groups them into dependency waves, presents the dispatch plan, and waits for my approval before anything runs. One wave forks, joins, and only then does the next wave fork. The fork is a decision, not a default.

**The workers are durable and named, not anonymous.** A fork-join pool is anonymous workers stealing tasks from a queue. My children are the opposite: keyed by branch, alive for the life of that branch, accumulating context, each in its own git worktree. The shared-state hazard that fork-join frameworks spend so much effort containing never materializes, because ownership is assigned at the fork instead of negotiated during execution.

**The join is a gate, not a barrier.** A join barrier waits for results and merges them. My join asks a harder question: do these results deserve to exist? The wave's output goes through the Nyquist test gate, then the goal-backward verifier, and a PR opens only on PASS. `/spawn` verifies by reading the git log, not by trusting what the children report. The join doesn't merge output. It merges confidence.

**The serial part moved, it didn't shrink.** Amdahl's law caps every fork-join system: Gene Amdahl, "Validity of the Single Processor Approach to Achieving Large Scale Computing Capabilities" (1967). The serial fraction of any workload caps its parallel speedup, no matter how many workers you add. You can only speed up the parallel fraction, and the serial remainder sets the ceiling. Generation parallelized; verification did not. So the math I laid out in *The Scope Compression Hypothesis* (https://www.andrewmiracle.com/2026/07/11/scope-compression-hypothesis.html) holds inside every loop: generation ≈ max (task time), but delivery ≈ generation + verification. Fork-join doesn't eliminate the serial work. It concentrates it at the join, which is exactly where my gates live.

And the pattern nests the same way the triangle does. The program loop forks sprints. The sprint loop forks waves. The session loop forks subagents. Fork-join at every scale, with a gate at every join.

## The end point: gates, ship, retro

The end point of every loop is feedback, and in my system the feedback comes in threes. A plan-checker audits the plan before execution. A Nyquist test gate checks the work after execution. A goal-backward verifier audits the codebase against the original intent last. Three gates, in sequence, none advisory: `/jira:execute` will not open a PR on a verifier FAIL, full stop, and `/spawn` verifies delivered work by reading the git log, not by trusting the agent's self-report.

The instinct goes deeper than tooling. In that same data-platform project, correctness itself is built in three layers: the engines, then a verifier that proves the engines agree, then a separate evaluator with an independent ground truth that catches the case where both engines misread the same thing. The principle written into that project's decision log applies to the whole harness: never trust a single source; nothing checks itself.

The strangest piece of the harness is also the most effective enforcement of that principle: a trust ledger, applied by a hook on every tool call. Every session starts at 50 out of 100, trust level L2. Levels gate what the agent may do. L1 edits files. L2 runs mutating bash and spawns agents. L3 pushes, opens PRs, deploys. L4 touches destructive operations. Deductions are Fibonacci-scaled: penalties follow the Fibonacci sequence (2, 3, 5, 8, 13, 21) so small slips stay cheap while severe or repeated failures escalate super-linearly. The cost curve itself discourages an agent from testing the edges. A delivery miss costs 5, an unverified claim costs 8, fabrication costs 13, tampering with the ledger itself costs 21. Self-reporting a violation costs a flat 3, because disclosure should always be cheaper than discovery. Only I can award points. Drop below 20 and the agent is terminated: all mutating tools denied, and I start a fresh session.

[Diagram: Trust ladder — levels gate tools, penalties scale, termination below 20. L4 destructive ops · force push, reset --hard; L3 push · PR · deploy · external sends; L2 mutating bash · spawn agents (every session starts here, 50/100); L1 file edits; < 20 · terminated: mutating tools denied. −21 ledger tampering, −13 fabrication, −8 unverified claim, −5 delivery miss, −3 self-report (disclosure < discovery). Only the operator awards points, via /trust +N.]

*The trust ledger: privilege is continuously recomputed from scored behavior.*

It sounds theatrical. It works because it prices honesty into the system. An agent that loses more trust by hiding a mistake than by admitting it will admit mistakes, and an agent whose privileges depend on verification will verify.

After the gates comes the move that completes the grammar: the retro turns feedback into a refined objective. `/jira:retro` rolls the sprint's workflow lessons into durable state, and those lessons shape the next commission. My runbooks make the discipline explicit: every step ends with a verification gate, and you do not proceed past a failed one. Feedback that doesn't refine the next objective is just logging. The end point of one loop is the start point of the next. That is what makes it a loop and not a pipeline.

## The statusline is the instrument panel

A loop you can't observe is a loop you can't operate, so the two numbers that govern every session live permanently at the bottom of my terminal, wired through the `statusLine` parameter in settings.json. It runs a command, a Node script in my hooks directory, that renders the model, the current task or milestone state, the directory, and the two gauges I actually watch.

The first gauge is context: a ten-segment meter with the used percentage, normalized against the buffer the runtime reserves for autocompaction, shifting from green to yellow to orange to a blinking red skull as the window fills. The statusline also writes those metrics to a bridge file that the context-monitor hook reads, so the agent itself gets warnings injected when its context runs low. The agent sees its own fuel gauge, not just me.

The second gauge is trust. The statusline calls the trust monitor in a compact render mode and appends the result: level and score, always visible. L2 · 50 on a fresh session. The cover image of this article shows it in the wild, sitting in the statusline of a session running a wall of loops. At any glance I know how much context the loop has burned and how much privilege the agent currently holds, which are exactly the two numbers that decide whether I let it run, hand it off, or terminate it.

## The memory that makes nesting possible

Three nested loops only work if state survives the boundaries between them, and most people leave that to chance. I engineer it.

The durable memory lives in a private context layer (call it `~/.context/northstar`), a versioned repo of workflow state that is specific to my setup and deliberately internal: a status.md that is the reference for each workstream, a handoff.md that acts as the session baton, a decision log of load-bearing calls, dated sprint directories each with brief, research, plans, execution, and verification artifacts, and the program packets above them. The sprint and program loops live there as documents, so any session loop can pick them up cold.

If you copy one practice from this article, make it this one: give your harness explicit context layers. A PLAN.md the session must read before it touches anything. A status doc that is the reference, not the chat. A decision log for the calls you never want re-litigated. A handoff doc for crossing sessions and machines. The filenames matter less than the discipline: named, durable, versioned context that any agent, on any machine, can pick up cold.

Inside a session, I keep autoCompact off, so nothing gets silently summarized away. `/handoff` compacts a session into a HANDOFF.md a cold agent can pick up: mission, repo state, locked decisions, open gates, a "not your problem" scope boundary, and a pickup checklist. Handoffs travel between machines over scp; a session that runs out of context on one box resumes on another with the document as the contract.

Two smaller habits matter as much. Long-running monitors run in subshells, not in the main thread. I learned that one the hard way and the correction is still in my history: "You were supposed to have this monitor running in a sub shell, so you don't overload your context." And anything the orchestrator needs to remember gets restated on every status check, because restatement is the only compaction-proof memory.

## The loop is the product

Here is the part people underestimate. None of this is about a specific model. The models keep changing and will keep changing. What compounds is the triangle: the contract, the commissions, the fork-join discipline, the gates, the trust accounting, the memory.

Prompt engineering optimizes a message. Loop engineering optimizes a system that keeps delivering after you close the lid of the laptop.

When I say "run this in a loop," what I mean is: set the objective as a written commission, fork the execution into waves, join at the gates, ship only what passes, and let the retro refine the next objective. Session inside sprint inside program, each running the same grammar with the same start and the same end. The agent does the laps. My job is to design the track, hold the gates, and decide what a lap is worth.

That is the whole trick. There is no prompt.

## References

1. A permission mode in the agent runtime: the agent may edit files without stopping to ask approval on every edit. Uncomfortable without gates; liberating with them.
2. Context compaction is what happens when a session's context window fills: the runtime summarizes or truncates older conversation to make room. Anything not written to a file or restated can silently vanish, which is why this whole setup leans on documents instead of chat history.
3. Scripts the runtime fires on lifecycle events: session start, prompt submit, before and after every tool call. Hooks are how the harness enforces policy mechanically instead of relying on the agent to remember the rules.
4. An independent agent whose only job is auditing the plan document before execution: adversarial review of the approach, not the code. Planner and checker never share a context, so the audit is genuine rather than the planner grading its own homework.
5. A group of tasks with no dependencies on each other, dispatched together. A wave must fully join, verified not just finished, before the next wave forks. Waves are how you parallelize a plan without letting dependents run ahead of their prerequisites.
6. Forward verification asks "does the code run?" Goal-backward verification starts from the original intent and walks in reverse: for every requirement in the plan, where in the diff is it satisfied? Any requirement without evidence fails the audit, even if all the tests pass.

*Tags: AI, Agentic Engineering, Engineering Culture. Author: Andrew Miracle, Head of Product & Research, Tecmie. Harness repo referenced throughout: https://github.com/koolamusic/claudefiles*
