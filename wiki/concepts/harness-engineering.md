---
title: Harness Engineering
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [dymitruk-move-prompts-into-scripts-deterministic, fowler-bockeler-harness-engineering, openai-harness-engineering-codex, anthropic-effective-harnesses-long-running-agents, langchain-anatomy-of-an-agent-harness, firecrawl-what-is-an-agent-harness, hashimoto-my-ai-adoption-journey, stripe-minions-one-shot-coding-agents, fowler-bockeler-maintainability-sensors, dilger-harness-is-20-percent-requirements-are-80, martinfowler-prince-building-reliable-agentic-ai-systems, tornhill-cannot-trust-agent-codescene-mcp, ahe-agentic-harness-engineering, guo-survey-question-answering-to-task-completion-harness-design, ning-code-as-agent-harness, wang-rethinking-evaluation-of-harness-evolution-for-agents, harnessx-composable-adaptive-evolvable-agent-harness-foundry, harnessforge-joint-harness-and-policy-evolution, sbco-verifier-grounded-harness-optimization, evo-bench-can-language-models-improve-agent-harness, mcateer-evolution-of-the-agent-harness, graph-engineering-era-of-llm-agents-system-intelligence, breunig-fable-and-the-end-of-the-free-lunch, breunig-harnesses-are-situated-agents, morris-humans-and-agents-in-software-engineering-loops, macmanus-schott-react-for-agents-flue-meta-harness, edwards-alexander-an-accidental-blackboard, breunig-who-taught-the-models-to-do-that, miller-ai-assisted-production-support-with-critterwatch, willison-codex-bundles-libreoffice, willison-claudes-new-system-prompt, willison-understanding-chatgpt-work, miracle-my-loop-engineering-workflow, addyosmani-code-agent-orchestra]
tags: [harness-engineering, agentic-ai, reliability, coding-agents]
---

# Harness Engineering

**Hub page.** Harness engineering is the practice of building and continuously improving the
[[agent-harness]] — everything around an LLM except the model itself — so that a non-deterministic
model does reliable work. Its defining stance, shared across sources: **treat every agent failure
as a system problem to permanently fix, not a prompt to retry** ([[mitchell-hashimoto]], via
[[firecrawl-what-is-an-agent-harness]]). When the agent makes a mistake, you engineer the
environment so it (mechanically) can't make that mistake again.

## Why it emerged

The term spread in early 2026: [[mitchell-hashimoto]] named it in
[[hashimoto-my-ai-adoption-journey|his adoption essay]] (Feb 5) — "anytime you find an agent makes a
mistake, you take the time to engineer a solution such that the agent never makes that mistake again"
— [[openai]] published a flagship case study days later, and
[[birgitta-bockeler]]/[[thoughtworks]] gave it a mental model. It names something practitioners were
already doing — the scaffolding that turns a stateless model into a
[[long-running-agents|long-running agent]]. As [[langchain]]'s Harrison Chase argues, better models
*expand* what harnesses must do rather than shrinking them (Claude Code is 512k+ LOC and growing).
The opposite trend claim is also in the KB — [[mcateer-evolution-of-the-agent-harness|McAteer's]]
**train → absorb → shed** account, where progress is measured by how much harness you get to *delete*
([[harness-absorption]]). Both can be true and the wiki does not pick.

[[mitchell-hashimoto|Hashimoto]]'s two concrete forms set the template: (1) **better implicit
prompting** via AGENTS.md (each line derived from an observed bad behavior); (2) **actual programmed
tools** (screenshot scripts, filtered test runners) that let the agent verify itself.

## The economic argument — "the end of the free lunch" ([[breunig-fable-and-the-end-of-the-free-lunch|Breunig, 2026-08-23]])

Every other source on this page justifies harness work on **reliability** grounds. Breunig supplies an
orthogonal argument: **the harness is what lets a cheaper model do the work.**

The analogy: under Moore's Law it made no sense to ruthlessly optimize code, because *"in 18 months, a CPU
would arrive that would double your performance"* (Herb Sutter's **"free lunch"**). When single-threaded
performance stagnated, *"we suddenly had to think about parallelization, architecture, memory locality…
**We had to think about what work went where.**"* His claim is that model pricing crossed the same
threshold in Aug 2026: *"Prior to Fable, it felt silly to waste too much time improving your coding
harness or context strategies. A new model would arrive at the same price (or cheaper!) and paper over
most of your problems."* Now: *"**So we started to think about what work went where.**"*

Two consequences for this page:

- **Model routing by cost/capability becomes a first-class harness concern**, not an afterthought. His own
  pattern is a spec-shaped handoff: *"I frequently chat with Fable to interrogate and shape a design,
  before handing off a brief to GLM."* The same practice appears as a committed artifact in
  [[addyosmani-code-agent-orchestra|Osmani's]] `MODEL_ROUTING.md` (planning → cheaper model,
  implementation → Sonnet/Opus/Codex, review → a dedicated security model) and as a standing instruction
  in [[miracle-my-loop-engineering-workflow|Miracle's]] commissions (*"Subagents default to the cheaper
  model tier; spend the expensive one on the critical path"*).
- **He pre-answers the deflation objection.** *"I get pushback that falling inference prices will
  eventually bring us back to sending everything through the largest models. But I'm not so sure: **those
  same gains will benefit the K3s and Qwens**, and as we continue to develop better harnesses it will be
  easier to provide weaker (but still great) models with sufficient context to perform well."* And a
  second, non-price lock-in: *"Fable's access controls, dynamic degradation, and required data retention
  spooked enough companies (and countries!) into thinking about **where they send their traces and where
  they get their tokens**"* — so routing is also a **data-governance and jurisdiction** decision, which
  makes it durable even if the price argument weakens.

**This is the sharpest available statement of the KB's recurring "the environment substitutes for model
capability" thesis** — cf. [[tornhill-why-human-level-ai-wont-be-enough]],
[[borg-tornhill-code-for-machines-not-just-humans]] (peer-reviewed: code health predicts refactoring
correctness) and [[tornhill-codescene-unhealthy-code-agentic-token-cost]] (a vendor claim: unhealthy code
raises token spend 35–45%). It is also the best argument in the KB for the
[[event-modeling]]/[[given-when-then]] seam: **a well-specified slice with its GWT is exactly the
"sufficient context" that lets a weaker model execute a brief** — cf.
[[dilger-harness-is-20-percent-requirements-are-80]].

*(A 540-word blog post. **No measurement**: the price ratios ("roughly 1/9th the cost", "~1/5th the cost
of Opus 5") are asserted with no source, and the quality comparison is an explicit shrug — *"Is GLM 1/9th
the quality of Fable? Perhaps, for certain classes of tasks. But for most rote coding it's more than
sufficient"* — with no benchmark and no definition of "rote." Every model name and ratio is date-bound to
Aug 2026. **Do not let this become "harness work is now proven worthwhile"** — the claim is that the
*incentive* changed, on one author's read of one month's pricing.)*

## The mental model ([[birgitta-bockeler|Böckeler]])

Two control directions × two execution types (see [[feedforward-and-feedback-controls]]):

- **Guides (feedforward)** steer *before* the agent acts; **Sensors (feedback)** let it
  self-correct *after*.
- **Computational** controls are deterministic/fast/cheap (tests, linters, type checkers);
  **Inferential** controls use an LLM (AI review, "LLM as judge") — richer but slower and
  non-deterministic.

The human's job is the **steering loop**: when an issue recurs, improve the controls. Three
regulation categories — *maintainability* (easiest), *architecture fitness*, and *behaviour*
(hardest, still unsolved). Not every codebase is equally **harnessable** ("ambient affordances":
strong typing, clear module boundaries, boring frameworks).

[[fowler-bockeler-maintainability-sensors|Böckeler's follow-up field report]] supplies the first
worked example of the **maintainability** category: computational sensors (ESLint,
`dependency-cruiser`) work well at the file/function level — especially with custom messages as
self-correction guidance and threshold-raising over binary suppression — but cross-file modularity
needs an **inferential** "garbage-collection" review, and **[[mutation-testing]]** is what catches
the coverage-illusion once testing is left to AI. Left unmanaged, the agent **compounds inadvertent
technical debt**.

## The operational test — in the loop vs on the loop ([[morris-humans-and-agents-in-software-engineering-loops|Morris, 2026-03-04]])

The crispest test in the KB for whether you are actually doing harness engineering:
*"**The difference between in the loop and on the loop is most visible in what we do when we're not
satisfied with what the agent produces**, including an intermediate artefact. The 'in the loop' way is to
fix the artefact, whether by directly editing it, or by telling the agent to make the correction we want.
**The 'on the loop' way is to change the harness that produced the artefact** so it produces the results
we want."*

Morris also defines the harness **from the loop side**, which is the inverse of how
[[loop-engineering]] currently frames the layering: *"The collection of specifications, quality checks,
and workflow guidance that control different levels of loops inside the how loop **is** the agent's
harness. The emerging practice of building and maintaining these harnesses, Harness Engineering, **is how
humans work on the loop**."* (See the layering dispute section on [[loop-engineering]].) He notes the same
relocation has a third name — the **"middle loop"**, from The Future of Software Development Retreat.

Two more contributions:

- **Why internal quality still matters when no human reads the code** — argued on *external* grounds:
  *"a cleanly-designed, well-structured codebase has externally important benefits over a messy codebase.
  **When LLMs can more quickly understand and modify the code they work faster and spiral less.** We do
  care about the time and cost of building the systems we need."* Internal quality is instrumental, and
  the instrument is now the agent — cf. [[ai-readable-code]],
  [[borg-tornhill-code-for-machines-not-just-humans]].
- **The agentic flywheel**, four months before the KB's other statements of it: humans direct **agents**
  to improve the harness, fed by a **signal-enrichment ladder** — start with the harness's existing tests
  and evals, then *"pipeline stages that measure performance and validate failure scenarios,"* then
  *"operational data from production, user journey logs, and commercial results."* *"What we have now is
  an agent harness that generates recommendations for improving itself."* With a staged autonomy path:
  interactive review → recommendations filed **into the product backlog** → agents **scoring their own
  recommendations** (risks, costs, benefits) with **auto-approval above a threshold** — which is the
  grader-leak hazard adopted as a deliberate design choice. He concedes where it lands: *"At some point
  this might look a lot like humans out of the loop, old-school vibe coding."*

**Provenance note for this page.** [[harness-engineering]] is a **Thoughtworks-coined** term, and four of
this page's primaries are Thoughtworks authors publishing in Thoughtworks' own *"Exploring Gen AI"* series
on martinfowler.com: [[fowler-bockeler-harness-engineering]], [[fowler-bockeler-maintainability-sensors]],
[[bockeler-tdd-inside-the-agent-loop]], and now
[[morris-humans-and-agents-in-software-engineering-loops]] and
[[edwards-alexander-an-accidental-blackboard]]. **NOT INDEPENDENT** — that material is the same house
arguing for its own term, and should not be counted as external corroboration for it. (This does not
discount it: Böckeler's TDD study remains the KB's only controlled negative eval in this area.)

*(Morris's piece has **no data, no case study and no worked example** — five conceptual diagrams and an
argument, with the flywheel written in the future tense. Its one empirical gesture — that mixed AI
productivity results *"may be at least partly"* explained by review overhead — names no study. Its
footnote is a useful correction to the KB's own usage: *"These days 'ralph loop' is often used
colloquially to mean just firing up a bunch of agents and leaving them to keep looping… But as originally
described the operator plays an important role in steering agents as they ralph."*)*

## How it shows up in practice

- **Repository as system of record** ([[openai-harness-engineering-codex]]): a ~100-line AGENTS.md
  *table of contents* over a structured `docs/` tree (**progressive disclosure**), custom linters
  whose error messages inject remediation instructions, and "garbage-collection" agents that fix
  drift. The goal is **[[agent-legibility]]** — "what the agent can't see doesn't exist."
- **Initializer + coding-agent structure** ([[anthropic-effective-harnesses-long-running-agents]]):
  feature lists (JSON), progress files, git, `init.sh`, and end-to-end self-verification.
- **Core primitives** ([[langchain-anatomy-of-an-agent-harness]]): filesystem, bash/sandbox,
  memory, compaction, [[ralph-loop]]s.
- **Shift-left feedback at scale** ([[stripe-minions-one-shot-coding-agents]]): heuristic <5s
  pre-push lints + selective CI over millions of tests with autofixes, capped at "often one, at most
  two" CI runs — powering [[unattended-coding-agents]] (1,000+ merged PRs/week, *Stripe's own figure*).
- **Production enterprise harness** ([[martinfowler-prince-building-reliable-agentic-ai-systems]],
  Bayer/Thoughtworks): a LangGraph control layer that bounds which agent can act, which tools it may
  use, where the workflow pauses, how failures retry, and how **state persists so a failed run resumes
  from the failed node** — plus cross-provider **LLM fallbacks**, three reflection loops, and
  Langfuse/RAGAS evals. A worked, regulated-domain instance of "engineer the context *and* the harness."
- **Deterministic external sensors over LLM self-review** ([[tornhill-cannot-trust-agent-codescene-mcp]]):
  an agent can't reliably assess its own code health, so give it a *computational* sensor (CodeScene
  [[model-context-protocol|MCP]]) as an external source of truth — the [[feedforward-and-feedback-controls|sensor]]
  argument applied to [[ai-readable-code]].
- **The harness as a self-evolving surface** ([[ahe-agentic-harness-engineering|AHE, Lin et al. 2026]]):
  the manual "inspect trajectories → revise prompts/tools/middleware" loop, **automated**. An evolution
  agent rewrites a decoupled **seven-component** harness (system prompt, tool description, tool
  implementation, middleware, skill, sub-agent config, long-term memory) with the base model frozen,
  lifting Terminal-Bench 2 pass@1 69.7% → 77.0% and beating the hand-built Codex-CLI harness
  (*arXiv **preprint**, not peer-reviewed — and **this gain is contested, not settled**: see the next
  bullet and [[harness-evolution]]*). Empirically
  the gain lives in **tools, middleware, and memory — not the system prompt** (prompt-only regressed),
  refining which harness surfaces actually carry reliability. This is [[loop-engineering|loop engineering's]]
  hill-climbing loop applied *to the harness itself*.
- **…and the field policing itself** ([[wang-rethinking-evaluation-of-harness-evolution-for-agents|Wang et al. 2026]]):
  the gain above is **contested, not settled**. Automatic harness evolution is *itself* an iterative search over
  candidate harnesses, so — the argument runs — it must be compared against simple task-level search /
  test-time-scaling baselines under **matched feedback and inference budgets** before "the harness got better"
  beats "we spent more inference"; and because these methods search against the benchmark they then report on,
  the gains "risk overfitting to that specific task set." On **Terminal-Bench 2.1** with GPT-5.4 and Claude
  Opus 4.6 they find harness evolution "does not consistently outperform simple test-time scaling methods and
  exhibits limited generalization" *(arXiv preprint, not peer-reviewed — as are AHE and every method paper it
  critiques)*. AHE's protocol is inside that critique's scope, so **cite 69.7% → 77.0% with the dispute
  attached, every time**. Note the unresolved counter-tension: Wang et al. test frontier bases, where AHE
  itself predicts the least headroom (its largest gains were on its *weakest* bases). Neither side has
  answered the other on the other's terms. See [[harness-evolution]].

## Tool design is harness engineering — two rules from Sept 2026

**Rule 1: a tool with no skill is an under-leveraged tool.** [[jeremy-miller]] states it as a standing
internal rule at JasperFx: *"any time CritterWatch exposes new information through an MCP tool, the paired
skill work ships with it"*, because *"a pile of tools doesn't make an agent good at operations — an agent
also needs to know the discipline"* ([[miller-ai-assisted-production-support-with-critterwatch]] —
**VENDOR SELF-REPORT**, a paid product post). The paired skill teaches the *loop* (summarize → query → act,
in that order, ids flowing through) rather than listing the tools. The same pairing is visible from the
outside in OpenAI's runtime: bundled binaries plus *"skills which tell Codex how to find and use those
binaries"* ([[willison-codex-bundles-libreoffice]]).

**Rule 2: make the tool unable to report an ambiguous result as an answer.** CritterWatch's dead-letter
reads fan out over every physical message store a service owns and return `databasesAnnounced` vs
`databasesAnswered` plus a `partial` flag, and the paired skill enforces: *"an empty result with
`partial: true` means some stores did not report — **never answer 'the queue is empty'**."* The rule exists
*"because of a real production failure mode where a console rendered 'no dead letters found' over a queue
quietly holding 42 of them."* This is a [[feedforward-and-feedback-controls]] guide implemented **in the
tool's return contract** rather than in a prompt or a review step — the strongest instance in the KB of
Hashimoto's stance ("engineer it so the agent can't make that mistake again") applied to a tool's *schema*
rather than to the codebase. It generalizes well beyond .NET: any fan-out read an agent will summarize
needs to distinguish *no data* from *no answer*.

**Caveat on both rules:** the source is a vendor demo over a manufactured incident, with nothing measured.
The rules are design lessons, not evidence that agent-run operations works.

## It is a research field now, not three candidate papers (2026-09-04)

The KB's watch config treated harness optimisation as a handful of named candidate papers. The evidence says
otherwise, and it is not close. **All of it is preprint evidence — arXiv is not peer review — but the *shape*
of a literature does not depend on peer review:**

- **Two independent surveys 27 days apart, disjoint author sets**, both written to organise this literature (Ning et al. submitted 2026-05-18, Guo et al. 2026-06-14 — Ning is the earlier of the two):
  [[guo-survey-question-answering-to-task-completion-harness-design|Guo et al. (arXiv:2606.20683, 17 authors,
  CityU HK / Sydney / Peking / TokenRhythm)]] and [[ning-code-as-agent-harness|Ning et al. (arXiv:2605.18747,
  42 authors, UIUC / Meta / Stanford)]]. A topic does not attract two surveys unless there is a corpus. **Note
  the correction: Ning et al. is a *survey*, not the method paper the config assumed.**
- **A shared decomposition vocabulary recurring across groups with no common authors, in three countries** —
  harness as prompts + tools + memory + control flow; traces as the optimisation substrate; an evolution agent;
  governed mutation. Ning et al. give that last pattern its own subsections (§3.5.1–3.5.3: "Deep Telemetry as
  the Optimization Substrate", "The Evolution Agent", "Governed Harness Mutation") — i.e. AHE's pattern
  recognised as a *category*, independently.
- **Method plurality on one problem — four distinct bets, four groups:** observability over decoupled files
  ([[ahe-agentic-harness-engineering|AHE]]), algebraic composition of typed primitives
  ([[harnessx-composable-adaptive-evolvable-agent-harness-foundry|HarnessX]]), harness–policy co-evolution
  ([[harnessforge-joint-harness-and-policy-evolution|HarnessForge]]), and cheap verifier-grounded
  self-supervision ([[sbco-verifier-grounded-harness-optimization|SBCO]]). **HarnessX's +14.5% and
  HarnessForge's +12.0% are contested claims, not settled gains — cite them with the dispute above
  attached, every time ([[harness-evolution]]).**
- **A shared benchmark culture:** Terminal-Bench 2 / 2.1, SWE-bench Verified, GAIA, ALFWorld, WebShop,
  tau^3-Bench, WebArena — plus a purpose-built instrument,
  [[evo-bench-can-language-models-improve-agent-harness|Evo-Bench]].
- **Internal methodological policing**, which is the decisive marker:
  [[wang-rethinking-evaluation-of-harness-evolution-for-agents|Wang et al.]] attack the evaluation protocol the
  rest of the cluster shares, with public code. Fields critique themselves; collections of papers do not.

Two of those surveys also place this page on a ladder. Guo et al.: **prompt engineering → workflows and
context engineering → harness engineering → agent-native training and co-evolution**, where harness
engineering is the rung that "**closes the loop**" (context engineering "remains fundamentally
**feedforward**" — the [[feedforward-and-feedback-controls]] distinction, arrived at independently).
[[graph-engineering-era-of-llm-agents-system-intelligence|Feng et al. (arXiv:2608.21156)]] agree on the first
three rungs and then diverge, putting **[[loop-engineering]]** fourth and **[[graph-engineering]]** fifth.
**Two independent surveys agree prompt → context → harness and disagree about what comes next; record both,
merge neither.**

## Relationship to neighbours

- **[[loop-engineering]]:** on this page's and Osmani's reading, the layer *one floor above* the harness
  (June-2026 term). Harness
  engineering makes a *single* agent run reliable; loop engineering wraps that harness in automated,
  repeating, self-improving loops (it "runs on a timer, spawns helpers, and feeds itself"). The harness
  is the unit the loop multiplies — see [[loop-engineering]] for the stacked-loop model and the five
  primitives + memory. **The ordering is disputed:** Morris (above), Breunig and Cloudflare's Flue put
  the harness *around* the loop rather than under it; [[loop-engineering]] carries both readings.
- **[[context-engineering]]:** harness engineering *uses* context engineering. Context engineering
  optimises *what the model sees*; harness engineering controls *the environment it operates in* —
  what it can access, what gets verified, what forces a retry. Building a coding-agent user harness
  is a specific form of context engineering ([[birgitta-bockeler|Böckeler]]).
- **[[agent-engineering]]:** the broader discipline of iterating LLMs into reliable systems;
  harness engineering is its environment-and-controls arm.
- **[[agent-governance]]:** the harness acts as a cybernetic *governor*; enforcement of invariants
  and audit trails overlaps with governance.
- **[[harness-evolution]] / [[harness-absorption]] / [[attention-interface]]:** what happens to the
  harness over time — automated improvement of it, migration of its capabilities into model weights,
  and what is left over when that migration is done.
- Distinct from **prompt engineering** (a single call) and from agent **frameworks/orchestrators**
  (see [[agent-harness]]).

## Counterpoint — "the harness is the easy 20%" ([[martin-dilger|Dilger]])

[[dilger-harness-is-20-percent-requirements-are-80|Dilger]] (2026-06-29) accepts harness engineering as
real but **subordinate**: the harness and the code are only ~20% of the solution; the other **80% is
clarifying requirements and understanding business processes** — "a human, communications problem" with
no technical fix. No quantity of agents, roles, skills, and guardrails rescues unclear requirements
("which trees to cut"). His charge is that the field over-invests in the fun 20% (taming the agent) and
under-invests in the 80% that [[event-modeling]] / [[spec-driven-development]] target. Not a refutation —
Böckeler's own view is that a harness can't *force* a non-deterministic model either — but a sharp claim
about **where the leverage is**: upstream of the harness, in the spec.

## Where automatic harness improvement does *not* reach

Two findings bound the practice, and both cut against the assumption that harness self-improvement generalises:

- **It is weakest where the workflow is prescribed.** [[evo-bench-can-language-models-improve-agent-harness|Evo-Bench]]
  finds autonomous evolution beats a hand-built harness on *General* tasks and excels at *Search*, but
  "struggles in **Office** tasks that demand highly specific processing workflows" *(arXiv preprint, not
  peer-reviewed)*. That is most enterprise work — and it is the closest thing to an experiment on
  [[dilger-harness-is-20-percent-requirements-are-80|Dilger's "the harness is the easy 20%"]] counterpoint
  above: a loop cannot discover a workflow nobody specified.
- **Self-improvement is only cheap where doing the task and editing the system need the same skill.**
  [[sbco-verifier-grounded-harness-optimization|SBCO]] names the precondition behind the Gödel-machine
  lineage: **self-referential** self-improvement "require[s] that the competence required to perform the task
  coincides or aligns well with the competence required for self-modification **which is the case for coding
  tasks**" *(arXiv preprint, not peer-reviewed)*. Outside coding it fails, and the workarounds are expensive.
  **Every harness-evolution result in this KB comes from coding or agent-benchmark tasks**, so the pattern's
  reach beyond them is unestablished. SBCO's own answer is *self-supervised rather than self-referential*:
  learn a decomposed bank of verifiers plus a harness policy from graded feedback, meta-agent fixed, no human
  labels — sensors as learned artifacts rather than authored ones.

## Open questions

How to keep a growing harness coherent (guides/sensors not contradicting — [[ahe-agentic-harness-engineering|AHE]]
finds harness components **interact non-additively**, so stacking good edits can *cap* the aggregate gain);
how to evaluate harness coverage/quality (a "code coverage" for harnesses — AHE's **change manifest +
next-round attribution** is one concrete answer, though it suffers "regression blindness"); whether single
general-purpose vs. specialised agents work best; the unsolved **behaviour harness**; and how much migrates
into models over time (AHE's weaker-base transfer suggests the harness *substitutes* for capability the
model lacks — the gain shrinks as the base saturates).

The batch adds three, all now stated by the field itself. **Can any of the reported gains survive a fair
protocol?** — the matched-budget and held-out-task objections in
[[wang-rethinking-evaluation-of-harness-evolution-for-agents]] are unanswered, and
[[evo-bench-can-language-models-improve-agent-harness|Evo-Bench]] answers one of Wang et al.'s two stated concerns (task-specific overfitting) by
construction (auxiliary-task evolution to isolate harness gains from base-model strength; sensitivity-aware
stratified splitting against task-set overfitting) while leaving the budget objection open. **Can a harness be
improved without regression?** — [[ning-code-as-agent-harness|Ning et al.]] list "self-evolving harnesses
without regression" and "harness-level evaluation and **oracle adequacy**" as open problems, which is the
field's own maps agreeing with AHE's measured *regression blindness*. **Should the model be frozen?** — AHE
freezes it so gains are attributable; [[harnessforge-joint-harness-and-policy-evolution|HarnessForge]] argues
that freezing it is exactly what leaves harness–reasoner **compatibility** unoptimised, and co-evolves the
harness–policy pair instead. *(All preprints.)* These are opposed commitments, not a progression.

- **Can you do harness engineering on a harness you rent?** Every practice on this page assumes the harness
  is yours to inspect and revise. For commercial agents in late 2026 the decisive layers are undisclosed —
  Anthropic publishes a core consumer prompt but not the per-feature blocks and not Claude Code's
  ([[willison-claudes-new-system-prompt]]); OpenAI publishes neither prompts nor tool descriptions, leaving
  the agent's own self-inventory as the only instrument ([[willison-understanding-chatgpt-work]]). Whether
  the discipline degrades to *harnessing around a black box* — and what that costs — is untested here.

## The convergence claim, running the other way (Dymitruk, 2026-08-15)

Nearly everything in this KB argues *from* [[event-modeling]] *to* agent practice.
[[dymitruk-move-prompts-into-scripts-deterministic]] argues the reverse in three sentences — do harness
engineering well enough and you reinvent the method:

> "Move as much from your prompts and agent md files into scripts. Deterministic behaviour is your goal.
> Evidence of how things work should be intermediate text files in directories that correspond to steps
> in your processes - even inboxes and outboxes. You'll naturally arrive at #EventModeling and
> #EventSourcing."

Three moves: prompts → scripts (this page's "engineer the environment, don't trust the prompt", stated as
a migration path); evidence as append-only intermediate files per step (a [[decision-trace]] arrived at
from the filesystem side, and the same instinct as
[[anthropic-effective-harnesses-long-running-agents]]'s progress files); and **"even inboxes and
outboxes"** — the tell, because once steps have inboxes and outboxes you have processors consuming and
emitting, which is Event Modeling's Automation pattern and event sourcing's transactional outbox.

It is an assertion by the method's creator about his own method's inevitability, so maximally motivated —
but it has an obvious test: do harnesses built with no Event Modeling exposure develop event-shaped
intermediate state? The loop-engineering cluster is full of practitioners describing exactly
these file-and-directory conventions without the vocabulary — [[miracle-my-loop-engineering-workflow|Miracle's]]
`status.md`/`handoff.md`/decision-log layering and
[[edwards-alexander-an-accidental-blackboard|the accidental blackboard]]'s in-repo plans are the two
closest instances now captured, neither of them Event-Modeling-informed.

## Related

[[token-budget-quality-cliff]] · [[agent-harness]] · [[harness-evolution]] · [[harness-absorption]] ·
[[attention-interface]] · [[loop-engineering]] · [[graph-engineering]] · [[agent-observability-and-evals]]

_Sources: [[fowler-bockeler-harness-engineering]] · [[openai-harness-engineering-codex]] · [[anthropic-effective-harnesses-long-running-agents]] · [[langchain-anatomy-of-an-agent-harness]] · [[firecrawl-what-is-an-agent-harness]] · [[guo-survey-question-answering-to-task-completion-harness-design]] · [[ning-code-as-agent-harness]] · [[wang-rethinking-evaluation-of-harness-evolution-for-agents]] · [[evo-bench-can-language-models-improve-agent-harness]] · [[sbco-verifier-grounded-harness-optimization]] · [[breunig-fable-and-the-end-of-the-free-lunch]] · [[morris-humans-and-agents-in-software-engineering-loops]] · [[miller-ai-assisted-production-support-with-critterwatch]] · [[willison-codex-bundles-libreoffice]]._
