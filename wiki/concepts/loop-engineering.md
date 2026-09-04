---
title: Loop Engineering
type: concept
created: 2026-06-28
updated: 2026-08-31
sources: [dilger-one-million-tokens-self-training-modeling-agent, dilger-modeling-agent-improved-by-learning-loop, bockeler-tdd-inside-the-agent-loop, dilger-describing-without-solving-burns-you-out, addyosmani-loop-engineering, langchain-the-art-of-loop-engineering, swyx-loopcraft-art-of-stacking-loops, willison-designing-agentic-loops, anthropic-getting-started-with-loops, willison-rewriting-bun-in-rust, addyosmani-own-the-outer-loop, ahe-agentic-harness-engineering, addyosmani-earning-taste-and-judgment, addyosmani-software-factories-light-and-dark, willison-fireside-chat-claude-code-team, willison-vibe-engineering, khononov-microservices-hype-to-ai-sloop, prefect-loops-vs-graphs]
tags: [harness-engineering, loop-engineering, agentic-ai, unattended-coding-agents, long-running-agents, focus]
---

# Loop Engineering

**The layer one floor above [[harness-engineering|the harness]].** Loop engineering is the practice
of **designing the control system that prompts, verifies, and stops an agent** — instead of being the
person who prompts it. Where [[harness-engineering]] builds the environment a *single* agent run
operates inside, loop engineering wraps that harness in **automated, repeating, self-improving loops**
so the human moves from *operator* to *designer*. [[addyosmani-loop-engineering|Addy Osmani]] puts the
boundary plainly: "Loop engineering sits one floor above the harness. The harness — but it runs on a
timer, it spawns little helpers, and it feeds itself."

The coinage is June 2026 ([[swyx-loopcraft-art-of-stacking-loops|swyx's "Loopcraft"]]), crystallized in
three practitioner quotes:
- **Peter Steinberger (Steipete):** "You shouldn't be prompting coding agents anymore. You should be
  designing loops that prompt your agents."
- **Boris Cherny** (Claude Code, Anthropic): "I don't prompt Claude anymore. I write loops, the loops
  do the work."
- **[[andrej-karpathy|Andrej Karpathy]]:** "remove yourself as the bottleneck… arrange things such
  that they're completely autonomous… arrange it once and hit go" — the same instinct that drives the
  [[llm-wiki]] this KB runs on.

## Earlier origin — Willison, Sept 2025

The idea (and a near-identical name) predates the June-2026 coinage: [[simon-willison]] named
**"designing agentic loops"** as "a critical new skill to develop" on **2025-09-30**
([[willison-designing-agentic-loops]]), built on the same definition — an agent "runs tools in a loop
to achieve a goal," so "the art of using them well is to carefully design the tools and loop." His
framing is more **hands-on and safety-first** than the 2026 sources and adds mechanics they under-weight:
**YOLO mode + sandboxing** (auto-approval is what makes brute force work and is "so dangerous"; quotes
Solomon Hykes — "an AI agent is an LLM wrecking its environment in a loop" — and recommends disposable
containers / [[prompt-injection]]-resistant no-internet sandboxes); **shell over
[[model-context-protocol|MCP]]** with tools documented in an `AGENTS.md`; **tightly scoped credentials**
(test/staging, hard budget caps); and a **when-to-loop** test — clear success criteria + tedious
trial-and-error, amplified by a clean automated test suite. So the KB's timeline is: Willison names the
*skill* (2025) → Osmani/swyx/LangChain name the *discipline and stack* (2026).

A parallel **term lineage** runs alongside: Willison also coined **"vibe engineering"**
([[willison-vibe-engineering]], 2025-10-07) for the *accountable* end of AI-assisted work — the
counterpart to [[vibe-modeling|vibe coding]] — which the ecosystem then re-settled as **"agentic
engineering"** (his own 2026-02-23 update). Loop engineering is the *mechanism* under that
accountable-end vocabulary: the discipline you practise while "staying the engineer."

## The Salty Lesson

swyx frames the stakes as **"the Salty Lesson for agents"** (a riff on Sutton's *Bitter Lesson* for
models): **"Don't fix things yourself, as you have done historically. Instead focus on systems that
scale with more agents, like goals and orchestration."** The thesis: the entire game is to **stack
loops** effectively — know when to go *down* a loop when things break (reliability) and *up* a loop as
models improve (leverage).

## The stacked-loop model ([[langchain-the-art-of-loop-engineering|LangChain]])

Four loops, each wrapping the one below; the key move is that an outer loop's feedback **reaches inside
and rewrites the inner loop**, so every cycle makes the inner loops more effective:

1. **Agent loop** — a model calls tools repeatedly until a task is done (the core [[react-loop]] /
   [[agent-harness]] primitive). *Automates work.*
2. **Verification loop** — a grader (deterministic or LLM-as-judge) scores output against a rubric and
   retries with feedback on failure. The **maker≠checker** split. *Ensures quality.* (Maps onto
   [[feedforward-and-feedback-controls|sensors]] and Böckeler's steering loop.) A worked in-the-wild
   instance: [[willison-sqlite-utils-4-mostly-written-by-fable|Willison's sqlite-utils 4.0]] release, where
   the agent reviews its own work, then a *different vendor's* model (GPT-5.5) reviews that and catches 2
   more P1 bugs fed into a fresh session — **cross-model** maker≠checker.
3. **Event-driven loop** — an external event (cron, webhook, new file, channel message) triggers the
   agent so it runs continuously as a background component, not something you invoke by hand
   ("always-on" / "heartbeats"). *Automates work at scale.* (This is where [[long-running-agents]] and
   [[unattended-coding-agents]] live.)
4. **Hill-climbing loop** — an analysis agent reads production **traces** and rewrites the harness
   config (prompts, tools, graders) — or, for open-weight models, feeds RL fine-tuning. *Automates
   improvement.* The self-improving outer loop; ties directly to [[agent-observability-and-evals]]. The
   **most rigorous primary for this loop** is [[ahe-agentic-harness-engineering|AHE (Lin et al., 2026)]] — a **preprint** (arXiv:2604.25850v1), not peer-reviewed, though it is a controlled study rather than a practitioner report:
   an evolution agent that autonomously rewrites a coding agent's harness and lifts pass@1 on Terminal-Bench 2
   from 69.7% → 77.0% over ten iterations, beating the hand-built Codex-CLI harness — the discourse above,
   turned into a measured experiment (see the dedicated section below).

## The hill-climbing loop, measured ([[ahe-agentic-harness-engineering|AHE, Lin et al. 2026]])

The one academic experiment behind the 4th loop. AHE keeps the **base model frozen** and lets a separate
**evolve agent** rewrite the harness, driven by three **observability** pillars that make autonomous
evolution stop "collapsing into trial-and-error": **component observability** (the harness is a decoupled
substrate of **seven editable component files** — system prompt, tool description, tool implementation,
middleware, skill, sub-agent config, long-term memory — so each failure maps to one file and every edit is
a revertible git commit), **experience observability** (millions of trajectory tokens distilled into a
layered, drill-down evidence corpus via **progressive disclosure**, so the evolver reads root causes not raw
logs), and **decision observability** (every edit ships a **change manifest** naming its predicted fixes and
at-risk regressions, verified against the next round's task deltas and **rolled back at file granularity** if
it fails — maker≠checker hard-wired, with the verifier/model config read-only so the self-modifier can't cheat).
Three findings sharpen the KB's picture: (1) **the gain is structural, not prose** — memory-only +5.6 pp,
tools-only +3.3 pp, middleware-only +2.2 pp, but **system-prompt-only −2.3 pp**, so prompt-only self-evolution
(ACE, TF-GRPO) misses where the value lives; (2) the frozen harness **transfers** (SWE-bench-verified at 12%
fewer tokens; +5.1 to +10.1 pp across three other model families, largest on weaker bases — the environment,
not the model, per [[tornhill-why-human-level-ai-wont-be-enough]]); (3) the loop suffers **regression
blindness** — it predicts which tasks an edit will *fix* ~5x better than random but which it will *break* only
~2x random, an honest measure of the "optimizes for the grader" leak. AHE also operationalizes the
"experience as explicit on-disk artifacts, not hidden parameter updates" thesis that links this loop to
[[event-sourcing]] and the [[llm-wiki]].

## The vendor taxonomy — four loop *types* ([[anthropic-getting-started-with-loops|Anthropic / Claude Code]])

The Claude Code team's own definition (**"a loop is an agent repeating cycles of work until a stop
condition is met"**) classifies loops by *how they're triggered, how they stop, which primitive
implements them, and which task suits them* — a **near-exact cross-map onto the LangChain stack above**,
but named from the operator's side and tied to concrete Claude Code primitives:

| Anthropic loop type | Trigger → stop | Primitive | Maps onto (LangChain) |
| --- | --- | --- | --- |
| **Turn-based** | user prompt → Claude judges done | plain prompt; encode checks as `SKILL.md` | agent loop (you are the checker) |
| **Goal-based** | manual → goal met OR turn cap | `/goal` (a *separate evaluator model* grades the stop) | verification / grader loop |
| **Time-based** | interval → you cancel / work done | `/loop` (local), `/schedule` (cloud) | event-driven / always-on loop |
| **Proactive** | event or schedule, no human → each task exits at its goal | compose `/schedule` + `/goal` + skills + **dynamic workflows** + **auto mode** | event-driven loop at scale |

Two design rules travel with it. **Quality is a property of the system around the loop:** clean
codebase, self-verification via skills, reachable docs, and a **second reviewer agent with fresh
context** (maker≠checker) — and when a result misses the bar, *"don't stop at fixing the individual
issue; encode it to improve the system for all future iterations"* (the hill-climbing move made
operational). **Token governance:** right-size the primitive/model, set clear stop criteria, **pilot
before large runs** (dynamic workflows can spawn hundreds of agents), and use **scripts for
deterministic work** ("running a script is cheaper than reasoning through the steps"). Caveat: it's a
vendor product doc — canonical for the *pattern*, framed around one product's features.

## A worked case at extreme scale ([[willison-rewriting-bun-in-rust|Bun → Rust]])

The rewrite of **Bun from Zig to Rust** is the most concrete public instance of the stacked loop.
Bun's **TypeScript test suite (~1M assertions) served as a language-independent conformance suite** —
i.e. the **grader/verification loop** made cheap and deterministic — letting a harness automate most of
the port. Jarred Sumner *"monitored workflows… prompting Claude to edit the loop to fix things"*
(loop-editing) and, when something broke, **"fixed the process that generates the code instead of
hand-fixing the code"** — the **hill-climbing loop** in the wild — with coordinated parallel agents in
worktrees. It shipped in Claude Code v2.1.181 ("Boring is good.") at ≈**$165k** in tokens, and raises
the [[willison-agentic-engineering-patterns|comprehension-debt]] question head-on ("how do you review a
+1M-line PR?"). The strongest existence proof yet that a conformance suite can *be* the loop's grader.

## The five primitives + memory ([[addyosmani-loop-engineering|Osmani]])

A loop needs five capabilities plus a place to remember — and the same shape ships natively in both
the Codex app and Claude Code (the names differ; the capability is identical):

1. **Automations** — scheduled discovery/triage; *the heartbeat* that makes it a loop and not a
   one-shot. (`/loop` re-runs on a cadence; `/goal` runs until a verifiable stop condition holds, with
   a *separate* model grading the stop — maker≠checker applied to "done.")
2. **Worktrees** — isolated checkouts so parallel agents don't collide on the same files.
3. **Skills** — project knowledge written down once (`SKILL.md`) so the loop doesn't re-derive your
   project from zero every cycle; the antidote to "intent debt." (Same SKILL.md pattern as
   [[jwilger-agent-skills-event-modeling]] and [[khononov-modularity-claude-code-plugin]]; a
   *vendor-maintained, source-verified* instance is [[miller-jasperfx-ai-skills-agent-skills|JasperFx AI
   Skills]] — 81 [[critter-stack]] skills that keep the agent off stale training data.)
4. **Plugins / connectors** — [[model-context-protocol|MCP]]-based access to real tools (issue tracker,
   DB, Slack) so the loop *acts* in your environment rather than only describing a fix.
5. **Sub-agents** — split the maker from the checker; a second agent (often a different model) catches
   what the first talked itself into.
6. **Memory (the sixth thing)** — on-disk state (a markdown file, a Linear board) that lives *outside*
   the conversation. "The agent forgets, the repo doesn't" — the same trick every
   [[long-running-agents|long-running agent]] depends on, and the same append-and-read instinct as
   [[event-sourcing]].

## The top rung — the [[software-factory]] ([[addyosmani-software-factories-light-and-dark|Osmani]])

Above the loop and the harness sits the **[[software-factory|software factory]]**: many harnessed loops fed
by a queue and drained through a review gate — "not a bigger agent; it is an org chart made of loops." Osmani
(leaning on [[dex-horthy|Dex Horthy]]'s "Harness Engineering is not Enough") adds three handles the KB now
files under [[software-factory]]: **light vs dark** (a *dark* factory ships code no human has read, verified
only by machines — it doesn't pay down [[comprehension-debt]], it takes it on "with the tests green the whole
way"; a *lit* factory keeps the lights on where judgment lives and moves review **upstream** to
design/architecture); **back pressure** ("you can only hand a loop as much autonomy as you can cheaply and
reliably verify, and not one inch more" — verification, not generation, is the constraint); and **loops vs
graphs** ("owning your control flow is really just walking the graph back around the loop" — a predefined
directed graph *is* back pressure drawn as a diagram). This is the qualitative, field-report companion to the
measured [[ahe-agentic-harness-engineering|AHE]] result.

## Taste is the ungradeable residue ([[addyosmani-earning-taste-and-judgment|Osmani]])

Once loops automate the *reps* that used to produce judgment, the durable human contribution is **choosing
what to build and judging whether it's any good** — "anything gradeable by someone else is getting
automated." The operational habit that lands here: **build a personal eval/rubric** (correctness,
maintainability, efficiency, security, style) and run it on ~50 real AI PRs — the verification/grader loop
turned inward as a calibration tool — plus "specify and verify separately" (spec quality is the biggest
lever) and "calibrate autonomy per task" (back-pressure as a daily instinct). The positive complement to the
"stay the engineer" caveats below.

## A vendor-team worked instance ([[willison-fireside-chat-claude-code-team|Claude Code team]])

Anthropic's own practice supplies concrete numbers for the stacked loops: **code review moved off humans over
months** by finding files where automated review "catches 100% of the issues," then, after any incident,
updating the reviewer *and adding the causing PR to an eval set so the metric never regresses* — the
hill-climbing loop + maker≠checker + an eval-as-trust substrate, in production. Their **on-disk memory
primitive** is literally "a markdown file per channel" (Claude Tag), and **auto mode** (a Sonnet classifier
gating each tool call, honoring dynamic in-prompt permissions and sandbox escapes) is the safety layer that
lets the loop run unattended — "the agent forgets, the repo doesn't," made concrete.

## Relationship to neighbours

- **[[harness-engineering]]:** loop engineering is strictly *above* it. The harness makes one run
  reliable; the loop runs the harness on a timer, in parallel, and feeds its own improvement. Osmani's
  "factory model" sense of the harness is the unit the loop multiplies.
- **[[ralph-loop]]:** the original "keep going across context windows" pattern is the **agent loop**
  (level 1) made persistent — a primitive loop engineering composes, not the whole stack.
- **[[long-running-agents]] / [[unattended-coding-agents]]:** these *are* the event-driven loop (level
  3) — agents that run with no human in the loop until a PR is ready ([[stripe-minions-one-shot-coding-agents|Stripe minions]]
  are a worked instance). Loop engineering names the surrounding discipline.
- **[[agent-observability-and-evals]]:** the hill-climbing loop (level 4) is evals/traces turned into
  an automatic harness-rewrite — the missing feedback path from observability back into the harness.
- **vs. prompt engineering:** "the leverage point moved" (Cherny). Loop design is *harder* than
  prompting, not easier — two people building the same loop get opposite results depending on whether
  they use it to move faster on work they understand or to avoid understanding it at all.
- **vs. [[graph-engineering]]:** the layer *above*. [[jeremiah-lowin|Lowin]]/[[prefect|Prefect]]
  ([[prefect-loops-vs-graphs]]) frame **loops as one agent's internal (micro) behaviour** and **directed
  agentic graphs as macro orchestration across many agents** — the next rung of the same
  prompt→multi-prompt→loop→graph "take more control" ladder. A single-node graph *is* a loop; splitting
  it lets you scope tools/models/access per node, return control at each edge, and gain reproducibility
  and auditability a bare loop can't. Complementary, not rival. (Same shape as
  [[addyosmani-software-factories-light-and-dark|Osmani's]] "a directed graph is back-pressure drawn as
  a diagram.")

## The standing caveats (Osmani)

Three problems get **sharper** as the loop gets better, not easier:
- **Verification is still on you** — "a loop running unattended is also a loop making mistakes
  unattended"; "done" is a claim, not a proof.
- **Comprehension debt** — the faster the loop ships code you didn't write, the bigger the gap between
  what exists and what you understand, unless you read what it made.
- **Cognitive surrender** — the comfortable posture (take whatever it gives back) is the dangerous one.
  "Build the loop. But build it like someone who intends to stay the engineer, not just the person who
  presses go."

The accountability corner of "stay the engineer" is stated sharply by [[simon-willison]] in
[[willison-directly-responsible-individuals|"Directly Responsible Individuals"]] (2026-07-12): however
autonomous the loop, an agent should **never** be the project's DRI, because "humans can take
accountability for their actions where machines cannot" (echoing IBM's 1979 "a computer can never be held
accountable, therefore a computer must never make a management decision"). This is the human-ownership
counterpart to [[addyosmani-own-the-outer-loop|Osmani's Answerability]] demand and a hard boundary on the
[[autonomy-ladder]] — the DRI slot does not transfer to the machine.

## Inner loop vs outer loop ([[addyosmani-own-the-outer-loop|Osmani, 2026-07]])

Osmani's follow-on to his primary makes the human's role precise: the agent takes the **inner loop**
(investigate → implement → verify → repeat, where an *independent* check — not the model's say-so —
decides "done"); the human owns the **outer loop**, an accountability boundary held up by three terms —
**Quality** (checks that produce evidence before anything ships) → **Verdict** (the human production
decision: ship / block / redirect / narrow / reject) → **Answerability** (you can explain *why* when
asked). The human belongs in the **constraints, sampling, audit, and ownership loops — never the inner
one** ("the agent can ship more than you can review"). Autonomy is granted *deliberately under the
maximum* so ordinary engineering signals (types, tests, sandboxes, audit logs) provide **back-pressure**
to stop the loop. He proposes an **"accountability contract" per codebase** and reframes the shift as
**"the bottleneck moves from 'can we build this?' to 'should this exist, can we answer for it?'"** —
backed by fresh figures (Sonar 2026: 42% of commits AI-assisted; Anthropic RCT: AI-leaning engineers
scored 17pp lower on comprehension; Wharton: when the AI was wrong, ~¾ accepted it anyway with *more*
confidence). This is the outer-loop complement to the five-primitive *inner*-loop machinery above, and
the sharpest KB statement of "stay the engineer."

## What does *not* belong inside the loop ([[bockeler-tdd-inside-the-agent-loop|Böckeler, 2026-08]])

Most of this page is about what to put *into* the loop. The KB's first captured **negative eval** is
about what to leave out. Böckeler tested whether telling an agent to follow **TDD inside its own loop**
improves outcomes: across 5 batches of greenfield tasks, blind-ranked by a stronger model, there was **no
quality gain** (non-TDD solutions often ranked higher), **no mutation-score gain**, and a **3–8.5× token
cost**. Three findings matter for loop design:

- **Process instructions can destroy a good behaviour.** The non-TDD runs did **full up-front design**
  before writing anything; TDD instructions suppressed that, so the design "emerged from the sum of many
  locally-minimal decisions and was rarely revisited," landing on "whatever shape the first test happened
  to lock in." A guide aimed at the agent's *method* displaced a better emergent method.
- **A self-graded step is not a check.** "When the agent both writes the test and confirms it failed, a
  red test tells you the agent ran it and saw failure, **not that the failure was for the right
  reason**." This is the **maker≠checker** rule (loop 2 above) applied at the finest grain — and a
  warning that verification loops staffed by the same agent are theater.
- **Complex process prompts are a maintenance liability**, "an uphill battle against the training data"
  that needs constant iteration and is likely to be **more volatile across model releases** than simple
  ones — a hidden cost in the hill-climbing loop's own surface area.

Her generalisation is the design rule: *"being overly specific about **how** we want a model to do
something is not a sustainable approach. Instead… monitor the **outcomes** and give feedback… and think
carefully about **where we insert ourselves as arbiters**."* In [[feedforward-and-feedback-controls]]
terms — spend the budget on **sensors**, not **guides**. Her substitutes are all outcome sensors
([[mutation-testing]] for regression quality; static analysis + periodic modularity review;
files-touched and tokens-per-change trends) plus **Ivett Ördög's "Approved Scenarios"** — human-frozen
functional scenarios that must be re-approved when violated, i.e. a human-authored spec *outside* the
loop rather than a process *inside* it. Note the compatibility with the [[given-when-then]] thread: the
spec should come from outside; only the iteration belongs inside.

The human-cost counterpart arrived the same week from [[martin-dilger]]
([[dilger-describing-without-solving-burns-you-out]]): running "5 agent sessions in parallel, overseeing
my agents like a kindergartner" left him burned out — *"a few years ago, we were obsessed with protecting
people from context switching. Now we call the same thing productivity."* His diagnosis is the
[[spec-driven-development]] version of cognitive surrender: teams that "stop solving problems and just
describe them, and then hand it to AI and hope it figures out the solution" are "checking out before it
gets interesting," and *"describing a problem without solving it leaves a hole that keeps growing."* A
practitioner datapoint against the implicit "more parallel loops = more leverage" assumption, from
someone who runs a 6–10-agent rig himself.

## A loop that rewrites its own skills, and grades itself against artifacts (Dilger, 2026-08)

The KB's most concrete instance of the **self-evolution** direction this page's open questions ask
about, and notably not a coding loop — the artifact under construction is an
[[event-modeling|event model]] ([[dilger-one-million-tokens-self-training-modeling-agent]], [[dilger-modeling-agent-improved-by-learning-loop]]).

The loop: model a requirement set → **structurally diff** the result against a corpus of hand-crafted
good models → have the agent **rewrite its own skill files** from the differences → re-model, comparing
against both the previous round and the corpus. Local hardware, QWEN3.7:27b, over a million tokens
overnight, left running continuously.

Two things it contributes to this page.

**It is a partial answer to the grader-leak question.** This page asks how a hill-climbing loop avoids
optimizing for the grader rather than the goal, with [[ahe-agentic-harness-engineering|AHE]] measuring
the leak rather than closing it. Dilger's rubric is an **artifact corpus, not a metric** — the agent
cannot game a structural diff against known-good models the way it can game a score, because there is
no scalar to maximize. That is a genuinely different shape of grader. The honest limit: it converges on
*the corpus author's conventions*, so it trades the leak problem for a taste-ownership problem.

**It complicates the hill-climbing assumption.** Roughly every fifth iteration degrades badly as the
model nears its token budget ([[token-budget-quality-cliff]]) — meaning iteration results are **not
independent samples of the agent's ability**, and a naive "did it improve?" comparison between
consecutive rounds can be measuring budget position rather than skill. Dilger's own loop makes exactly
that comparison. He says he'll feed the cliff back into the loop; how to correct for it is open.

Also note what the loop *recovered*: three modeling conventions its author holds but had never written
down as rules. The rubric extracted tacit knowledge from artifacts — relevant to
[[addyosmani-earning-taste-and-judgment|"taste is the ungradeable residue"]], since part of it graded.

*Caveat: self-reported by the vendor of the platform, unquantified, one local model.*

## Open questions

How to verify an unattended loop's output at scale (the maker≠checker split helps but doesn't close
it); how the hill-climbing loop avoids optimizing for the grader rather than the goal (**[[ahe-agentic-harness-engineering|AHE]]
now measures the leak** — "regression blindness," ~2x random at predicting what an edit will break — rather
than resolving it; naming upcoming regressions is "the clearest direction for future self-evolution loops");
whether loop-engineering primitives converge to a portable standard across Codex/Claude Code (AHE's
**seven-component NexAU substrate** is one concrete proposal for the editable surface); and the
unexplored seam — **could an [[event-modeling|Event Model]] supply the loop's goals and stop
conditions** (slice = unit of work, GWT = the verification rubric), tying this thread to
[[dilger-event-modeling-agent-harness|Dilger's Event Modeling Agent Harness]]? (That last seam is now
partly walked — see the self-training loop above, though it grades *models* rather than using a model to
grade code.) Newly open: **does output quality track remaining budget rather than task difficulty**, and
if so what does that do to every iteration-over-iteration comparison in this page
([[token-budget-quality-cliff]])?

## The skeptics' read — is "the loop" just this cycle's Holy Grail?

The thread above is built almost entirely from advocate/practitioner primaries. The KB's one
**contrarian counterweight** is [[vlad-khononov]]
([[khononov-microservices-hype-to-ai-sloop]], 2026-06-30): the **AI "(s)loop"** (spelled with a nod to
*slop*) is "the new Holy Grail," and the hype **rhymes with microservices 12 years ago** — "a crowd
chasing something most of them can't quite define," the metric shifted from "thousands of services" to
"thousands of deploys per day." As microservices' reckoning produced the modular monolith and the
monorepo, he asks what we'll "reach for to cope with the hangover this time." He does **not** dispute
the mechanics — his standing thesis is that the payoff lands only on a **modular substrate**
([[khononov-golden-age-of-modularity]], [[business-capabilities]]) — he disputes the froth and predicts
a correction. It rhymes with the "dumbest version becomes representative" worry [[jeremiah-lowin|Lowin]]
voices about the [[ralph-loop|Ralph loop]] ("a new round of slop") and with the "stay the engineer"
caveats above, but Khononov is the only captured voice framing the *whole trend* as a repeat hype cycle.

_Sources: [[bockeler-tdd-inside-the-agent-loop]] · [[dilger-describing-without-solving-burns-you-out]] · [[addyosmani-loop-engineering]] · [[langchain-the-art-of-loop-engineering]] · [[swyx-loopcraft-art-of-stacking-loops]] · [[willison-designing-agentic-loops]] · [[anthropic-getting-started-with-loops]] · [[willison-rewriting-bun-in-rust]] · [[addyosmani-own-the-outer-loop]] · [[ahe-agentic-harness-engineering]] · [[addyosmani-earning-taste-and-judgment]] · [[addyosmani-software-factories-light-and-dark]] · [[willison-fireside-chat-claude-code-team]] · [[willison-vibe-engineering]] · [[khononov-microservices-hype-to-ai-sloop]] · [[prefect-loops-vs-graphs]]._
