---
source_url: https://github.com/jwilger/agent-skills
title: "Agent Skills for Software Development (jwilger/agent-skills) — event-modeling skill + factory pipeline"
author: John Wilger (jwilger)
publication: GitHub
published: 2026 (actively evolving; v4.1 factory pipeline; domain-modeling skill listed available as of 2026-02-12)
retrieved: 2026-06-13
type: article
---

# Agent Skills for Software Development (jwilger/agent-skills)

[Verbatim capture of the repository README. This is an on-target EM×agents primary
artifact NOT previously in the KB: a portable Agent Skills repo whose `event-modeling`
skill is the upstream design step that feeds an **autonomous AI-agent build pipeline**
("factory pipeline") — event model → GWT scenarios → vertical slices → autonomous TDD,
review, mutation testing, CI. This is the *opposite* direction from Dymitruk's "agents
as users/processors inside a model" framing and from Qlerify's "AI assists modeling"
framing: here Event Modeling is the human-authored spec that constrains and drives a
team of coding agents. Distinct from the already-captured proophboard/skills source
(different author/project; that one targets prooph board's tool). GitHub site
nav/header/footer chrome stripped. The lengthy version-migration appendices (v2→v3,
v3→v4, v4.0→v4.1 command lists) are omitted as boilerplate; substantive sections kept
in the author's words. Exact publish/commit date not confirmable from the rendered page
(commits/tags pages are client-rendered); repo shows 145 commits, 51 tags, v4.1, "© 2026".]

## Agent Skills for Software Development

Portable [Agent Skills](https://agentskills.io) that encode professional
software development practices -- TDD, domain modeling, event modeling,
code review, architecture decisions, and team-based ensemble workflows.
These skills teach any AI coding agent a disciplined SDLC process,
regardless of which harness or editor you use.

**Highlighted capability: Ensemble Team Workflow.** The `ensemble-team`
skill creates a full AI expert team for your project -- with tiered
presets (full/lean/solo-plus), consensus-based planning via Robert's
Rules, ping-pong TDD pairing, mob code review, and built-in
retrospectives.

## Skill Inventory

### Tier 0 -- Entry Point
- `bootstrap` — Zero-config onboarding, harness/capability detection, AGENTS.md generation, skill recommendations

### Tier 1 -- Core Process (universal, standalone)
- `tdd` (build) — Adaptive TDD cycle with guided and automated modes; detects harness capabilities and routes to the best execution strategy
- `domain-modeling` (decide) — Parse-don't-validate, primitive obsession detection, type-driven design
- `code-review` (ship) — Three-stage review protocol: spec compliance, code quality, domain integrity
- `architecture-decisions` (decide) — ADR format, governance, and lightweight decision records
- `event-modeling` (understand) — Discovery, swimlanes, GWT scenarios, model validation
- `ticket-triage` (plan) — Evaluate ticket readiness against six criteria with actionable remediation guidance

### Tier 2 -- Team Workflows (benefit from harness delegation support)
- `ensemble-team` (setup) — Full AI team setup with tiered presets (full/lean/solo-plus), ping-pong TDD pairing, mob review, progressive disclosure, and consensus-based planning
- `task-management` (build) — Work breakdown, state tracking, dependency management

### Tier 3 -- Utility
- `debugging-protocol`, `user-input-protocol`, `memory-protocol`

### Tier 4 -- Factory Pipeline (requires pipeline orchestrator)
- `pipeline` (all) — Three-phase factory pipeline orchestrator: plan → build → review. Boundary-enforced TDD gates, enriched slice context, git worktree isolation
- `ci-integration` (ship) — Quality gate definitions and CI adapter for automated pass/fail decisions
- `factory-review` (review) — Structured human review protocol for factory output with audit trail

### Advanced (optional)
- `mutation-testing`, `atomic-design`

## Architecture

### Skills-Only with Optional Hardening

**Skills** are portable markdown documents (SKILL.md) that teach an agent
*what to do*. They conform to the [Agent Skills specification](https://agentskills.io/specification)
and work on any compatible harness. Skills are the single source of truth
for all practices.

**Enforcement is proportional to capability.** Skills adapt to what the
harness provides. On harnesses with delegation primitives (subagents),
the `tdd` skill uses structural enforcement -- context isolation,
handoff schemas, and role specialization. On harnesses without
delegation, the agent follows practices by convention with self-verification
checklists.

**Optional hardening.** On Claude Code, the bootstrap skill can install
hook templates that add mechanical enforcement: pre-tool-use hooks that
block unauthorized file edits per TDD phase, post-tool-use hooks that
require pasted test output, and subagent-stop hooks that enforce mandatory
domain review.

## Harness Compatibility

Skills work on every harness (Claude Code, Codex, Cursor/Windsurf, OpenCode,
Goose, Amp, Aider). The `tdd` skill auto-detects available delegation
primitives and selects the best execution strategy. The factory pipeline
adapts to harness capabilities: full structural enforcement on Claude Code
(parallel slices in git worktrees), serial execution on Codex, and
advisory-mode gate checking on harnesses without delegation primitives.

## Factory Pipeline (v4.0+)

v4.0 introduces a factory pipeline that automates the build-and-ship
phases while keeping humans in control of planning and review.

v4.1 adds four improvements to the pipeline:

- **Boundary-level acceptance test enforcement.** The TDD gate now
  requires acceptance tests to exercise an external boundary (HTTP, CLI,
  message queue, websocket, Playwright UI, or manual verification).
  Tests that only call internal functions are rejected. CYCLE_COMPLETE
  evidence includes `boundary_type` and `boundary_evidence` fields.
- **Pre-implementation context checklist.** Before dispatching a TDD
  pair, the pipeline gathers architecture docs, glossary, domain types,
  and **event model context**. This is passed as `project_references` and
  `slice_context` to the TDD orchestrator.
- **Enriched slice context.** Each slice now carries a `context` block
  with boundary annotations on GWT scenarios, **event model source path**,
  related slices, domain types referenced, and UI components referenced.
- **Git worktree isolation for parallel slices.** At full autonomy,
  parallel slices execute in isolated git worktrees at
  `.factory/worktrees/<slice-id>`. Falls back to sequential execution
  when `git worktree` is unavailable.

### Three-Phase Workflow

1. **Human-driven (understand + decide).** The human defines what to build
   -- requirements, acceptance criteria, architecture decisions. The AI team
   helps with **event modeling**, domain modeling, and planning, but the human
   approves the plan.
2. **Agent-autonomous (build + ship).** The pipeline executes the approved
   plan without blocking on human input. Quality gates (tests, mutation
   score, CI status) replace human approval gates. Decisions are classified
   as gate-resolvable, judgment-required (batched for review), or blocking
   (pipeline halts). The full TDD cycle, code review, and CI integration
   run autonomously.
3. **Human review (inspect + tune).** The human reviews shipped work,
   batched decisions, and the audit trail. Feedback flows back into the
   next planning cycle.

### Progressive Autonomy
- **Conservative:** Agent proposes, human approves each vertical slice before build begins.
- **Standard:** Agent builds autonomously. Human reviews at the end of each batch. Rework autonomous up to 2 cycles per gate.
- **Full:** Agent selects pairs, orders slices, and optimizes based on factory memory. Human reviews completed batches only.

### Prerequisites for the Factory Pipeline
- An ensemble team already set up (`ensemble-team` skill, Phase 1-5 complete)
- **Vertical slices defined (from event modeling with GWT scenarios)**
- A CI/CD pipeline configured for your project
- The three factory skills installed: `pipeline`, `ci-integration`, `factory-review`

### Typical Session
1. **Plan (human + team):** You describe what to build. The coordinator
   facilitates **event modeling**, domain modeling, and vertical slice definition
   using the full Robert's Rules protocol.
2. **Configure and hand off:** The team agrees on autonomy level and gate
   thresholds. The coordinator hands the slice queue, team roster, and config
   to the pipeline controller.
3. **Build (autonomous):** The pipeline takes each slice through:
   decompose → TDD pair implements → full-team code review → address
   feedback → mutation test → push + CI → merge or escalate. No human
   input required unless a gate fails 3 times or a blocking concern is raised.
4. **Review (human):** Invoke the `factory-review` skill — it shows slices
   completed, rework rate, gate failures, pending escalations, and quality trends.

### Slice queue / event-model coupling (v4.1)
Slices now require a `context` block with at least one GWT scenario that
has a `boundary` field; enqueue validation rejects slices missing this.
A recommended `project_references` section in `.factory/config.yaml`
includes `event_model_root: docs/event-model/`, which the pipeline gathers
before dispatching each TDD pair.

(Per the related agentskills.so listing for this skill: the `event-modeling`
skill runs a two-phase process — Phase 1 domain discovery producing overview
documentation, Phase 2 workflow design generating workflow overviews and slice
files — eliciting actors, events, commands, read models, automations, and slices;
generating Given/When/Then scenarios; and running model validation. Incomplete
models with missing GWT scenarios and undefined automations block slice
decomposition in pipeline-mode gating.)

## License
CC0 1.0 Universal.
