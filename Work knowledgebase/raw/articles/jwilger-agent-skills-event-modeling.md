---
source_url: https://github.com/jwilger/agent-skills
title: "Agent Skills for Software Development (jwilger/agent-skills) — event-modeling skill + factory pipeline"
author: John Wilger (@jwilger)
publication: GitHub
published: 2026 (repo at v4.1; 145 commits, 51 tags — exact last-commit date not confirmable via static fetch)
retrieved: 2026-06-13
type: article
---

# Agent Skills for Software Development (jwilger/agent-skills)

[GitHub repository README, captured verbatim. GitHub site nav/chrome and the
v3.x/v2.x migration sections stripped; the author's words retained. This is the
on-target EM×agents source: Event Modeling encoded as a portable AI-coding-agent
skill that, together with a TDD skill and a "factory pipeline," drives autonomous
agents through vertical slices defined by Given-When-Then scenarios. Distinct from
existing captures — Dymitruk's general claim (raw/notes/dymitruk-...), Qlerify's
AI-assists-modeling tool (raw/articles/qlerify-...), and prooph board's skills
(raw/articles/proophboard-skills-...). Here Event Modeling is the human-driven
*design* method whose output (slices + GWT) becomes the machine-checkable contract
an agent team builds against. CC0-1.0 licensed.]

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

| Skill | Description | Phase |
| --- | --- | --- |
| `bootstrap` | Zero-config onboarding, harness/capability detection, AGENTS.md generation, skill recommendations | -- |

### Tier 1 -- Core Process (universal, standalone)

| Skill | Description | Phase |
| --- | --- | --- |
| `tdd` | Adaptive TDD cycle with guided and automated modes; detects harness capabilities and routes to the best execution strategy | build |
| `domain-modeling` | Parse-don't-validate, primitive obsession detection, type-driven design | decide |
| `code-review` | Three-stage review protocol: spec compliance, code quality, domain integrity | ship |
| `architecture-decisions` | ADR format, governance, and lightweight decision records | decide |
| `event-modeling` | Discovery, swimlanes, GWT scenarios, model validation | understand |
| `ticket-triage` | Evaluate ticket readiness against six criteria with actionable remediation guidance | plan |

### Tier 2 -- Team Workflows (benefit from harness delegation support)

| Skill | Description | Phase |
| --- | --- | --- |
| `ensemble-team` | Full AI team setup with tiered presets (full/lean/solo-plus), ping-pong TDD pairing, mob review, progressive disclosure, and consensus-based planning | setup |
| `task-management` | Work breakdown, state tracking, dependency management | build |

### Tier 4 -- Factory Pipeline (requires pipeline orchestrator)

| Skill | Description | Phase |
| --- | --- | --- |
| `pipeline` | Three-phase factory pipeline orchestrator: plan → build → review. Boundary-enforced TDD gates, enriched slice context, git worktree isolation | all |
| `ci-integration` | Quality gate definitions and CI adapter for automated pass/fail decisions | ship |
| `factory-review` | Structured human review protocol for factory output with audit trail | review |

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
hook templates (`skills/tdd/references/hooks/`) that add mechanical
enforcement: pre-tool-use hooks that block unauthorized file edits per
TDD phase, post-tool-use hooks that require pasted test output, and
subagent-stop hooks that enforce mandatory domain review. These are
optional recipes, not a separate plugin layer.

## Factory Pipeline (v4.0+)

v4.0 introduces a factory pipeline that automates the build-and-ship
phases while keeping humans in control of planning and review.

v4.1 adds four improvements to the pipeline:

* **Boundary-level acceptance test enforcement.** The TDD gate now
  requires acceptance tests to exercise an external boundary (HTTP, CLI,
  message queue, websocket, Playwright UI, or manual verification).
  Tests that only call internal functions are rejected. CYCLE_COMPLETE
  evidence includes `boundary_type` and `boundary_evidence` fields.
* **Pre-implementation context checklist.** Before dispatching a TDD
  pair, the pipeline gathers architecture docs, glossary, domain types,
  and event model context. This is passed as `project_references` and
  `slice_context` to the TDD orchestrator.
* **Enriched slice context.** Each slice now carries a `context` block
  with boundary annotations on GWT scenarios, event model source path,
  related slices, domain types referenced, and UI components referenced.
* **Git worktree isolation for parallel slices.** At full autonomy,
  parallel slices execute in isolated git worktrees at
  `.factory/worktrees/<slice-id>`. Falls back to sequential execution
  when `git worktree` is unavailable. Conflicts are detected at merge
  time rather than predicted up front.

### Three-Phase Workflow

1. **Human-driven (understand + decide).** The human defines what to build
   -- requirements, acceptance criteria, architecture decisions. The AI team
   helps with event modeling, domain modeling, and planning, but the human
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

The pipeline supports three autonomy levels:

* **Conservative:** Agent proposes, human approves each vertical slice
  before build begins. Rework requires human sign-off.
* **Standard:** Agent builds autonomously. Human reviews at the end of
  each batch. Rework is autonomous up to 2 cycles per gate.
* **Full:** Agent selects pairs, orders slices, and optimizes based on
  factory memory. Human reviews completed batches only.

### Using the Factory Pipeline — Prerequisites

You need:

* An ensemble team already set up (`ensemble-team` skill, Phase 1-5 complete)
* **Vertical slices defined (from event modeling with GWT scenarios)**
* A CI/CD pipeline configured for your project
* The three factory skills installed: `pipeline`, `ci-integration`, `factory-review`

### Typical Session

1. **Plan (human + team):** You describe what to build. The coordinator
   facilitates event modeling, domain modeling, and vertical slice definition
   using the full Robert's Rules protocol.
2. **Configure and hand off:** The team agrees on autonomy level and gate
   thresholds. The coordinator hands the slice queue, team roster, and config
   to the pipeline controller.
3. **Build (autonomous):** The pipeline takes each slice through:
   decompose → TDD pair implements → full-team code review → address
   feedback → mutation test → push + CI → merge or escalate. No human
   input required unless a gate fails 3 times or a blocking concern is raised.
4. **Review (human):** When the pipeline finishes, invoke the
   `factory-review` skill.

### Slice queue / project references (v4.1)

Slices now require a `context` block with at least one GWT scenario that
has a `boundary` field. Enqueue validation rejects slices missing this.

```
# .factory/config.yaml (project references)
project_references:
  architecture_doc: docs/architecture.md
  glossary: docs/glossary.md
  design_system_catalog: docs/design-system.md
  event_model_root: docs/event-model/
```

The pipeline gathers this context before dispatching each TDD pair.

## Harness Compatibility (excerpt)

Skills work on every harness (Claude Code, Codex, Cursor/Windsurf, OpenCode,
Goose, Amp, Aider). The `tdd` skill auto-detects available delegation
primitives and selects the best execution strategy. The factory pipeline
adapts to harness capabilities: full structural enforcement on Claude Code
(parallel slices in git worktrees), serial execution on Codex, and
advisory-mode gate checking on harnesses without delegation primitives.

## Notes on the `event-modeling` skill (per README + skill-marketplace listing)

The `event-modeling` skill is the "understand"-phase entry: *Discovery,
swimlanes, GWT scenarios, model validation.* Per the skill listing it
activates on phrases like "model this workflow", "event model", "write GWT
scenarios", and "decompose into slices", and covers discovering domain actors,
identifying automations, mapping integrations, and decomposing workflows into
vertical slices. Each pattern maps to one vertical slice — State Change
(Command → Event) and State View (Events → Read Model). When paired with the
`tdd` skill, the GWT scenarios produced by event modeling become the
acceptance tests that enforce the model. The stated value: "communication —
a structured conversation that surfaces hidden domain knowledge and creates
shared understanding between humans and agents before any code is written."
