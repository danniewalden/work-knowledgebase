---
title: "Source: Osmani — The Code Agent Orchestra"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [addyosmani-code-agent-orchestra]
raw_file: [raw/articles/addyosmani-code-agent-orchestra.md]
tags: [multi-agent-orchestration, agentic-coding, loop-engineering, ralph-loop, uncitable-figure, focus]
---

# Source: Osmani — The Code Agent Orchestra

Source: [[addy-osmani]], *"The Code Agent Orchestra — what makes multi-agent coding work"*,
addyosmani.com, **2026-03-26** (write-up of an O'Reilly AI CodeCon talk). Raw capture:
`raw/articles/addyosmani-code-agent-orchestra.md`. The **earliest** Osmani piece in the KB and the
antecedent to his loop-engineering arc — it predates [[addyosmani-loop-engineering]] by ~2.5 months.

**Read the markers first.** Almost every quantity in this piece is the author's practitioner judgement
or a demo observation, **not a study result** (see Limits), and its one apparently-researched claim —
about LLM-generated `AGENTS.md` files — **names and links no study anywhere on the page and must not be
repeated as a finding.** **NOT INDEPENDENT** for the agentic-engineering framing generally: Osmani is a
Director at Google Cloud AI, the piece closes by promoting his own O'Reilly book on the subject, and it
cites his own earlier posts ("The Future of Agentic Coding", "The Factory Model") as support for its own
concepts.

## Summary

The shift **from conductor to orchestrator**: from one agent in a tight synchronous loop, where *"your
ceiling was whatever fit in that single context window"* and *"the conversation thread was your
workspace,"* to many asynchronous agents each with its own context window and file scope, where *"the
codebase becomes your canvas, not a conversation thread."* Osmani names the **three walls of the
single-agent ceiling** (context overload, no specialization, no coordination), then walks three patterns
that break them — **subagents**, **Agent Teams**, and **purpose-built orchestration tools** — and closes
on the discipline: *"The human bottleneck was a feature, not a bug."*

## Key points

- **The three walls.** **Context overload** — "large codebases overwhelm a single context window."
  **No specialization** — a generalist juggling data layer, API, UI and tests is "master of none."
  **No coordination** — "even if you spawn helpers, they can't communicate, share a task list, or resolve
  dependencies." *Subagents solve the first two; Agent Teams solve all three.*
- **Pattern 1 — subagents, and what they don't give you.** A parent decomposes and spawns children with
  **explicit file ownership and report artifacts** (his worked example: a Data Layer subagent writes
  `db.js` + `DATA.md`, a Business Logic subagent writes `validation.js` + `LOGIC.md`, and an API Routes
  subagent **reads both reports** before building `server.js`). What's missing: *"the parent must
  manually manage the dependency graph. There's no peer messaging between agents. There's no shared task
  list. And if you're sloppy about file scoping, two agents could write to the same file."*
- **Hierarchical subagents — teams of teams.** *"Instead of your orchestrator spawning six subagents —
  which fragments its context — spawn two feature leads. Each feature lead then spawns its own two or
  three specialists… The parent never sees those details. This mimics how real engineering organizations
  work. You don't have the VP of Engineering assigning tasks to individual engineers."*
- **Pattern 2 — Agent Teams: the coordination primitives, which are the transferable part.** Three
  layers — **Team Lead** (decomposes, creates the task list, synthesizes), a **shared task list**
  (statuses pending/in_progress/completed/blocked, **explicit dependencies**, and **file locking**), and
  **teammates** (independent instances, own context windows, tmux panes). Two mechanisms matter:
  **automatic dependency resolution** (a completed task flips its blocked dependents to pending, and a
  teammate picks them up) and **peer-to-peer messaging** — *"The backend agent tells the frontend agent
  the API contract directly: 'GET /search?q= returns [{id,title,url}].' This doesn't go through the
  lead… This peer-to-peer approach prevents the lead from becoming a coordination bottleneck."*
  Experimental, behind `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`.
- **Reliability pro-tips.** A hard `MAX_ITERATIONS=8` per teammate plus a **forced reflection prompt
  before each retry** — *"What failed? What specific change would fix it? Am I repeating the same
  approach?"* — because *"without it, agents loop endlessly trying the same broken approach."* And a
  **dedicated `@reviewer` teammate**: read-only, on a strong model, tools limited to *lint, test,
  security-scan*, **auto-triggered on every TaskCompleted event**, at 1 reviewer per 3–4 builders, so
  *"the lead only sees green-reviewed code. It's like having a permanent CI quality gate built into the
  team itself."*
- **Three quality gates.** **Plan approval** — teammates write a plan, the lead approves or rejects
  before code exists (*"far cheaper to fix a bad plan than to fix bad code"*; his demo has the lead
  rejecting a plan for missing a database migration step). **Hooks** — a `TeammateIdle` hook verifies
  tests pass before an agent may stop; a `TaskCompleted` hook runs lint and tests, and *"if the hook
  fails, the agent keeps working until it passes."* **`AGENTS.md` for compound learning** — every session
  reads it, every session adds to it.
- **A three-tier tool taxonomy, dated to 2026** and useful as a census: **Tier 1** in-process subagents
  and teams (single session, no extra tooling — "start here"); **Tier 2** local orchestrators, agents in
  isolated worktrees with dashboards/diff review/merge control, "best for 3-10 agents on known
  codebases" (Conductor, Vibe Kanban, Gastown, OpenClaw + Antfarm, Claude Squad, Antigravity, Cursor
  Background Agents); **Tier 3** cloud async — *"Assign a task, close your laptop, return to a pull
  request"* (Claude Code Web, GitHub Copilot Coding Agent, Jules, Codex Web). *"Most developers in 2026
  will use all three tiers — Tier 1 for interactive work, Tier 2 for parallel sprints, Tier 3 to drain
  the backlog overnight."* His broader observation from the tool survey: **"the control plane is becoming
  the primary experience, and the editor is one instrument underneath it."**
- **Multi-model routing as a committed artifact.** A `MODEL_ROUTING.md` mapping planning → a cheaper
  model, implementation → Sonnet/Opus/Codex, review → a dedicated security model.
- **The Ralph loop, restated in five steps** — **pick** (next task from `tasks.json`) → **implement** →
  **validate** (tests, types, lint) → **commit** (if checks pass, and update task status) → **reset**
  (clear context, start fresh). *"The key insight is stateless-but-iterative. By resetting each
  iteration, the agent avoids accumulating confusion."* **Four channels of memory persist across
  resets: git commit history, a progress log, the task state file, and `AGENTS.md` as long-term semantic
  memory.** Safeguards: feed errors back for auto-retry but **kill and reassign after 3+ stuck
  iterations**; always feature branches; hard limits on iterations, time and tokens; the agent opens a PR
  and you review before merge. Credited to Geoffrey Huntley **and Ryan Carson** (whose `ralph` tool and
  Antfarm project implement it) — the Carson attribution is new to the KB.
- **Self-improvement via `REFLECTION.md` proposals.** After every task, force the agent to write: *what
  surprised me, one pattern to add to `AGENTS.md`, one prompt improvement.* **The lead reviews and merges
  approved learnings** — *"This is how compound learning actually compounds — systematically, not ad
  hoc."*
- **Gastown's "beads."** *"Immutable, git-backed records of every decision and outcome with full
  provenance. Agents query past beads through task graphs and a SQL-addressable data plane — not
  traditional vector-based RAG, but structured, queryable institutional memory that goes far beyond a
  flat markdown file."*
- **The discipline argument, which is the best-written part.** *"When humans write code slowly, you feel
  the pain early… Pain is immediate, so you fix as you go. With an orchestrated army of agents, there's
  no natural bottleneck. Small harmless mistakes — a code smell here, a duplication there, an unnecessary
  abstraction — compound at a rate that's unsustainable. **You have removed yourself from the loop, so
  you don't feel the pain until it's too late.** Then one day you try to add a feature, and the
  architecture doesn't allow it. **Your tests are equally untrustworthy because agents wrote those
  too.**"*
- **The bottleneck has shifted — to verification.** Four named reasons, all specific: tests that passed
  before a change don't guarantee they catch regressions from it; agents write tests that are
  *"technically valid but miss the cases that matter"*; context limits mean constraints outside the
  current view get missed; and **"flaky environments, which a single developer encounters as an annoying
  edge case, become systemic blockers when forty agents hit the same flaky test simultaneously."**
- **Delegate the tasks, not the judgment.** Keep: architecture and API design (*"agents have seen tons of
  bad architecture in their training data and will happily cargo-cult enterprise patterns into your
  startup"*), **deciding what NOT to build** (*"saying no is a feature agents don't have"*), and review
  with full system context (*"agents only ever have a local view"*).
- **The spec is the leverage, and it multiplies both ways.** *"Ambiguous requirements propagate through
  dozens of parallel runs, each going slightly wrong in a slightly different direction… The spec isn't a
  prompt anymore. The spec is product thinking made explicit. This is why strong software engineers get
  more leverage from these tools than weak ones."*
- **The factory production line:** Plan → Spawn → **Monitor** (*"every 5-10 minutes. Don't hover"*) →
  **Verify** → Integrate → **Retro**. With WIP limits (*"Don't run more agents than you can meaningfully
  review"*), kill criteria, and **"one file, one owner."**
- **UNCITABLE FIGURE — do not repeat as a finding.** The page asserts: *"Research has shown that 'LLM-
  generated AGENTS.md files offer no benefit and can marginally reduce success rates (~3%) while
  increasing inference costs by 20%+.' Developer-written context files, by contrast, provide a modest ~4%
  improvement."* **No study is named or linked anywhere in the page text**, so the citation cannot be
  followed from this capture and the three figures (~3%, 20%+, ~4%) are unverified. The *practice* he
  derives from it — **human-curated `AGENTS.md` only; never let an agent write to it directly; the lead
  approves every line; keep it short with clear sections (STYLE / GOTCHAS / ARCH_DECISIONS /
  TEST_STRATEGY)** — is a defensible practitioner recommendation on its own and can be carried as such.
  The numbers cannot.
- **Limits.** **IMPRESSION NOT MEASUREMENT for every other quantity in the piece**, and they should
  never be promoted to figures: *"Parallelism (3x throughput)"*; *"3-5 teammates is the sweet spot"*;
  *"three focused agents consistently outperform one generalist agent working three times as long"*;
  *"[forced reflection] substantially cuts stuck agents"*; the per-agent token budgets (Frontend 180k,
  Backend 280k, auto-pause at 85%); and *"cost-neutral at roughly 220k tokens total"* for the subagent
  demo. These are the author's judgement and observations from four **demo videos** (which the capture
  notes are not reproducible in text — only the surrounding prose is present), built on a toy bookmarks
  app. **NOT INDEPENDENT** as above. Everything about Agent Teams is **experimental** and
  product-version-bound; the Tier 1/2/3 tool census will age within months. Steve Yegge's "8 levels of
  AI-assisted coding" is cited as a framework without evaluation.

## Connections / contrast

**This is the KB's missing antecedent for [[multi-agent-orchestration]] on the coding side.** That page
is currently built from protocol/architecture sources (Anthropic's orchestrator-worker patterns, the EDA
fabric, [[devadoss-cead-capability-aligned-agent-design|CEAD]], [[martinfowler-prince-building-reliable-agentic-ai-systems|PRINCE]]).
Osmani supplies the **coding-agent coordination primitives** it lacks: a shared task list with explicit
dependencies and **file locking**, **automatic dependency unblocking**, and **peer-to-peer messaging that
routes around the lead.** Those three are a concrete alternative to both the blackboard
([[edwards-alexander-an-accidental-blackboard]], schema-less shared memory, no routing) and the graph
([[wong-graph-engineering-wiring-agents-into-an-organization]], [[prefect-loops-vs-graphs]], explicit
edges). Three structurally different coordination substrates, now all in the KB, with **no source
comparing them.**

**"One file, one owner" is in direct tension with the accidental blackboard.** Osmani's rule is
partition-by-ownership: *"Never let two agents edit the same file. Conflicts kill velocity."*
Edwards-Alexander's effect required the opposite — everybody reading and writing a shared surface,
continuously — and it died when the push frequency was reduced. **Partition avoids the CI load;
sharing buys coordination and knowledge transfer.** Neither source acknowledges the trade-off; it is a
real open question and belongs on [[multi-agent-orchestration]].

**It anticipates the loop-engineering arc by 2.5 months.** The "human bottleneck was a feature, not a
bug" argument is [[comprehension-debt]] with a mechanism (**you stop feeling the pain**), and *"your
tests are equally untrustworthy because agents wrote those too"* is the sharpest one-line statement in
the KB of why maker ≠ checker cannot be satisfied by agent-written tests — sitting directly against
[[bockeler-tdd-inside-the-agent-loop|Böckeler's]] measured result and
[[addyosmani-human-judgment-relocates|his own]] "when green is misleading." The **`REFLECTION.md` with
lead approval** is [[loop-engineering]]'s hill-climbing loop with a **human merge gate** — a design
[[morris-humans-and-agents-in-software-engineering-loops|Morris]] describes as an early rung on the way
to auto-approval, and one [[ahe-agentic-harness-engineering|AHE]] removes entirely. Useful as the
conservative end of that spectrum.

**Gastown's "beads" is an event-sourced agent memory in the wild.** Immutable, git-backed, full
provenance, queried through task graphs and a SQL data plane, explicitly *not* vector RAG — that is
[[event-sourcing]] plus projections applied to agent memory, and it belongs alongside
[[esaa-event-sourcing-for-autonomous-agents]], [[event-sourced-agentic-patterns]] and
[[nick-tune-graphs-memory-skills-agents]] as an independent arrival at the same design. Second-hand
here, and unevaluated.

**The forty-agents-hit-the-same-flaky-test observation** is the best argument in the KB for treating
environment reliability as a *scaling* property rather than hygiene — it converges with
[[addyosmani-agentic-code-quality|his own]] "brittle environments that don't hold up under script-driven
stress" and with [[edwards-alexander-an-accidental-blackboard|the CI-overload finding]]: at agent scale,
**shared infrastructure becomes the contended resource**, not the codebase.

## Links

[[multi-agent-orchestration]] · [[agentic-coding]] · [[loop-engineering]] · [[ralph-loop]] ·
[[software-factory]] · [[comprehension-debt]] · [[harness-engineering]] · [[agent-harness]] ·
[[graph-engineering]] · [[spec-driven-development]] · [[context-engineering]] · [[token-budget-quality-cliff]] ·
[[feedforward-and-feedback-controls]] · [[event-sourcing]] · [[event-sourced-agentic-patterns]] ·
[[unattended-coding-agents]] · [[long-running-agents]] · [[agent-observability-and-evals]] ·
[[addy-osmani]] · [[addyosmani-loop-engineering]] · [[addyosmani-practical-loop-engineering]] ·
[[addyosmani-human-judgment-relocates]] · [[addyosmani-agentic-code-quality]] ·
[[addyosmani-software-factories-light-and-dark]] · [[addyosmani-earning-taste-and-judgment]] ·
[[edwards-alexander-an-accidental-blackboard]] ·
[[wong-graph-engineering-wiring-agents-into-an-organization]] · [[prefect-loops-vs-graphs]] ·
[[bockeler-tdd-inside-the-agent-loop]] · [[morris-humans-and-agents-in-software-engineering-loops]] ·
[[ahe-agentic-harness-engineering]] · [[nick-tune-graphs-memory-skills-agents]] ·
[[esaa-event-sourcing-for-autonomous-agents]]

_Source: [[addyosmani-code-agent-orchestra]] (raw: `raw/articles/addyosmani-code-agent-orchestra.md`)._
