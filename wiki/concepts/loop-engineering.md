---
title: Loop Engineering
type: concept
created: 2026-06-28
updated: 2026-09-04
sources: [dilger-one-million-tokens-self-training-modeling-agent, dilger-modeling-agent-improved-by-learning-loop, bockeler-tdd-inside-the-agent-loop, dilger-describing-without-solving-burns-you-out, addyosmani-loop-engineering, langchain-the-art-of-loop-engineering, swyx-loopcraft-art-of-stacking-loops, willison-designing-agentic-loops, anthropic-getting-started-with-loops, willison-rewriting-bun-in-rust, addyosmani-own-the-outer-loop, ahe-agentic-harness-engineering, addyosmani-earning-taste-and-judgment, addyosmani-software-factories-light-and-dark, willison-fireside-chat-claude-code-team, willison-vibe-engineering, khononov-microservices-hype-to-ai-sloop, prefect-loops-vs-graphs, voss-what-the-hell-is-a-loop-anyway, wong-loop-engineering-teaching-ai-agents-how-to-think, miracle-my-loop-engineering-workflow, morris-humans-and-agents-in-software-engineering-loops, breunig-harnesses-are-situated-agents, addyosmani-practical-loop-engineering, addyosmani-human-judgment-relocates, addyosmani-code-agent-orchestra, addyosmani-agentic-code-quality, macmanus-schott-react-for-agents-flue-meta-harness, macmanus-pocock-wayfinder-skill-fog-of-war, wang-rethinking-evaluation-of-harness-evolution-for-agents, evo-bench-can-language-models-improve-agent-harness, sbco-verifier-grounded-harness-optimization, harnessx-composable-adaptive-evolvable-agent-harness-foundry, harnessforge-joint-harness-and-policy-evolution, mcateer-evolution-of-the-agent-harness, laycock-maybe-we-shouldnt-be-reviewing-all-this-code, willison-more-than-just-code-review, tornhill-controlling-the-uncertainty-machine, dilger-loop-engineering-never-argue-with-agent, nick-tune-event-sourced-claude-code-workflows, fowler-fragments-2026-09-01, miller-pondering-continuous-integration-ai-world-order]
tags: [harness-engineering, loop-engineering, agentic-ai, unattended-coding-agents, long-running-agents, focus]
---

# Loop Engineering

**The layer one floor above [[harness-engineering|the harness]]** — *on the reading this page opened
with, which is itself contested; see "Does the loop sit above the harness, or inside it?" below.* Loop
engineering is the practice of **designing the control system that prompts, verifies, and stops an agent**
— instead of being the person who prompts it. Where [[harness-engineering]] builds the environment a
*single* agent run operates inside, loop engineering wraps that harness in **automated, repeating,
self-improving loops** so the human moves from *operator* to *designer*.
[[addyosmani-loop-engineering|Addy Osmani]] puts the boundary plainly: "Loop engineering sits one floor
above the harness. The harness — but it runs on a timer, it spawns little helpers, and it feeds itself."

The coinage is June 2026 ([[swyx-loopcraft-art-of-stacking-loops|swyx's "Loopcraft"]]), crystallized in
three practitioner quotes:
- **Peter Steinberger (Steipete):** "You shouldn't be prompting coding agents anymore. You should be
  designing loops that prompt your agents."
- **Boris Cherny** (Claude Code, Anthropic): "I don't prompt Claude anymore. I write loops, the loops
  do the work."
- **[[andrej-karpathy|Andrej Karpathy]]:** "remove yourself as the bottleneck… arrange things such
  that they're completely autonomous… arrange it once and hit go" — the same instinct that drives the
  [[llm-wiki]] this KB runs on.

**But the vocabulary predates the moment the market adopted it — twice.** Besides Willison (below),
[[morris-humans-and-agents-in-software-engineering-loops|Kief Morris]] published the
**out-the-loop / in-the-loop / on-the-loop** taxonomy *and* **"the agentic flywheel"** (agents directed to
improve the harness themselves, with a staged path from interactive review → recommendations filed into
the product backlog → agents scoring their own recommendations and **auto-approval above a score
threshold**) on **2026-03-04** — four months before [[addyosmani-own-the-outer-loop|Osmani's outer loop]]
and three before [[langchain-the-art-of-loop-engineering|LangChain's hill-climbing loop]], both of which
this page presents as the naming events. Morris also supplies the crispest operational test for the
distinction: *"The 'in the loop' way is to fix the artefact… **The 'on the loop' way is to change the
harness that produced the artefact** so it produces the results we want."* So the KB's timeline is:
Willison names the *skill* (2025-09) → Morris names the *positions* and the *flywheel* (2026-03) →
Osmani/swyx/LangChain name the *discipline and stack* (2026-06) → [[voss-what-the-hell-is-a-loop-anyway|Voss]]
observes that the word now means at least four things (2026-07). *(Morris is **NOT INDEPENDENT** on
harness engineering — Thoughtworks author, Thoughtworks series, Thoughtworks-coined term.)*

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
trial-and-error, amplified by a clean automated test suite. He is the first rung of the corrected
timeline above (skill 2025-09 → positions 2026-03 → discipline 2026-06 → disambiguation 2026-07), which
supersedes the two-step "Willison → Osmani/swyx/LangChain" chronology this page used to state.

A parallel **term lineage** runs alongside: Willison also coined **"vibe engineering"**
([[willison-vibe-engineering]], 2025-10-07) for the *accountable* end of AI-assisted work — the
counterpart to [[vibe-modeling|vibe coding]] — which the ecosystem then re-settled as **"agentic
engineering"** (his own 2026-02-23 update). Loop engineering is the *mechanism* under that
accountable-end vocabulary: the discipline you practise while "staying the engineer."

## What "a loop" means — five definitions that do not agree

The word is overloaded, and the KB should say so before using it. [[voss-what-the-hell-is-a-loop-anyway|Laurie
Voss]] wrote his July-2026 mapping essay for exactly this reason: *"the people talking about loops aren't
all discussing the same thing. I counted at least four distinct architectures hiding behind that one
word."* Five definitional primaries are now captured, and they conflict on the unit, on the layering, and
on whether this is one discipline or several.

| Source | What a loop **is** | The unit it iterates on | Where the harness sits |
| --- | --- | --- | --- |
| [[langchain-the-art-of-loop-engineering\|LangChain]] | four *stacked* loops: agent → verification → event-driven → hill-climbing | work, quality, scale, improvement | below the loop |
| [[anthropic-getting-started-with-loops\|Anthropic]] | "an agent repeating cycles of work until a stop condition is met" — four *types* by trigger/stop/primitive | one product's primitives | below the loop |
| [[voss-what-the-hell-is-a-loop-anyway\|Voss]] | **at least four different architectures**: execution / task / product / system, plus the **oversight loop** he names | steps in a task / one artifact / a codebase+backlog / the primary system itself | not his axis |
| [[wong-loop-engineering-teaching-ai-agents-how-to-think\|Wong]] | **"a loop is a task plus a check. A task without a check is just hope."** One construct, four components: trigger, goal, verifier, stop rules | one agent's campaign toward one goal | **below** — "a harness governs one step, a loop governs the campaign" |
| [[miracle-my-loop-engineering-workflow\|Miracle]] | **many loops, one grammar** — session/sprint/program at hours/days/weeks, all running *objective → execution → feedback → refined objective* | the same thing at three time scales | the harness is "a place, not a prompt" the loops run **on** |
| [[morris-humans-and-agents-in-software-engineering-loops\|Morris]] (2026-03) | a **why loop** (ideas→outcomes) over nested **how loops** | intermediate artefacts | **above/around** — the harness *is* what controls the loops |
| [[breunig-harnesses-are-situated-agents\|Breunig]] | the loop is the small **core** the developer drives from the keyboard | one task | **around** — eight layers of world; Cloudflare's Flue **hides the loop from users entirely** |

**Three specific incompatibilities worth keeping in front of the reader:**

- **The three fourfold taxonomies have different members.** Voss's *task loop* (the [[ralph-loop|Ralph
  loop]]) has no LangChain counterpart; LangChain's *verification loop* is not one of Voss's four at all
  (for Voss, verification is an **exit condition of every loop**, not a loop); and Voss classifies the
  [[software-factory]] **as** a loop — his *product loop* — where this KB files it as the rung *above*
  loops.
- **Voss's taxonomy needs the loops to be unalike; Miracle's needs them to be alike.** Voss distinguishes
  his four precisely by what ends them and where the human sits. Miracle's triangle exists *because*
  "every loop, at every scale, runs the same grammar and shares the same start point and end point."
  Both cannot be the frame.
- **Loop-above-harness vs harness-above-loop.** See the dedicated section below.

**Where they do converge — and it is a real result.** Two independent authors state the same criterion
for what makes something a loop at all: Voss — *"Dispatch, gather, validate is a pipeline: nothing feeds
back into a next cycle, and **a loop without feedback is just a `for` statement**"* (which is why he
excludes Cognition's fan-out "Agentic MapReduce" from his map, calling fan-out *"a topology you can
deploy inside any of the four loops, not a loop of its own"*); and Miracle — *"**Feedback that doesn't
refine the next objective is just logging.** The end point of one loop is the start point of the next.
That is what makes it a loop and not a pipeline."* **Refinement of the next iteration is the test.** It
is worth running the KB's own [[agentic-workflow-patterns]] against it: several of those patterns are
pipelines.

Voss's other durable contribution is that **autonomy is a dial that exists separately on every loop** —
*"You can run a fully autonomous execution loop inside a heavily supervised product loop"* — so the
question is never which camp wins but *"what information do you need to set each dial correctly?"* He
also names the ring swyx's own diagram left blank (verbs *set goals, allocate, cull*, exit condition
*none*) the **oversight loop**, *"the one ring where a human should live,"* quoting Osmani from the AIEWF
stage: **"That inner loop is capability. The outer loop is agency."**

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
   **Since 2026-07 those gains are contested.** [[wang-rethinking-evaluation-of-harness-evolution-for-agents|Wang
   et al. (arXiv:2607.12227v2)]] argue automatic harness evolution is itself a search and must be compared against
   test-time scaling under **matched feedback and inference budgets**, and that searching and reporting on one
   benchmark risks overfitting to it; on Terminal-Bench 2.1 with GPT-5.4 and Claude Opus 4.6 it "does not
   consistently outperform simple test-time scaling methods and exhibits limited generalization" *(also a
   preprint, not peer-reviewed)*. Cite AHE's 69.7% → 77.0% with the dispute attached. The full picture — four
   competing methods, a purpose-built benchmark, and both sides of the argument — is on [[harness-evolution]].

## The hill-climbing loop, measured ([[ahe-agentic-harness-engineering|AHE, Lin et al. 2026]])

The one academic experiment behind the 4th loop — **and its headline number is contested; read the
paragraph closing this section, and [[harness-evolution]], before quoting it.** AHE keeps the **base model
frozen** and lets a separate
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

**A practitioner instance of the same rung, built on an event log (Tune, 2026-03-04).**
[[nick-tune-event-sourced-claude-code-workflows]] persists **only events** from his Claude Code workflow
state machine and derives state by replay, which turns the loop's own history into the instrument:
per-state dwell time, **rejection counts** (code review failed) and **hook-denial counts** (the agent
attempted something disallowed in that state), plus a journal enforced at ≥1 entry per iteration by hard
blocks. His stated target for the last two is **zero** — *"they indicate a waste of time, waste of
tokens, and indicate our agent has sub-optimal instructions"* — which is the cleanest **defect signal on
the harness rather than on the code** the KB holds. And the hill-climbing step is explicit: *"Don't just
build metrics from your events, feed them to your AI assistant… It can identify why problems exist and
suggest how to optimize the context or workflow"* — a CLAUDE.md edit or a review-agent prompt change.

Read against [[dilger-modeling-agent-improved-by-learning-loop|Dilger's self-training loop]], the two
differ in **what grades the run**: Dilger's grader is a structural diff against a corpus of hand-crafted
artifacts, Tune's is the execution log of the loop itself. The page's own warning about metric-shaped
graders applies to Tune's and not to Dilger's — a zero-denials target is exactly the kind of proxy an
agent can satisfy by narrowing what it attempts.

*(**IMPRESSION NOT MEASUREMENT · NOT INDEPENDENT** — his own harness, and the "15 minutes in RESPAWN vs
2 minutes DEVELOPING" reading is from **one session of a personal project**, which he states. His
"great results on real projects" carries no number, and cross-session analysis and the control centre
are **explicitly unbuilt**.)*

**Three 2026 findings bound the loop, and all three are preprint evidence.** *One:* it does not generalise off
coding-shaped work — [[sbco-verifier-grounded-harness-optimization|SBCO]] identifies the precondition behind
self-referential self-improvement ("the competence required to perform the task coincides or aligns well with
the competence required for self-modification **which is the case for coding tasks**"), so the entire evidence
base for this loop is coding and agent benchmarks; SBCO's answer is *self-supervised rather than
self-referential*, learning a bank of verifiers from graded feedback with a fixed meta-agent. *Two:* it is
weakest where workflows are prescribed — [[evo-bench-can-language-models-improve-agent-harness|Evo-Bench]]
finds autonomous evolution beats hand-built harnesses on *General* and *Search* tasks but "struggles in
**Office** tasks that demand highly specific processing workflows", the closest thing to an experiment on
[[dilger-harness-is-20-percent-requirements-are-80|Dilger's "harness is the easy 20%"]]. *Three:* it plateaus
early — Evo-Bench reports "critical temporal anomalies like **early saturation**", independently corroborating
AHE's non-monotone curve. Also worth registering as a *disagreement* inside the same literature: AHE claims to
beat a hand-built harness (Codex-CLI), while Evo-Bench's nine-model sweep reports automatic evolution "closely
**approaching** state-of-the-art human-engineered baselines" — approaching, not beating.

## The vendor taxonomy — four loop *types* ([[anthropic-getting-started-with-loops|Anthropic / Claude Code]])

The Claude Code team's own definition (**"a loop is an agent repeating cycles of work until a stop
condition is met"**) classifies loops by *how they're triggered, how they stop, which primitive
implements them, and which task suits them*. This page used to call the result a **"near-exact cross-map
onto the LangChain stack above"**; **it no longer does.** Two vendors' four-part schemes being alignable
is not a settled taxonomy — a third fourfold taxonomy ([[voss-what-the-hell-is-a-loop-anyway|Voss]]) has
different members entirely, and two further definitions (Wong, Miracle) fit none of the three. See *What
"a loop" means* above. The mapping column below is a convenience, not a correspondence:

| Anthropic loop type | Trigger → stop | Primitive | Loosely maps onto (LangChain) |
| --- | --- | --- | --- |
| **Turn-based** | user prompt → Claude judges done | plain prompt; encode checks as `SKILL.md` | agent loop (you are the checker) |
| **Goal-based** | manual → goal met OR turn cap | `/goal` (a *separate evaluator model* grades the stop — **transcript against stated rules only, not output quality**) | stop-condition referee, *not* the verification loop |
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
   one-shot. (`/loop` re-runs on a cadence; `/goal` runs until a verifiable stop condition holds, with a *separate*
   evaluator model grading the stop. **Note what that evaluator is not:** per
   [[addyosmani-practical-loop-engineering|Osmani, 2026-08]], *"The evaluator sitting behind goal is not
   that checker… **It doesn't look at the content** to see if it's good or bad in any way, shape, or form.
   All it does is **examine the conversation transcript** to see if the hard rules you specified have been
   met."* It is a **stop-condition referee, not an output reviewer** — so it is not maker≠checker in the
   quality sense, and a separate verifying sub-agent is still required.)
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

## Two months on: what the primitives are actually used for ([[addyosmani-practical-loop-engineering|Osmani, 2026-08-14]])

The discipline has narrowed to **two primitives** where in early 2026 it meant hand-rolled bash loops and
[[ralph-loop|Ralph]] experiments *"largely on some of our personal projects where, if we ran into a wall,
it didn't really have a big cost."* `/goal` drives a bounded task to a measurable finish line; `/loop` is
*"a little bit more of a scheduler… think of it a little bit like a cron,"* best for polling logs or
watching external state. Composed: **loop supplies the heartbeat, goal supplies the hands.**

**A `/goal` invocation carrying five distinct constraints**, worth keeping as the KB's template: a target
metric *with its named measurement tool* ("Lighthouse performance score is >= 92 and LCP under 1.8s **as
shown by the Lighthouse CLI output**"), an invariant ("Do not change the public API of any hooks"), a
**per-turn progress requirement** ("Each turn must improve at least one reported metric"), a
**no-progress abort** ("abort if two consecutive turns show no improvement"), and a **turn cap** ("Stop
after 10 turns").

**What loops are not for — the exclusion criterion this page has lacked.** *"If you don't have a clear
idea of what the end-state/done/good means for your completion, it may not be the right pattern."* The
named anti-goal is *"keep going until this UI design is good"* — *"What does that mean? Good to who? How
is it being evaluated?"* **Tasks requiring human taste, subjective design, or open-ended creative
exploration are excluded**, which is the operational form of
[[addyosmani-earning-taste-and-judgment|"anything gradeable by someone else is getting automated."]]

**Delegation calibrated by blast radius:** fully delegated — "go write the documentation for it," "go
double check that we have sufficient test coverage"; watched closely — complex work, and **anything
touching authentication, security, finance, or a system the agent has been granted access to.** *"There's
nuance when deciding to use it for an evergreen codebase without users… vs. say a brownfield bank
codebase."*

**A spin detector, and a convergent bound.** *"Give the same command a third time with no change from the
second and it's probably time to stop."* Three practitioners independently land on the same limit:
Osmani's third-identical-attempt rule; [[addyosmani-code-agent-orchestra|his own]] "kill and reassign
after 3+ stuck iterations"; and [[miracle-my-loop-engineering-workflow|Miracle's]] *"If a fix fails
twice, stop. Re-read the whole section, find where the mental model was wrong, and propose something
fundamentally different. **No third attempt at the same idea.**"* Convergent practitioner rule — **none of
the three measured it.**

*(Product-specific fine print, Aug 2026: recurring loops **expire seven days after creation** and are
**session-scoped**, though `--resume`/`--continue` restores them inside the window; `/schedule` runs in
the cloud for anything that must outlive the session.)*

## A fully specified single-practitioner rig ([[miracle-my-loop-engineering-workflow|Miracle, 2026-08-10]])

*"I don't have a prompt. I have a triangle of loops… The prompt is maybe five percent of the outcome. The
loops are the rest."* Three nested loops — **session** (hours), **sprint** (days), **program** (weeks) —
all running one grammar, starting from **a written commission rather than a chat message** and ending on
*ship only what passes verification, then a retro*. Four things it contributes that this page did not
have:

- **Three gates in sequence, none advisory.** A **plan-checker** agent audits the plan before execution
  (planner and checker never share a context); a **Nyquist test gate** samples the change surface densely
  enough *"to reconstruct what was actually built, and catch where it aliases away from what was asked"*;
  and a **goal-backward verifier** — *"Forward verification asks 'does the code run?' Goal-backward
  verification starts from the original intent and walks in reverse: for every requirement in the plan,
  where in the diff is it satisfied? **Any requirement without evidence fails the audit, even if all the
  tests pass.**"* That is a **verifier axis the KB has not named** — direction, not just independence —
  and it is the direct answer to [[addyosmani-human-judgment-relocates|"when green is misleading"]]. A
  [[given-when-then|GWT]] set is exactly a backward-verifiable requirement list.
- **Amdahl's law at the join.** Execution is fork-join, but *"the join is a gate, not a barrier… The join
  doesn't merge output. **It merges confidence.**"* And the bound: *"**Generation parallelized;
  verification did not.** So generation ≈ max(task time), but delivery ≈ generation + verification.
  Fork-join doesn't eliminate the serial work. It concentrates it at the join, which is exactly where my
  gates live."* This is the formal underpinning for [[software-factory]]'s back-pressure rule and for
  [[addyosmani-human-judgment-relocates|"my cognitive bandwidth does not scale with the agents."]]
- **Documents, not conversations, at every boundary.** *"Documents survive context windows.
  Conversations don't."* A `status.md` that **is** the reference (not the chat), a `handoff.md` session
  baton (mission, repo state, locked decisions, open gates, a **"not your problem" scope boundary**,
  pickup checklist) that travels between machines over `scp`, a decision log *"for the calls you never
  want re-litigated."* His one transferable instruction: *"If you copy one practice from this article,
  make it this one: give your harness explicit context layers."* `autoCompact` is **disabled on
  purpose**, and the orchestrator **restates its branch table at every status check** because
  *"restatement is the only compaction-proof memory."*
- **Bounded audit loops and a self-visible fuel gauge.** Two revisions on a plan, two attempts on a fix,
  then a human — *"Unbounded loops are how agents burn hours polishing a wrong answer."* The statusline's
  context meter is **written to a bridge file the context-monitor hook reads, so warnings are injected
  into the agent**: *"The agent sees its own fuel gauge, not just me."*

His governing principle is the one this page's maker≠checker rule needs stated flatly: **"never trust a
single source; nothing checks itself."** *(Practitioner self-report; **no outcome measured** — every
quantity in the piece is configuration, not evidence. His trust ledger is filed under
[[autonomy-ladder]].)*

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
measured (and now contested — [[harness-evolution]]) [[ahe-agentic-harness-engineering|AHE]] result. Note
that [[voss-what-the-hell-is-a-loop-anyway|Voss]] classifies the factory **as** a loop (his *product loop*),
against this placement of it above loops.

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

**Contested on principle (2026-09).** "Code review moved off humans" is exactly the move
[[rachel-laycock]] rejects: *"I don't think the answer is an AI agent pretending to be the human
reviewer so we can preserve exactly the same process at higher speed. **That's automating the ceremony
rather than questioning why the ceremony exists**"*
([[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]]). Her alternative is to relocate what review
is *for* — knowledge transfer, architectural alignment, collective ownership — into pairing, team design
sessions and [[fitness-functions]], and then review by exception. Both belong here and the KB does not
pick: Anthropic's version is the automate-the-gate position **with a trust ladder** (per-file evidence
that the automated reviewer catches everything, plus an eval-set regression guard after each incident),
which is precisely the evidence Laycock's objection would demand — and it is also a **vendor team
reporting on its own tool**, while she is Thoughtworks' CTO on Thoughtworks' own channel and offers no
data at all. The full five-way argument, including
[[tornhill-controlling-the-uncertainty-machine|Tornhill's]] uncertainty triage and
[[willison-more-than-just-code-review|Willison's]] "eyeballing every line was never the best
verification," is on [[verification-burden]]; the resource ceiling under it is on
[[attention-bottleneck]].

## Does the loop sit above the harness, or inside it? (unresolved)

This page opens by placing loop engineering *"one floor above the harness,"* following
[[addyosmani-loop-engineering|Osmani]]. That ordering is contested, and the contest is not merely
verbal — it decides where you put a policy.

- **Loop above harness** — [[addyosmani-loop-engineering|Osmani]] and
  [[wong-loop-engineering-teaching-ai-agents-how-to-think|Wong]]: *"A harness governs one step. A loop
  governs the campaign."* The harness's own guard stops one step spinning; the loop's stop rules end the
  whole campaign.
- **Harness above/around loop** — [[morris-humans-and-agents-in-software-engineering-loops|Morris]],
  **2026-03-04**, five months earlier: *"The collection of specifications, quality checks, and workflow
  guidance that control different levels of loops inside the how loop **is** the agent's harness. The
  emerging practice of building and maintaining these harnesses, Harness Engineering, **is how humans
  work on the loop**."* On this reading harness engineering is not a lower floor; it is the human's work
  at the loop's boundary. *(**NOT INDEPENDENT** — Thoughtworks author, Thoughtworks series, arguing for a
  Thoughtworks-coined term.)*
- **The loop is the small core; the harness is the world** —
  [[breunig-harnesses-are-situated-agents|Breunig]]: Harrison Chase's four agent elements (system
  prompt, planning tool, file system, subagents) *"describ[e] the core loop… the core loop the developer
  controls with the keyboard. The **harness** manages everything beyond this, the world the developer sits
  within."*

**The sharpest evidence is a product.** Breunig notes that Cloudflare's **Flue** uses a declarative
pattern that **"hides the loop from users"** — and Flue's creator, in
[[macmanus-schott-react-for-agents-flue-meta-harness]], states the corollary directly: *"Our early bet
was that the harness is actually not a feature, but it's fundamental to what you think an agent is.
**There is no agent without a harness.**"* If the loop can be abstracted away as an implementation detail
of a declarative harness, then "loop engineering" may name a **current tooling gap** rather than a
permanent layer — which is also, from the opposite direction,
[[voss-what-the-hell-is-a-loop-anyway|Voss's]] point that *"nobody designs the token loop."* Unresolved;
do not smooth it over.

## Relationship to neighbours

- **[[harness-engineering]]:** loop engineering is strictly *above* it *on this page's opening reading* —
  the harness makes one run reliable; the loop runs the harness on a timer, in parallel, and feeds its own
  improvement. Osmani's "factory model" sense of the harness is the unit the loop multiplies. **But three
  of five definitional sources invert this ordering** — see the layering-dispute section above; do not
  treat the "strictly above" as settled.
- **[[ralph-loop]]:** the original "keep going across context windows" pattern is the **agent loop**
  (level 1) made persistent — a primitive loop engineering composes, not the whole stack. (For
  [[voss-what-the-hell-is-a-loop-anyway|Voss]] it is instead a *distinct architecture*, his **task loop**,
  with its own exit condition rather than a persistent version of the innermost one — see
  [[ralph-loop]].)
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
  a diagram." Note that two independent 2026 surveys place the rungs differently — see
  [[graph-engineering]].)

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

## The task list is the hard part — and Event Modeling supplies it (Dilger, 2026-06-10)

[[dilger-loop-engineering-never-argue-with-agent]] is this page's Event-Modeling entry, and it answers
the page's own standing question — *what supplies the task list?* — with one sentence:

> "The hard part in Loop Engineering is not implementing the loop, it's defining the list of tasks. In
> Event Modeling this happens naturally and is part of the process. **Every 'slice' of functionality
> becomes a task.**"

**Chronology correction this ingest establishes:** the KB dates the *Event Modeling Agent Harness* to
[[dilger-event-modeling-agent-harness]] (2026-06-17). **This article is a week earlier (06-10)** and
already carries the whole mechanic, so the idea's date should move to 2026-06-10 and 06-17 read as the
restatement.

**The loop, minimally:** define a task list; run tasks one at a time; **record what you learned after
each**; then **clear the context completely** — *"No bias. No bad decisions lingering. No wrong
information. Just the learnings - and the next task."* Provenance he states himself: he read Geoffrey
Huntley in **2025**, dismissed the [[ralph-loop|RALPH loop]] (*"running an agent in a loop?
Nonsense"*), then realised he was already doing it. He also frames loop engineering as *"the 'new
thing' after Spec-Driven Development"* — his own ordering of the two disciplines.

**"I never argue with an agent."** *"Every agent will immediately tell you how right you are. That's not
learning. That's hand-waving agreement… The agent isn't learning from your corrections. It's just
agreeing with you - and carrying the confusion forward."* Operationally: each iteration has defined
goals and rules, and **a broken rule ends the iteration with no discussion** — discard everything except
the learnings and retry. His mechanism claim for why — *"confusion is what produces hallucination. It's
not a random event. It's the predictable result of a polluted context window"* — is **asserted with no
evidence**; the KB holds better-evidenced versions at [[context-rot]].

**Do not engineer the loop.** Asked to make an agent stop, revert and restart when its task changes
mid-flight, his answer is that the loop already handles it: *"The moment you start overengineering it -
adding more state, more memory, more decision-making between iterations - you start reintroducing
exactly the problems the loop was designed to eliminate. You're building back the noise. Simplicity
isn't a limitation of loop engineering. It is loop engineering."* **This is a direct counter-position to
the elaboration this page documents elsewhere** — LangChain's four stacked loops, Osmani's five
primitives plus four memory channels, Miracle's trust ledger and three sequenced gates. Dilger's claim is
that the machinery is mostly compensating for a missing task list. Both positions are now on this page
and the KB does not pick between them.

**The board as the loop's control surface** (the concrete mechanism, and the fullest statement of it in
the KB): slices carry status; **Planned** means an agent may claim it; agents subscribe to
`slice:changed` (Claude Code, Codex and Hermes named); a claiming agent moves it to **In Progress**,
which **locks it against other agents**. Three terminal outcomes: **Done**; **Blocked**; or **the agent
dies, the slice times out in progress, and another agent picks it up** — the timeout being what makes an
unattended fleet safe to leave running ([[unattended-coding-agents]], [[long-running-agents]]). Editing
finished work: move Done → In Progress, edit, move to Planned, and an agent **diffs the specified slice
against the code and reconciles the code to the spec**. Hints go in **comments on the slice**, which the
agent checks off. *"There's no manual prompting involved. Just change a slice and wait until the agent
did the work."*

**The load-bearing claim, and the batch's cleanest disagreement.** *"If something fails, the problem is
in the spec, not the prompt."* That is [[spec-driven-development]]'s thesis stated as a debugging rule —
and it is exactly what the SDD sceptics deny.
[[eberhardt-putting-spec-kit-through-its-paces|Eberhardt]] hit a trivial unpopulated-variable bug and
*"asked Copilot, and it concurred, this isn't an issue with the spec"*;
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill's]] requirements-explosion argument
says most defects **cannot** be spec defects, because the spec cannot contain the implicit design
decisions. Whether loop failures are spec failures is now a live, testable question this page should
carry as open.

*(**VENDOR SELF-REPORT** — eventmodelers.ai/EM-Studio is Dilger's own platform; every mechanism above is
one of its features, and the piece closes selling his book, the build-kits and paid training
(*"as I did for hundreds of engineers already"* — **his own figure**). **No evidence of any kind**
appears in it, and the central claim is stated absolutely: *"Clean iterations with recorded learnings
will outperform long, polluted conversations every single time. Not sometimes. Every time."* Carry that
as a position, not a finding.)*

## Three supervisors, three things being supervised (Sept 2026)

A distinct role keeps appearing beside the loop — a second process whose job is not the task but *whether
progress is still happening* — and three unrelated sources now instantiate it at different levels:

- **The trajectory.** NVIDIA's AVO supervisor *"monitors the broader trajectory for stagnation or repeated
  unproductive cycles and can redirect the main agent toward alternative strategies"*, while the main agent
  keeps deciding what to inspect, change, test and evaluate — across a **seven-day** run
  ([[fowler-fragments-2026-09-01]]; **VENDOR SELF-REPORT, secondhand**).
- **The verification environment.** [[jeremy-miller]]'s "Bobcat" supervises test runs and does *"selective
  test retries, process restarts, and even hard Docker resets based on known test flakes"*, because *"heavy
  development can break down when Docker containers have run too long in tests"*
  ([[miller-pondering-continuous-integration-ai-world-order]]; his own tool, *"hugely helpful"*,
  unquantified).
- **The agent's earned autonomy.** Miracle's trust-level statusline and termination rules
  ([[miracle-my-loop-engineering-workflow]]) supervise *how much rope the loop gets*, not whether it is
  stuck. **Configuration, not evidence** — see §0 of the Batch C deltas.

**Worth separating deliberately:** stagnation detection (is the search still productive?), environment
hygiene (is the harness still healthy?) and trust accounting (should this loop continue at all?) are three
different questions with three different signals, and this page currently discusses only stop *conditions*
— which answer none of them. The AVO case is also the only one where the supervisor can **change the
strategy** rather than halt or retry.

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

Newly open from Batch C: **does "a loop" name one construct or several?** — three mutually incompatible
fourfold taxonomies are now captured (LangChain, Anthropic, Voss) plus two more definitions that fit none
of them (Wong, Miracle); and **is the harness below the loop or around it?** — three of five definitional
sources invert this page's stated ordering, with Cloudflare's Flue *hiding the loop entirely* as the
hardest evidence that the layering is a tooling artefact rather than a fact.

- **Is loop failure spec failure?** [[dilger-loop-engineering-never-argue-with-agent|Dilger]] asserts
  *"if something fails, the problem is in the spec, not the prompt"* and rebuilds his whole workflow on
  it. [[eberhardt-putting-spec-kit-through-its-paces|Eberhardt's]] broken dev server and
  [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill's]] requirements explosion both
  say a large class of defects cannot be spec defects. Nobody has classified a real run's failures
  against that distinction — and it is cheap to do.
- **Does the loop need machinery, or a task list?** The page documents steadily more elaborate loop
  stacks; Dilger's position is that elaboration is compensating for the absence of a well-formed unit of
  work, and that a [[slice]] supplies one. Both cannot be right about the same workloads.

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

_Sources: [[bockeler-tdd-inside-the-agent-loop]] · [[dilger-describing-without-solving-burns-you-out]] · [[addyosmani-loop-engineering]] · [[langchain-the-art-of-loop-engineering]] · [[swyx-loopcraft-art-of-stacking-loops]] · [[willison-designing-agentic-loops]] · [[anthropic-getting-started-with-loops]] · [[willison-rewriting-bun-in-rust]] · [[addyosmani-own-the-outer-loop]] · [[ahe-agentic-harness-engineering]] · [[addyosmani-earning-taste-and-judgment]] · [[addyosmani-software-factories-light-and-dark]] · [[willison-fireside-chat-claude-code-team]] · [[willison-vibe-engineering]] · [[khononov-microservices-hype-to-ai-sloop]] · [[prefect-loops-vs-graphs]] · [[voss-what-the-hell-is-a-loop-anyway]] · [[wong-loop-engineering-teaching-ai-agents-how-to-think]] · [[miracle-my-loop-engineering-workflow]] · [[morris-humans-and-agents-in-software-engineering-loops]] · [[breunig-harnesses-are-situated-agents]] · [[addyosmani-practical-loop-engineering]] · [[addyosmani-human-judgment-relocates]] · [[addyosmani-code-agent-orchestra]] · [[addyosmani-agentic-code-quality]] · [[macmanus-schott-react-for-agents-flue-meta-harness]] · [[macmanus-pocock-wayfinder-skill-fog-of-war]] · [[wang-rethinking-evaluation-of-harness-evolution-for-agents]] · [[evo-bench-can-language-models-improve-agent-harness]] · [[sbco-verifier-grounded-harness-optimization]] · [[harnessx-composable-adaptive-evolvable-agent-harness-foundry]] · [[harnessforge-joint-harness-and-policy-evolution]] · [[mcateer-evolution-of-the-agent-harness]] · [[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]] · [[willison-more-than-just-code-review]] · [[tornhill-controlling-the-uncertainty-machine]] · [[dilger-loop-engineering-never-argue-with-agent]] · [[nick-tune-event-sourced-claude-code-workflows]] · [[fowler-fragments-2026-09-01]] · [[miller-pondering-continuous-integration-ai-world-order]]._
