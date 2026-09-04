---
title: Event-Modeled Agent Design
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [dilger-podcast-episode-47-agentic-modeling-audit-trails, nick-tune-event-sourced-claude-code-workflows, dilger-git-as-primary-persistence-for-event-models, tornhill-blast-from-the-past-sdd-illusion-of-known-scope, dilger-ux-as-first-class-in-spec-driven-development, dilger-only-engineers-care-about-consistent-systems, dilger-ui-only-interactions-filtering, dilger-loop-engineering-never-argue-with-agent, tune-no-rapport-with-a-model-you-didnt-code, dilger-one-million-tokens-self-training-modeling-agent, dilger-modeling-agent-improved-by-learning-loop, dilger-todo-lists-storylines-one-scenario, ng-spec-driven-development-is-waterfall-in-markdown, dilger-eventmodelers-supports-esdm-export, dilger-highlighting-markers-give-context-to-agents, dilger-describing-without-solving-burns-you-out, bockeler-tdd-inside-the-agent-loop, dymitruk-event-modeling-future-proof-agents, qlerify-event-modeling-tool-ai, eventmodeling-what-is-event-modeling, anthropic-effective-harnesses-long-running-agents, stripe-minions-one-shot-coding-agents, proophboard-skills-ai-agent-event-modeling, jwilger-agent-skills-event-modeling, jwilger-agent-skills-factory-pipeline, dilger-spec-driven-development-applied, dilger-faros-ai-report-amplifies-unclear-requirements, dilger-keep-command-handlers-pure, dilger-automatic-domain-discovery-claude-code, dilger-model-is-a-living-spec-always-on-agent, dilger-event-modeling-agent-harness, fraktalio-event-modeler-connect-ai-agents-mcp, dymitruk-ai-trained-on-dysfunction-agents-are-a-must, rico-fritzsche-autonomous-domain-capabilities-ccc, dilger-harness-is-20-percent-requirements-are-80, dilger-first-event-modeling-conference-munich-recap, dilger-planning-like-excel-legible-to-human-and-ai, esdm-event-sourced-domain-modeling, johansen-is-it-safe-to-jump-em-conf-2026, dilger-local-llm-distributed-agent-setup-event-modeling, dilger-triplet-flexible-agent-enabled-architecture, dilger-spec-driven-tools-need-event-modeling-front-half, dilger-the-shapes-event-modeling-anti-patterns, dilger-agentic-collaboration-freeform-drawings, dilger-event-model-structure-linter-reference-catalog, dilger-99-percent-software-boring-two-patterns, dymitruk-ai-melts-barrier-event-modeling-is-the-map]
tags: [event-modeling, agentic-ai, synthesis, focus]
---

# Event-Modeled Agent Design

**Focus-area synthesis** (an active focus area for Dannie, tracked in memory). Can [[event-modeling]] —
the design *method*, not just [[event-sourcing]] — be used to design agent and multi-agent systems?
[[adam-dymitruk]], the method's creator, says yes
([[dymitruk-event-modeling-future-proof-agents]]): "agents can be described as either **users** or
**specific processors**," composable into a multi-agent system "without throwing away your existing
system design." This page works out the mapping and marks where it's externally supported vs. the
KB's own extrapolation.

## The core mapping (Dymitruk's claim)

- **Agent as user** → an actor in a swimlane that issues **commands**, exactly like a human. Useful
  when an agent fronts a workflow (e.g. a Slack-invoked coding agent kicking off a task —
  [[stripe-minions-one-shot-coding-agents]]).
- **Agent as processor** → the **Automation pattern**: a processor works a "todo list," issues
  commands to other systems, and stores their replies back as **events**. This is the natural home
  for autonomous/background agents.
- **Multi-agent system** → several users/processors composed on one timeline, communicating through
  the shared event ledger.

## Construct-by-construct (KB extrapolation onto the harness thread)

| Event Modeling construct | Agent/harness analog (in-KB) |
| --- | --- |
| **Event** (state-changing fact on the timeline) | the append-only progress ledger: `claude-progress.txt` + git history + feature-list JSON ([[anthropic-effective-harnesses-long-running-agents]]); minion run records ([[stripe-minions-one-shot-coding-agents]]) |
| **Command** (an actor's intention) | the task prompt that starts a run (the Slack message to a minion) |
| **View / read model** (passive) | legibility surfaces: AGENTS.md map, progress files, run web UI ([[agent-legibility]]) |
| **Translation pattern** | MCP tools converting external data into local events ([[model-context-protocol]]; Stripe hydrates context over links before a run) |
| **Automation pattern** | the initializer-executor / [[ralph-loop]] working a feature list one item at a time |
| **Given-When-Then** (one per command/view) | feature-list specs + self-verification ([[feedforward-and-feedback-controls]]); Qlerify drafts GWT per event ([[qlerify-event-modeling-tool-ai]]) |
| **Swimlanes / Conway's Law** | subdirectory-scoped agent rules (Stripe); team-owned layered domains ([[openai-harness-engineering-codex]]) |
| **Flat cost curve via explicit contracts** | "enforce invariants, not implementations" + harness templates per topology ([[harness-engineering]]) |

## Why the fit is natural

Both [[event-modeling]] and agent harnesses treat **current state as a replay of an append-only
ledger** and isolate work behind explicit contracts. The KB already argued this for the *substrate*
in [[event-sourced-agentic-patterns]] (event sourcing as the agent backbone); this page adds the
*design-method* layer on top — the patterns become event schemas, [[guardian-agents]] become
subscribers that veto events before they commit, and governance audit trails are the log itself.

## The file-format + linter rung (ESDM, 2026-07)

The focus area long had the *vision* of a model that is a spec legible to humans and agents alike
([[dilger-planning-like-excel-legible-to-human-and-ai]], [[dilger-is-code-still-the-source-of-truth]]),
agents that *author* models ([[fraktalio-event-modeler-connect-ai-agents-mcp]],
[[proophboard-skills-ai-agent-event-modeling]]), and even a YAML dialect for it
([[dilger-event-modeling-knowledge-hub-emlang|EmLang]]) — but no open, specified, tool-backed format.
[[thenativeweb|thenativeweb]]'s [[esdm-event-sourced-domain-modeling|ESDM]] fills that rung: an
**MIT-licensed YAML language + offline linter** for event-sourced domains, with "modeling with AI" as a
first-class use case ("YAML plain enough that LLMs read and write it directly; the fixed schema + named
vocabulary give them the constraints they need"). Two mechanisms make it agent-relevant beyond earlier
sources: (1) the model as **version-controlled files whose drift fails a PR check** — enforcement, not
documentation, echoing [[dilger-keep-command-handlers-pure|"enforce, don't just document"]]; and (2) a
**fixed, non-configurable linter** as a deterministic sensor ([[feedforward-and-feedback-controls]],
[[harness-engineering]]) — the same "give the agent a deterministic external sensor" instinct as
[[tornhill-cannot-trust-agent-codescene-mcp]]. It ships [[given-when-then|GWT]] as a validated extension
schema, making the agent's acceptance-gate artifact itself machine-checked. Contrast with the board+MCP
camp (Fraktalio/prooph): ESDM is **file-first and offline**, letting any LLM read/write the YAML
directly rather than authoring on a hosted board. Caveat: it models ES/DDD/CQRS *structure*, not the
Dymitruk timeline/swimlane method, and is vendor-authored and early.

**The persistence rung (2026-09-02).** [[dilger-git-as-primary-persistence-for-event-models]] makes
**git a primary store for the model, not an export**: one repository per board, branching supported,
under a "BYODS — bring your own datastore" design (Redis, S3, YAML, SharePoint all named), with
*"you can store your models in a Worm-Drive for auditability."* Two consequences for this page. **(1) It
collapses the file-first-vs-board+MCP framing entirely** — the board *is* files, so an agent can read
the model and its whole history with ordinary git tooling, and **model↔code drift becomes a diff between
two repos** rather than a bespoke check. Compare [[dilger-drawio-model-in-code]], where model-in-git was
right but raw XML gave the agent *"no framework to follow, no rules"*; this is that idea with a schema
and a platform behind it, and [[esdm-event-sourced-domain-modeling|ESDM]]'s file-first position reached
from the hosted-board side. **(2) Branching a *specification* is new**, and it is the natural pairing
for a fleet of agents claiming slices off one board
([[dilger-loop-engineering-never-argue-with-agent]]) — though nothing in the source says how a
two-dimensional board serialises for meaningful diffs, what happens when two agents diverge on the same
slice, or how branching interacts with the claim-lock. *(**VENDOR SELF-REPORT** — EM-Studio is Dilger's
own platform, and the git backend is **announced as being added, not reported in use**.)*

## What's solid vs. open

- **Externally supported (a ladder of increasing concreteness):** (1) agents map onto Event
  Modeling's user/processor roles ([[dymitruk-event-modeling-future-proof-agents]]); (2) AI and Event
  Modeling already interoperate in tooling ([[qlerify-event-modeling-tool-ai]]); (3) agents are being
  built to *practise* Event Modeling directly — [[prooph-board]] ships agent **Skills + an MCP server**
  teaching coding agents to create EM elements ([[proophboard-skills-ai-agent-event-modeling]]), and
  **[[fraktalio]]**'s Event Modeler now exposes an MCP endpoint where an agent authors the model *and
  generates Given-When-Then per command, including business exceptions*
  ([[fraktalio-event-modeler-connect-ai-agents-mcp]]) — a second independent vendor on this rung; and
  (4) **the event model now governs a multi-agent build** — [[john-wilger]]'s `agent-skills`
  ([[jwilger-agent-skills-event-modeling]], and the v4.1 capture [[jwilger-agent-skills-factory-pipeline]])
  makes the method's *output* (vertical slices + GWT scenarios) the machine-checkable contract for an
  autonomous "factory pipeline": GWT scenarios become the TDD acceptance gates (rejected unless they
  exercise an external boundary), the `event_model_root` is loaded as pre-implementation context, and the
  human/agent boundary follows a Conservative→Standard→Full [[autonomy-ladder]]. This is the **cleanest KB
  instance of the reversed direction of fit** — not an agent *modeled as* a user/processor and not an
  agent that *authors* the model, but the **event model as the upstream, human-authored spec that drives a
  whole [[software-factory|factory]] of coding agents** (slice = work-item, GWT = review-gate oracle). The
  closest shipping evidence to date. And (5) a **practitioner-evangelist** thread: [[martin-dilger]] (building
  [[eventmodelers-ai]]) argues the *why* from the requirements side — AI amplifies unclear requirements
  rather than fixing them, so the event model is the spec that constrains the agent
  ([[dilger-faros-ai-report-amplifies-unclear-requirements]], [[spec-driven-development]]); the model
  defines *where logic may live* and must be enforced because agents drift
  ([[dilger-keep-command-handlers-pure]]); an agent can even *bootstrap* the model from a running
  UI ([[dilger-automatic-domain-discovery-claude-code]], [[domain-discovery]]); and he now describes
  the model run as a **live spec** — a background agent building continuously from board edits, with a
  slice→"generate tests from the spec (the harness)"→implement→PR loop, optionally a modeling-agent→
  builder-agent "full autopilot" ([[dilger-model-is-a-living-spec-always-on-agent]];
  [[long-running-agents]], [[unattended-coding-agents]]). He has since crystallized this into a named
  **Event Modeling Agent Harness** ([[dilger-event-modeling-agent-harness]], 2026-06-17): a 24/7
  [[ralph-loop]] whose **unit of work is the EM slice** on a Draft→Ready→In Progress→Done board, with
  GWT scenarios as the BDD feedback backbone and cheap local models doing the coding once a
  "blue-print architecture" makes it "painting by numbers" — the most concrete statement yet of the
  [[agent-harness]] built *on* the method. He then **ships the implementation details**
  ([[dilger-local-llm-distributed-agent-setup-event-modeling]], 2026-07-02): 3× on-prem Asus GX10 running
  **Gemma4 / Qwen3.6:27B via Ollama**, 6–10 agents in [[ralph-loop|ralph-loops]] 24/7, and — the load-bearing
  mechanism — a **board-level claim-lock on the slice** ("Planned" → exactly one agent claims → "In
  Progress", locked) that makes parallel multi-agent work **collision-free without code-level
  coordination**, because [[vertical-slice-architecture|slices are decoupled by design]] ("no merge
  conflicts, no coupling hell"); move a slice "Done"→"Planned" and an agent reconciles code to spec. A real
  running instance of the DCB-style conditional-append guard the KB's own worked models only assumed. And his **80/20 framing** (2026-06-29) states the stakes
  bluntly: the harness + code are only ~20%, the other 80% is getting the requirements/business processes
  right — exactly the [[event-modeling]] half — so an event-modeled spec is what makes the agent harness
  pay off ([[dilger-harness-is-20-percent-requirements-are-80]]; cf. [[harness-engineering]]).
  Framing-rich but vendor-marketing, not independent evidence. **Direction of fit** now cuts both ways: agents that *author* the model
  (Fraktalio's MCP, Dilger's discovery) and the model that *governs* the agent (jwilger's gates,
  Dilger's slice loop) — together a closed authoring↔execution loop. He then names the **mechanism**
  that makes the model agent-usable ([[dilger-planning-like-excel-legible-to-human-and-ai]], 2026-07-09):
  an **Excel-like grid** gives every element a **cell-reference coordinate**, so the model becomes
  *addressable in both directions* — an agent can be instructed *("add a field in B3, adjust all
  dependents")* and can report back against the same handle *("there's a problem in B3…")*. Freeform
  whiteboards degrade and can't be addressed this way; the grid is his answer to "what makes a spec
  legible to a human and an AI at once" — a concrete refinement of the model-as-agent-spec claim (see
  [[ai-readable-code]]).
- **Supporting voices (2026-06-15):** [[adam-dymitruk]] now states the blunt *why* — AI was "trained on
  dysfunction," so agents are needed precisely to *assemble* best-practice systems against a spec, not
  to invent them ([[dymitruk-ai-trained-on-dysfunction-agents-are-a-must]]); he names
  [[martin-dilger]] and [[yordis-prieto]] as the practitioners doing it. And the **capability** angle:
  [[rico-fritzsche]]'s [[autonomous-domain-capabilities|RPU/CCC]] makes a
  [[business-capabilities|capability]] own its context/decision/consequences from recorded events — a
  natural, contracted **agent-ownership boundary** (an agent owns a capability, builds context from the
  log, decides, emits), reinforcing the "agent as user/processor on a swimlane" mapping. Both are
  framing, not worked models.
- **A practitioner-org adopter + a new open seam (2026-07-01):** [[christian-johansen]] of
  [[chronoshub|ChronosHub]] ([[johansen-is-it-safe-to-jump-em-conf-2026]], a reflection on the **Event
  Modeling Conference 2026**) reports a real org with **leadership buy-in** for an EM + [[event-sourcing|ES]]
  engineering strategy explicitly aimed at "the agentic future" — a rare adoption datapoint rather than
  vendor framing. It also opens a seam this concept hadn't tracked: **experience engineering × agents** —
  once the systems are built, how do you shape the *interaction/experience layer* so it works for **both
  humans and AI agents** at once? A layer *above* the system-design mapping on this page (and adjacent to
  the human/AI-legibility thread in [[dilger-planning-like-excel-legible-to-human-and-ai]] and
  [[ai-readable-code]]). No worked answer yet — flagged as an open direction. The same source frames EM's
  growth constraint as **narrative/leadership adoption**, not technique.
- **Vendor demo, not yet a published artifact (2025-10):** at the first Event Modeling Conference
  ([[dilger-first-event-modeling-conference-munich-recap]]), [[allard-buijze]]'s Day-2 keynote demoed
  the new **[[axoniq|AxonIQ]] platform turning Event Models into working code automatically** — the
  most concrete "model→code" instance the focus area has surfaced, though it's a staged vendor keynote,
  not an independent published worked model. The same recap adds two **modeling lessons** that bear on
  this concept: (a) **"the model is not the implementation"** — *"just because the event is in the Event
  Model doesn't mean it has to be in the code"* (drop, merge, or split events for engineering reasons);
  a useful tension against [[dilger-is-code-still-the-source-of-truth|Dilger's own "model is the source
  of truth"]] line (source-of-truth for *intent*, latitude for *realization*); and (b) the **two-model /
  "zoom-in" approach** — keep the main model high-level, spin a second zoom-in model for a complex
  automation slice — a direct answer to the recurring *"how do I model an Automation / where does the
  logic go?"* question that is exactly the agent-processor design problem.
- **Still in-house extrapolation:** the full construct-by-construct mapping onto the harness thread
  above. No *externally published* source yet gives a *worked* event model of a multi-agent/harness system —
  even jwilger's pipeline *consumes* an event model (`docs/event-model/`) it doesn't show. **The KB now
  has its own worked model** (2026-06-15): `outputs/worked-event-model-autonomous-coding-factory.md` —
  an **autonomous coding factory** (feature request → merged PR) modeled end-to-end with seven slices,
  six agent processors across role/capability swimlanes, GWT contracts, a guardian-veto subscriber, an
  autonomy-ladder Orchestrator, and a DCB-style conditional-append safety invariant. It's an
  *illustration*, internally consistent with the sources but untested against a running system — it
  closes the "no worked example at all" gap, not the "no independent real-world one" gap. **A second
  worked model** (`outputs/worked-event-model-customer-support-desk.md`) does the same for an
  **autonomous customer-support desk** ([[customer-support-agents]]) — triage → context (MCP) → draft →
  guardian/escalation → act+send → CSAT, with the same DCB guard ("nothing sent/executed without
  approval"). Together the two triangulate this concept from both flagship use cases ([[agentic-coding]]
  + [[customer-support-agents]]). A visual swimlane render of the coding-factory model lives at
  `outputs/worked-event-model-autonomous-coding-factory.mermaid`. (Companion: the notation primer
  `outputs/denoting-an-agent-in-an-event-model.md` — user/processor roles + cheat-sheet.)
- **The seam, inverted — event sourcing on the agent loop (2026-03-04).**
  [[nick-tune-event-sourced-claude-code-workflows]] models a Claude Code workflow as a state machine
  (DEVELOPING → REVIEWING → COMMITTING → RESPAWNING) and persists **only the events**, deriving state by
  replay in SQLite. The payoff is entirely observational: per-state dwell times, **rejection counts**
  (review failed) and **hook-denial counts** (the agent attempted something disallowed in that state),
  a journal enforced at ≥1 entry per iteration by hard blocks, and the events fed **back to Claude** to
  propose CLAUDE.md or system-prompt changes. His reading of one session — *"my agents spent 15 minutes
  in the RESPAWN state whereas they only spent 2 minutes actually building the feature"* — is an
  instrument reading from **one session of his own personal-project harness, and he says so**
  (**IMPRESSION NOT MEASUREMENT · NOT INDEPENDENT**). He scopes the value honestly: it pays off for
  autonomous loops, not for chatbot-style or hand-held sessions, and *"if we get to that point [where
  workflows just work], the observability and analysis doesn't provide any value."*

  **Why it matters to this page and why it does not close the gap.** This is *not* an event model of a
  multi-agent system in the Dymitruk sense — no swimlanes, no commands, no read models, no timeline
  notation — so the standing "wanted next" (a **worked event model of a harness**, using the method)
  stays open. What it *is*, is the first published system where the **agent loop's own history is the
  source of truth**, which makes it the nearest empirical cousin of this page's central mapping and the
  strongest evidence that treating agent runs as an event stream buys something concrete. Note also the
  boundary the same author draws: he instruments and automates the **loop** while doubting he can
  delegate the **domain model** at all ([[tune-no-rapport-with-a-model-you-didnt-code]],
  2026-08-28) — which is a direct challenge to the claim that a good
  enough DSL lets agents do the modelling work.
- **Adjacent cross-check (captured):** [[esaa-event-sourcing-for-autonomous-agents]] (arXiv, Feb 2026)
  gives a *worked* multi-agent system built on event *sourcing/CQRS* — agents emit JSON **intentions**,
  a deterministic orchestrator applies **effects** — which is strikingly close to Event Modeling's
  **command → event** flow and Automation pattern, even though it doesn't use the method or its
  notation. The nearest thing to a worked example, one substrate-level remove from this page's claim.
- **Wanted next:** a worked example using Event Modeling *the method* (Dymitruk long-form, a talk, or
  a paper); the broader academic formal/discrete-event agent-specification lineage (e.g. DEVS world
  models, "Formally Specifying the High-Level Behavior of LLM-Based Agents") as further cross-checks.

**The "Triplet" as the packaged operating model.** [[dilger-triplet-flexible-agent-enabled-architecture|Dilger's
"Triplet"]] (2026-07-26) names the assembled form of this design: Event Modeling (plan) + Vertical Slices
(structure) + Event Sourcing (store), used *in union*, marketed as a **"flexible, agent-enabled
architecture."** Its agent claim is the crisp economic version of this whole page's thesis — the same low
coupling that makes a system easy for humans to change makes it cheap for agents, because an agent working one
[[vertical-slice-architecture|slice]] "only needs that slice's context, the event log, and a precise model
instead of half the codebase," keeping context/token/review cost down and letting parallel agents add
throughput without collision (the structural precondition behind [[dilger-event-modeling-agent-harness]]).

**EM as the front half of Spec-Driven toolkits.** A newer direction of fit
([[dilger-spec-driven-tools-need-event-modeling-front-half]], 2026-08-02): rather than EM *governing* an
agent or *being authored* by one, the event model **feeds** the SDD toolchains (Spec-Kit / Spec-Kitty /
AWS Kiro) that otherwise "skip the digging" and jump to tech-stack + a premature domain model. Because the
Event Modeling Format is standardized, a skill/CLI (`eventmodelers export --spec-kitty`) turns the model
into the toolkit's task list — EM as the problem-understanding front half, an **interop bridge** rather
than a rival tool.

**A third direction of fit — agent *critiques* the model (Dilger, 2026-08).** Beyond agent-authors-model
and model-governs-agent, Dilger ships the agent as a **model reviewer**, working upstream of code on the
spec itself: the **`/wdyt` AI-skill** walks a board, challenges assumptions, and flags his
[[event-modeling-anti-patterns|"Shapes" anti-patterns]] ([[dilger-the-shapes-event-modeling-anti-patterns]]);
and a mooted **EM "linter"** grades a board's *structure* (not correctness) by having Claude Code compare it
against a curated reference catalog ([[dilger-event-model-structure-linter-reference-catalog]]). These are
model-level quality gates that sit *above* the code-level [[given-when-then|GWT]] gates. He also extends the
human/agent-legibility surface from structured coordinates to **freeform marks**: agents now **read** board
sketches (inside/outside a lasso, arrow direction) and, via [[model-context-protocol|MCP]] tools, **draw
back** — sketches, arrows, question marks — turning visual annotation into a two-way channel
([[dilger-agentic-collaboration-freeform-drawings]]). And his "only two patterns" reduction
([[dilger-99-percent-software-boring-two-patterns]]) supplies the *why agents fit* in one line: the
repetitive State-change/State-view shape gives an agent "tight guardrails … instead of an open-ended blank
page."

**Why the model, not the LLM, is the asset (Dymitruk, 2026-08-09).** [[dymitruk-ai-melts-barrier-event-modeling-is-the-map|Dymitruk]]
states the durable-asset case bluntly: code is "a black box" with "no standard way to see what's going on
inside," but an event model is a **map** that gives control "no AI tooling gives you" — so *which LLM you
use* "doesn't matter that much" ("picking up pennies in front of a steamroller"). The LLM-agnostic form of
the model-as-source-of-truth thesis, and a direct counter to [[yordis-prieto-code-is-the-ultimate-diagram|Prieto's
code-first view]].

**The format question, split out (2026-08).** The surface-and-format half of this concept has grown large
enough to live on its own page: [[agent-readable-model-artifacts]]. The short version — what makes a model
usable by an agent is **addressability** (a shared handle to instruct and report against), and the ladder
runs freeform whiteboard → raw XML in git → grid coordinates → board-via-MCP → linted file format →
**export-on-demand in whatever format the agent asks for**. That last rung arrived on 2026-08-13, when
[[eventmodelers-ai]] began exporting any Event Model to [[esdm-event-sourced-domain-modeling|ESDM]] over
UI/API/MCP/CLI — "so your agent can request any modeled slice or chapter in the format it needs" — with a
joint [[golo-roden|Roden]]–Dilger extension announced to carry EM's **timeline** into ESDM
([[dilger-eventmodelers-supports-esdm-export]]). This closes the KB's standing "ESDM/EmLang materialization"
gap and collapses the file-first-vs-board+MCP framing this page used to draw. A companion datapoint:
**screen markers** — region-scoped "what matters right now" annotations that agents read, validate, and
build UI from ([[dilger-highlighting-markers-give-context-to-agents]]).

**Two caveats landing in the same week (2026-08).** The concept's optimism now has counter-weight from
both sides. From the *verification* side, [[birgitta-bockeler]]'s eval found that making an agent do TDD
**inside its own loop** bought no quality and 3–8.5× the tokens, because agent-authored micro-tests
suppress up-front design and a self-confirmed red test proves only that the agent saw a failure, "not that
the failure was for the right reason" ([[bockeler-tdd-inside-the-agent-loop]]). Read carefully this
*supports* the [[given-when-then|GWT]] claim rather than undermining it — her target is the agent inventing
its own tests, not an externally authored acceptance spec — but it puts a real constraint on the
"generate tests from the model, let the agent iterate" loop: the spec must come from outside the loop, and
the trustworthy signals are outcome sensors ([[mutation-testing]]), not process instructions. From the
*human* side, [[martin-dilger]] names the failure mode of his own thesis: teams that "stop solving problems
and just describe them, and then hand it to AI and hope it figures out the solution… that's checking out
before it gets interesting" ([[dilger-describing-without-solving-burns-you-out]]). Both converge on the
same question — **where does the human stay in the loop** — and answer it in the same place: own the
problem and the acceptance criteria, delegate the process.

## The model as *rubric*, not just as spec (Dilger, 2026-08) — the missing evidence

Everything above uses the event model as an **input**: a spec the agent is handed, a contract it must
satisfy, a board whose slices it claims. Dilger's late-August self-training loop uses it as an
**output check**, and that is a different and previously unevidenced claim
([[dilger-one-million-tokens-self-training-modeling-agent]], [[dilger-modeling-agent-improved-by-learning-loop]]).

The setup: a corpus of hand-crafted "well crafted" event models; a realistic requirement set; the agent
models it; the result is **structurally diffed** against the corpus — "Are Chapters laid out the same
way? Are Read Models structured in a similar way? How are given / when / thens structured?" — and the
agent then **rewrites its own skill files** from the differences and re-models, comparing against both
the previous round and the corpus. Local hardware, QWEN3.7:27b, >1M tokens overnight.

Why this closes a gap the page has carried since June:

- **It supplies the mechanism behind "the model makes agent output checkable."** The page has asserted
  this repeatedly (GWT as acceptance gate, the model as machine-checkable contract). Those are checks
  that the *code* matches the model. This is a check that a *model* matches good models — possible only
  because the model has a schema. You cannot structurally diff two Markdown specs, which is precisely
  [[model-as-code-vs-model-as-language]]'s live question.
- **It extracts tacit method knowledge.** All three of the loop's discoveries — storylines over plain GWT
  for Read Models on Automations ([[dilger-todo-lists-storylines-one-scenario]]), linked elements bridging
  events across chapters, Read-Model copies instead of back arrows — are conventions Dilger holds but had
  not stated as rules. The corpus carried method knowledge the skill files did not. That is a partial
  answer to [[addyosmani-earning-taste-and-judgment|"taste is the ungradeable residue"]]: a slice of taste
  turned out to be gradeable once it was embodied in structured artifacts.
- **The consumer shapes the model.** The agent learned to break screens into functional blocks with
  dedicated Read Models *because* it makes UI generation easier — [[agent-readable-model-artifacts]]'
  argument observed from the inside.

**What it does not close.** The lint pass's caveat holds: this is a system that *produces* event models,
not a multi-agent system that *is* one, so the KB's standing open question — a worked event model **of** a
harness — remains open. This is the nearest thing yet, not the thing. The evidence is also self-reported
by the platform's vendor, with no held-out set described and "improvement" defined as convergence on the
author's own conventions.

And the loop surfaced its own limit: roughly every fifth iteration degrades badly as the model nears its
token budget ([[token-budget-quality-cliff]]). Be careful with the inference here, because it is tempting
and he does not license it: **he does not say the rubric is what caught the bad iterations** — by his own
account he noticed them while watching runs, then dug into the reasoning traces. What holds is the
structural version: a loop with no rubric has nothing that *would* catch a bad fifth iteration, because
the artifact looks finished. That is still the strongest practical argument on this page for
model-as-rubric, but it is an argument from the failure's shape, not from his account of finding it.

## Agents modelling *with* you, and the over-specification failure (Ep 47, date unresolved)

[[dilger-podcast-episode-47-agentic-modeling-audit-trails]] pushes two rungs of this page forward and
puts a real limit on a third.

> **⚠ The date of this source is unresolved and must stay that way.** The page carries no publication
> date in HTML, metadata or body. Ep 47 is **absent from the podcast RSS feed and from
> podcast.eventmodeling.org**, both of which still end at **Ep 46 (2026-04-26/27)**, so it post-dates
> 2026-04-27 and nothing further can be established. It announces [[golo-roden]] for an *"already
> sold-out"* conference and the site banner reads *"September cohort sold out"*. **It may well be a
> channel prior sweeps never polled** (`eventmodelers.ai/docs/podcast` is a separate, more current index
> than the `.org` one) **rather than a genuinely new item.** Also **show-notes level, not verified
> against audio**, and **VENDOR SELF-REPORT** — the platform and the skill are Dilger's products.

**Agents as co-modellers.** Dilger ran a Claude Code instance and a **Hermes** agent modelling alongside
him simultaneously, adding slices and comments, and reports it *"was indistinguishable from modeling
with humans"* — **IMPRESSION NOT MEASUREMENT**, and a felt comparison rather than an evaluation, but the
furthest the agent-authors-the-model rung has gone.

**The `/wdyt` skill, worked.** The agent reads the slices and **posts clarifying-question comments on
them**: *"He commented on the slice and asked: well, what happens if a user clicks this twice? What
should be the behavior? … And this is perfectly valid — a perfectly valid question."* Note the shape:
the agent's output is a **question on the artifact**, not an edit to it — a model-level review gate
above the code-level [[given-when-then|GWT]] gates.

**And the failure, which is the transferable finding.** The first version *"flooded the model with 100
comments inventing hypothetical gaps."* The fix was a restriction: *"don't just look at what is there —
don't comment on something because it's not specified. Just look at what is there and make sense of it,
then give me comments. And then it got significantly better."* [[adam-dymitruk]] adds why it matters
more here than in code review: an over-eager agent flooding a GWT list with edge cases *"can make a
simple slice look far more complex than it really is, since event modeling is visual"* — so the noise
does not merely waste attention, it **degrades the artifact's primary affordance**. The method's own
answer predates the tooling: *"event modeling already solves the 'infinite possibility tree' problem:
draw a few representative example paths and trust the implementer to infer the rest."*

**What this costs the model-as-rubric optimism above.** The rubric section argues a schema'd model makes
agent output gradeable. This shows the converse risk: **an agent pointed at a spec can inflate it**, and
the inflation is invisible to a structural diff (a bloated slice is still well-formed). It is the same
mechanism [[bockeler-tdd-inside-the-agent-loop|Böckeler]] found one altitude down — an agent inventing
its own acceptance criteria — and the same remedy applies: **the criteria must come from outside the
loop.** See [[event-modeling-anti-patterns]] for the anti-pattern this creates.

## The sharpest external challenge: whose model is it? (Ng, 2026-03)

[[ng-spec-driven-development-is-waterfall-in-markdown]] attacks document-first
[[spec-driven-development|SDD]] toolkits, not Event Modeling — but one of its arguments lands squarely on
this page, and the KB should not let it pass unexamined. Ng's claim is that a written spec **flattens a
cross-functional set of mental models into a single voice — the author's**: "The designer thinks in user
flows. DevOps thinks in deployment constraints. Product thinks in business outcomes." None of them
will ever open the artifact you feed the agent. Hence "a contract between you and the LLM that nobody
else signed."

**Why this is the strongest form of the objection for this page.** Every claim here about the model being
a better agent input than a prompt or a markdown spec rests on a property of the artifact — it is visual,
timeline-ordered, linted, MCP-addressable. Ng's objection is about a property of the *process*: an
artifact is only multi-perspective if multiple perspectives were actually in the room when it was built.
An event model authored solo by an architect and then handed to agents is exactly the object he is
describing, whatever its file format.

**What the KB can answer, and what it can't.** Event Modeling's standing answer is that it is a
*facilitated workshop method* — the model is built with stakeholders, in their vocabulary, and stays live
as they change it ([[dilger-model-is-a-living-spec-always-on-agent]],
[[dilger-user-stories-need-event-modeling-framework]]). And Ng's complaint is close to
[[dilger-spec-driven-tools-need-event-modeling-front-half|Dilger's own]] verdict on the same toolkits —
Dilger's phrase is that they *"skip the digging"*; Ng's is that they produce documents that flatten the
people who hold the constraints — so the two are closer allies
than the headline suggests, and the multi-perspective work
([[dilger-agentic-collaboration-freeform-drawings]], screen markers, prooph board's wireframe links) is
precisely an attempt to keep more than one lens attached to one model. What the KB **cannot** currently
show is evidence that modelling sessions resist the flattening in practice — no captured source measures
stakeholder participation in a model that later drove agents. That is now a named gap on this page, and
Ng's [[decision-trace]] is the rival proposal to beat: it keeps the multi-perspective input as a *record
of conversation* instead of trying to encode it in a single artifact.

**What this batch adds to the answer (2026-09-04), and it is partial in a specific way.** Three captures
bear directly on the flattening objection. [[dilger-only-engineers-care-about-consistent-systems]]
reaches **Ng's own diagnosis from the opposite camp** — every hop between end user and engineer reshapes
the requirement, and *"now with AI - we are just adding one more hop to the chain. Engineers talking to
AI, writing tons of markdown.. one more handover"* — and prescribes calling the end user and then
*"invit[ing] them to a short Event Modeling Session. Show them what you planned, show them the screens
you sketched."* [[dilger-ux-as-first-class-in-spec-driven-development]] and
[[dilger-ui-only-interactions-filtering]] supply the mechanism: **the screen is the artifact a
non-developer can react to**, and it is in the model rather than derived from it (see
[[screens-as-specification]]). Ep 47 adds Dymitruk's blunt version: *"all the arguments about not having
screens and design sessions is just gatekeeping by architect wannabes."*

That is a real answer to *"nobody will open a `.specify` folder"* — a sketched screen needs no folder.
It is **not** an answer to *"nobody else signed it"*: the KB still holds **no captured source measuring
stakeholder participation in a model that later drove agents**, and every one of these sources is
[[martin-dilger]] on his own platform (**VENDOR SELF-REPORT**). The gap named on this page stands; what
changes is that the camp now has a stated mechanism rather than only a claim about workshop practice.

**And a second external challenge, sharper for this page than Ng's.**
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill's]] requirements-explosion argument
says each specified requirement spawns *tens of implicit design requirements* that cannot be known up
front, because **implementation is the discovery process** — so the acceptance-gate story on this page
(GWT scenarios as the machine-checkable contract an agent must satisfy) is checking the small share of
decisions that were specifiable. His obstacle (3) closes the obvious escape: enrich the model until it
resolves the implicit decisions and *"the moment a model becomes the implementation, it ceases to be a
good model."* Note this is **not** the waterfall objection — he explicitly declines that — and it is
aimed at strong-form [[spec-driven-development|SDD]], which is where this page sits. The KB has no
answer to it, and no captured source even attempts one.

_Sources: [[dymitruk-event-modeling-future-proof-agents]] · [[qlerify-event-modeling-tool-ai]] · [[proophboard-skills-ai-agent-event-modeling]] · [[fraktalio-event-modeler-connect-ai-agents-mcp]] · [[jwilger-agent-skills-event-modeling]] · [[jwilger-agent-skills-factory-pipeline]] · [[dilger-spec-driven-development-applied]] · [[dilger-faros-ai-report-amplifies-unclear-requirements]] · [[dilger-keep-command-handlers-pure]] · [[dilger-automatic-domain-discovery-claude-code]] · [[dilger-model-is-a-living-spec-always-on-agent]] · [[dilger-event-modeling-agent-harness]] · [[dilger-planning-like-excel-legible-to-human-and-ai]] · [[eventmodeling-what-is-event-modeling]] · [[anthropic-effective-harnesses-long-running-agents]] · [[stripe-minions-one-shot-coding-agents]] · [[dilger-triplet-flexible-agent-enabled-architecture]] · [[dilger-spec-driven-tools-need-event-modeling-front-half]] · [[dilger-the-shapes-event-modeling-anti-patterns]] · [[dilger-agentic-collaboration-freeform-drawings]] · [[dilger-event-model-structure-linter-reference-catalog]] · [[dilger-99-percent-software-boring-two-patterns]] · [[dymitruk-ai-melts-barrier-event-modeling-is-the-map]] · [[dilger-eventmodelers-supports-esdm-export]] · [[dilger-highlighting-markers-give-context-to-agents]] · [[dilger-describing-without-solving-burns-you-out]] · [[bockeler-tdd-inside-the-agent-loop]] · [[ng-spec-driven-development-is-waterfall-in-markdown]] · [[dilger-one-million-tokens-self-training-modeling-agent]] · [[dilger-modeling-agent-improved-by-learning-loop]] · [[dilger-todo-lists-storylines-one-scenario]] · [[dilger-podcast-episode-47-agentic-modeling-audit-trails]] · [[nick-tune-event-sourced-claude-code-workflows]] · [[dilger-git-as-primary-persistence-for-event-models]] · [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]] · [[dilger-ux-as-first-class-in-spec-driven-development]] · [[dilger-only-engineers-care-about-consistent-systems]] · [[dilger-ui-only-interactions-filtering]] · [[dilger-loop-engineering-never-argue-with-agent]]._
