# Ingest deltas — Batch C: loop engineering and agentic practice

**Written 2026-09-04. 18 raw captures compiled into 18 source pages in `wiki/sources/`.**
This file is the work order for the orchestrator. Nothing in `wiki/entities/`, `wiki/concepts/`,
`wiki/index.md`, `wiki/overview.md` or `wiki/log.md` was touched by this batch.

**Source pages written** (all with `raw_file:` set):
`voss-what-the-hell-is-a-loop-anyway` · `wong-loop-engineering-teaching-ai-agents-how-to-think` ·
`wong-graph-engineering-wiring-agents-into-an-organization` · `miracle-my-loop-engineering-workflow` ·
`morris-humans-and-agents-in-software-engineering-loops` · `breunig-harnesses-are-situated-agents` ·
`breunig-fable-and-the-end-of-the-free-lunch` · `breunig-who-taught-the-models-to-do-that` ·
`edwards-alexander-an-accidental-blackboard` · `addyosmani-practical-loop-engineering` ·
`addyosmani-human-judgment-relocates` · `addyosmani-code-agent-orchestra` ·
`addyosmani-agentic-code-quality` · `osmani-ai-wont-teach-you-the-lesson-unless-you-force-it` ·
`macmanus-prs-not-welcome-software-factories` · `macmanus-schott-react-for-agents-flue-meta-harness` ·
`macmanus-pocock-wayfinder-skill-fog-of-war` · `zalando-agentic-engineering-snapshot`

**Delta items: 34** (24 concept UPDATEs, 1 concept CREATE, 3 entity UPDATEs, 6 entity CREATEs) plus a
closing note on `index.md` / `log.md`, which this batch does not own.

**Standing instruction for every paste below:** the interested-claim markers are *inside* the pasted
text on purpose. Do not strip them when placing the text, and do not let a figure travel to a third
page without its marker. Section 0 lists every number in this batch that must not be promoted.

---

## 0. Numbers this batch refused to promote — apply on any page that cites them

Not a page edit. A checklist for the fidelity pass and for any future page that reaches for these.

| Figure | Source | Why it is not a datum |
| --- | --- | --- |
| AI SDK factory "authors 25–35% of merged PRs, closes 70–80% of issues" | `macmanus-prs-not-welcome-software-factories` | **VENDOR SELF-REPORT.** Vercel on Vercel, relayed second-hand, **four weeks after implementation**, no methodology, no regression or reopen data. |
| `AGENTS.md`: LLM-generated "~3% success reduction, 20%+ inference cost"; developer-written "~4% improvement" | `addyosmani-code-agent-orchestra` | **UNCITABLE.** Presented as research but **no study is named or linked anywhere in the page**. The *practice* (human-curated only) may be carried; the three figures may not. |
| "Parallelism (3x throughput)", "3–5 teammates is the sweet spot", "three focused agents outperform one generalist working 3x as long", "substantially cuts stuck agents", token budgets 180k/280k, "roughly 220k tokens total" | `addyosmani-code-agent-orchestra` | **IMPRESSION NOT MEASUREMENT.** Practitioner judgement plus four demo videos on a toy bookmarks app. |
| "It's totally shifted in the last six months"; "never seen that in my entire decade-plus" | `macmanus-prs-not-welcome-software-factories` | **IMPRESSION NOT MEASUREMENT.** Never render as a figure or a rate. |
| Zalando: "33% of our PRs are low-risk and are auto-approved"; "reduced PR lead time by 20–40%" | `zalando-agentic-engineering-snapshot` | **VENDOR SELF-REPORT** (Zalando on Zalando's own bot). The lead-time figure is *"compared with all PRs"* — a **selection-biased comparison**; low-risk PRs would merge faster anyway, so the delta is not attributable to the bot from what is published. |
| Zalando's CCN / PR-size / commit-message inflection points | `zalando-agentic-engineering-snapshot` | **Four codebases, no control arm**, agent adoption partly inferred from inconsistent `Co-authored-by` markers, all four figures are untranscribed images. Illustrative, not causal — as the author presents them. |
| Opus 4.1 reward hacking "52% → 18%", "65% less likely… if you simply asked it not to" | `breunig-who-taught-the-models-to-do-that` | **VENDOR SELF-REPORT.** Anthropic's own figures, own model, own system card, own internal benchmark, no replication — *and* the delta sits inside a programme of other post-training changes. |
| Anthropic "65% of its product team's code" via Claude Tag; Warp "ratcheting auto-merge from 20% toward 60%" | `voss-what-the-hell-is-a-loop-anyway` | **VENDOR SELF-REPORT, relayed.** The Warp figure is a stated *target path*, not an achieved result. |
| Osmani's 82-minute factory run; "7 minutes" vs "56 minutes"; "two to four times as long" | `addyosmani-human-judgment-relocates` | **IMPRESSION NOT MEASUREMENT.** One unoptimized run of a movies demo by the reference repo's own author. |
| "5–10 agents daily", "80–90 PRs/day", "80,000 stars"; Pocock's "220,000 stars / 347,000 subscribers"; Astro 62k / tldraw 50k stars; AI SDK 20M npm downloads | Osmani, Pocock, MacManus pieces | **Workload and popularity, not efficacy.** Never cite as evidence that a practice works. |
| Miracle's trust-ledger quantities (50/100 start, Fibonacci 2/3/5/8/13/21, terminate <20), `MAX_ITERATIONS=8`, "nine packets / twenty plans" | `miracle-my-loop-engineering-workflow` | **Configuration, not evidence.** No outcome is measured; the ledger's efficacy is argued from first principles. |
| Breunig's model price ratios ("~1/9th the cost", "~1/5th of Opus 5") | `breunig-fable-and-the-end-of-the-free-lunch` | Asserted with **no source**, and the quality comparison is an explicit shrug. Date-bound to Aug 2026. |

---

## 1. `wiki/concepts/loop-engineering.md` — UPDATE (7 items)

The page is the KB's largest and this batch changes its **frame**, not just its content. Items 1.1–1.3
are the load-bearing ones; do them in order.

### 1.1 — CREATE a new section laying out the competing definitions side by side

**Why:** the page currently presents LangChain's four-loop stack and Anthropic's four loop *types* as a
"near-exact cross-map," i.e. as a settled taxonomy. This batch adds a **third fourfold taxonomy that
does not line up with either**, plus two more definitions that are incompatible with all of them. Do not
merge them. The disagreement is the content.

**Where:** insert as a new `##` section **immediately after** the existing section
`## Earlier origin — Willison, Sept 2025` and **before**
`## The Salty Lesson`.

**Paste:**

```markdown
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
```

### 1.2 — CREATE a section on the loop/harness layering dispute

**Why:** the page states one ordering as settled. Three of this batch's five definitional sources invert
it, and one of them (Morris) predates the coinage the page relies on.

**Where:** insert as a new `##` section **immediately before** the existing
`## Relationship to neighbours`.

**Paste:**

```markdown
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
```

### 1.3 — CORRECT the provenance paragraph (Morris predates the June-2026 coinage)

**Why:** the page dates the vocabulary to June 2026 with Willison (Sept 2025) as the sole earlier origin.
Morris has *on-the-loop* and *the agentic flywheel* on **2026-03-04** — four months before Osmani's
"Own the Outer Loop" and three before LangChain's hill-climbing loop, both already on this page.

**Anchor — the existing sentence:**

> The coinage is June 2026 ([[swyx-loopcraft-art-of-stacking-loops|swyx's "Loopcraft"]]), crystallized in
> three practitioner quotes:

**Action:** leave that sentence and its three quotes intact; **append the following paragraph directly
after the three-quote list** (i.e. immediately before `## Earlier origin — Willison, Sept 2025`).

**Paste:**

```markdown
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
```

### 1.4 — CORRECT what the `/goal` evaluator actually does (two places)

**Why:** the page twice credits `/goal`'s evaluator with being maker≠checker applied to "done." Osmani,
who uses it daily, says explicitly that it **never looks at content**. The KB is crediting the instrument
with more than it does, and the back-pressure argument depends on knowing which instrument checks what.

**Anchor A — in `## The five primitives + memory ([[addyosmani-loop-engineering|Osmani]])`, primitive 1,
the existing parenthetical:**

> (`/loop` re-runs on a cadence; `/goal` runs until a verifiable stop condition holds, with a
>   *separate* model grading the stop — maker≠checker applied to "done.")

**Action:** replace that parenthetical with:

```markdown
(`/loop` re-runs on a cadence; `/goal` runs until a verifiable stop condition holds, with a *separate*
  evaluator model grading the stop. **Note what that evaluator is not:** per
  [[addyosmani-practical-loop-engineering|Osmani, 2026-08]], *"The evaluator sitting behind goal is not
  that checker… **It doesn't look at the content** to see if it's good or bad in any way, shape, or form.
  All it does is **examine the conversation transcript** to see if the hard rules you specified have been
  met."* It is a **stop-condition referee, not an output reviewer** — so it is not maker≠checker in the
  quality sense, and a separate verifying sub-agent is still required.)
```

**Anchor B — in the Anthropic loop-type table row:**

> | **Goal-based** | manual → goal met OR turn cap | `/goal` (a *separate evaluator model* grades the stop) | verification / grader loop |

**Action:** replace that row with:

```markdown
| **Goal-based** | manual → goal met OR turn cap | `/goal` (a *separate evaluator model* grades the stop — **transcript against stated rules only, not output quality**) | stop-condition referee, *not* the verification loop |
```

### 1.5 — ADD Osmani's practical section: what loops are for, and what they are not

**Where:** insert as a new `##` section **immediately after** the existing
`## The five primitives + memory ([[addyosmani-loop-engineering|Osmani]])`.

**Paste:**

```markdown
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
```

### 1.6 — ADD Miracle's rig as the batch's worked practitioner topology

**Where:** insert as a new `##` section **immediately after** the new section from item 1.5.

**Paste:**

```markdown
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
```

### 1.7 — Frontmatter and footer

**Action:** add to `sources:` (append, preserving existing order):
`voss-what-the-hell-is-a-loop-anyway, wong-loop-engineering-teaching-ai-agents-how-to-think, miracle-my-loop-engineering-workflow, morris-humans-and-agents-in-software-engineering-loops, breunig-harnesses-are-situated-agents, addyosmani-practical-loop-engineering, addyosmani-human-judgment-relocates, addyosmani-code-agent-orchestra, addyosmani-agentic-code-quality, macmanus-schott-react-for-agents-flue-meta-harness, macmanus-pocock-wayfinder-skill-fog-of-war`

Bump `updated: 2026-09-04`. Add the same slugs to the trailing `_Sources: …_` line.

**Also, in `## Open questions`, append this sentence:**

```markdown
Newly open from Batch C: **does "a loop" name one construct or several?** — three mutually incompatible
fourfold taxonomies are now captured (LangChain, Anthropic, Voss) plus two more definitions that fit none
of them (Wong, Miracle); and **is the harness below the loop or around it?** — three of five definitional
sources invert this page's stated ordering, with Cloudflare's Flue *hiding the loop entirely* as the
hardest evidence that the layering is a tooling artefact rather than a fact.
```

---

## 2. `wiki/concepts/agent-harness.md` — UPDATE (restructure; 2 items)

The page is one of the KB's thinnest (a components list plus architecture patterns) and **cannot carry
this batch's definitional material as-is.** Recommend adding the two sections below and, if the page
still reads thin afterwards, treating the shape as the problem rather than adding more sources.

### 2.1 — ADD Breunig's eight-layer "situated agent" model

**Where:** insert as a new `##` section **immediately after** the existing
`## Core components / primitives` (so the flat inventory is followed by the gradient that organises it).

**Paste:**

```markdown
## A harness is a "situated agent" — eight layers ([[breunig-harnesses-are-situated-agents|Breunig, 2026-08-14]])

The KB's strongest definitional framing for this page since Böckeler's guides/sensors. Breunig keeps
Harrison Chase's four elements of an agent — **system prompt, planning tool, file system, subagents** — as
*"the core loop the developer controls with the keyboard,"* and defines the **harness as everything
beyond it: "the world the developer sits within."* Zoom out from one agent at the keys and the harness
manages:

1. **Session** — the current task and context, *"as both a trajectory and a durable, branchable log. You
   can zoom backwards, fork, and replay it."*
2. **Environment** — the instance: sandbox, terminal, worktree, computer, container.
3. **Repo** — the project: code, history, current work, `AGENTS.md`, guides, hooks, versioned in Git.
4. **Memory** — *"the person's predilections, accrued over time, managing progress and past decisions."*
5. **Skills** — the domain: reusable workflows or domain knowledge *"worth wielding in this situation."*
6. **Team** — colleagues: shared rooms, shared traces, project tracking, issues, bug reports.
7. **Organization** — *"the policies and audits, defined by legal, leadership, and procurement."*
8. **Model** — the LLMs, *"the common artifact shared by all."*

**The ordering rule is the genuinely new idea:** *"As we move outward, each layer is used by more people
and changed less often."* That converts a flat inventory into a **rate-of-change gradient**, which is what
you need in order to decide *where a given policy belongs*. Compare
[[langchain-anatomy-of-an-agent-harness]] and [[firecrawl-what-is-an-agent-harness]], both of which stop
at the Repo layer — the KB had no place for Team, Organization or Model before this.

**What a harness does, in one line:** *"Harnesses account for the above layers, fanning out from the
agent, to determine what ends up in the context, how the loop runs, and what gets saved."*

**The Aug-2026 census, worth dating because it will age fast:** **Omnigent** (Databricks) — a
*meta-harness* calling out to Claude Code, Codex, Pi and others; **DeepSeek Harness** — *"totally
modular: models, tools, skills, sessions, sandboxes, storage, loops, scheduling, and the UI are all
swappable"*; **Buzz** (Block) — a Nostr social network for agents and humans; **QM** (Y Combinator) —
**org-shaped scoping**, where *"each employee, Slack room, and project gets its own memory, files,
credentials, permissions, schedules, and sandboxed execution"*; **Flue** (Cloudflare) — declarative, and
it **hides the loop from users**; **Muse Code** (Meta) — model **co-trained with the harness itself**;
plus OpenClaw, NanoClaw, Hermes, Conductor, Prime Agent. Breunig's read: *"they're more alike than
different,"* with innovation happening **per layer**.

**Two consequences the KB should carry.** (1) **Stickiness.** *"It's trivial to jump from Claude Code to
Codex… but if the entire org and team have already set up a system that manages all of the above, it's
really hard to shift… It's going to be funny if the network effects the AI labs have been searching for
end up looking just like the network effects of the SaaS era."* (2) **Model-harness co-training may be
routine and undisclosed** — on Meta training Muse Spark to know its harness, *"much like others, they just
don't write about it…"* If true, that complicates every benchmark claiming to isolate harness quality
from base-model strength, including [[ahe-agentic-harness-engineering|AHE]]'s frozen-model design. An
unevidenced aside; carry it as an open question, not a refutation.

*(Limits: a ~870-word opinion post, no measurement; the census is a list of launch announcements, mostly
from vendor blogs, none evaluated; the lock-in claim is an unfalsified prediction. The cited companion
"Overfitting the Harness" (2026-05-10) is **not in `raw/`**, so the co-training aside cannot be followed
from this capture.)*
```

### 2.2 — ADD "there is no agent without a harness" and the two framework generations

**Where:** insert as a new `##` section **immediately after** the new section from 2.1.

**Paste:**

```markdown
## "There is no agent without a harness" ([[macmanus-schott-react-for-agents-flue-meta-harness|Schott, 2026-08-15]])

The strongest statement of harness-primacy in the KB, from someone who bet a product on it. Fred Schott
(creator of Astro; Cloudflare) on **Flue**: *"Our early bet was that **the harness is actually not a
feature, but it's fundamental to what you think an agent is. There is no agent without a harness.**"*
And its corollary: *"Instead of you and your code driving the LLM and telling it what to do with scripts,
**you're putting the agent into this harness, and it is able to drive itself and work through
problems**."*

- **Two generations of agent framework, distinguished by whether the harness was designed in.** The
  *"OG agent frameworks"* — Vercel's AI SDK, Cloudflare's own Agents SDK, Mastra — *"weren't created with
  a harness as the central concept"* and are adding harnesses now as **a feature**; Flue and Vercel's
  **eve** both have them built in. *(A vendor's competitive characterisation of competitors, not an
  audited one.)*
- **Flue is an opinionated take on Pi, an open source minimal harness** — the relation Vite has to Astro:
  *"it doesn't do too much, but it gives the right APIs."* A useful two-tier split for this page:
  **minimal harness** vs **opinionated framework over it.**
- **"Meta-harness" is not yet a defined term**, per someone selling in the category: *"there's confusion
  about what the term meta-harness even means at this early stage."* Schott declines a
  one-API-across-all-harnesses design because *"the framework and the harness are very intertwined."*
- **Hooks: a mechanism for the dynamic capability this page only asserts.** An agent is a JavaScript
  function that *"re-renders on every turn"*; 16 built-in hooks including `useSkill()`, `useTool()`,
  `useSubagent()` *"attach different resources and capabilities dynamically to enhance themselves at
  runtime."* His motivating example is a **security** pattern: a support agent *"might bring in an
  account management tool **after first verifying a user**"* — capability scoping **by lifecycle stage**,
  which is [[prefect-loops-vs-graphs|Lowin's]] per-node scoping ("don't hand your agent a bazooka")
  implemented *inside* one agent instead of across graph nodes.
- **A design lesson worth generalising:** *"file based magic is an antipattern."* Flue 1 ported
  file-based routing from web frameworks and it failed, because the unit turned out to be different —
  *"for a lot of people building with Flue, especially the bigger customers, **their whole company is one
  agent**. They don't care about routing."* A caution for every borrowed abstraction in this space,
  including React's, which Schott is now borrowing.
- **Period marker.** Bret Taylor (Sierra CEO, OpenAI chairman), quoted in the same piece: *"We're sort of
  in the **jQuery era of agents**, not the react era."*

*(Vendor launch interview: no benchmark, no adoption figures, no independent user reports. Flue 2 is its
first stable release; the whole framework census is date-bound to Aug 2026.)*
```

**Frontmatter:** add `breunig-harnesses-are-situated-agents, macmanus-schott-react-for-agents-flue-meta-harness, breunig-fable-and-the-end-of-the-free-lunch` to `sources:`; bump `updated: 2026-09-04`; extend the `## Related` list with those slugs.

---

## 3. `wiki/concepts/software-factory.md` — UPDATE (4 items)

### 3.1 — ADD the "do you actually need one yet?" test, near the top

**Why:** the page presents the factory as the rung above the loop with **no threshold for entering it**.
Osmani supplies one, and his prior is "probably not yet."

**Where:** insert as a new `##` section **immediately after** the existing `## The wiring diagram` and
**before** `## Light vs dark`.

**Paste:**

```markdown
## Do you actually need a factory yet? ([[addyosmani-human-judgment-relocates|Osmani, 2026-08-21]])

The prior question this page never asks. *"**In my experience, you can get surprisingly far with your
stock coding harness!**"* — Claude Code or Codex, multiple sessions, good SPECs with verification baked
in, constraints, *"you can even throw a batch of GitHub issues at them with implementation and
human-involvement criteria."* And the blunt version: *"You may be fine. Your work may actually be totally
fine without needing a factory."*

**The threshold:** *"Add a software factory when you need an **event-driven queue of work** (e.g. Slack
triggers, GitHub issues, Linear, a backlog) to run in an **isolated cloud environment** to handle triage,
implementation and testing with some explicit human babysitting."* I.e. the trigger is **repeatability +
event-driven-ness**, not scale or ambition.

**And what it actually buys, which is unglamorous:** *"The factory becomes useful when the hard part is
making your different runs behave consistently, handing work off between agents and **avoiding different
sessions from claiming the same issue**, preserving evidence and **stopping production when human review
is falling behind**."* Note the last clause: **throttling itself against reviewer capacity is part of the
factory's job**, not an external control.

**The factory's real interface is a mutable label on a work item.** Warp triages every incoming issue
into **ready-to-implement / ready-to-spec / needs-info / wait-to-implement**, *"and the label is what
fires the next agent."* Osmani: *"This label does a few jobs in one go: **it's the queue, the lock** and
since a session only picks up what's marked ready, it's **where a human can park stuff without saying no
permanently**."* Queue, mutual exclusion and deferral in one field — and
[[macmanus-prs-not-welcome-software-factories|Astro's and Flue's]] PR-to-issue conversion is that parking
spot made mandatory.

**Four ways a human participates**, beyond approving a final diff: **shape** (early), **steer**
(mid-implementation redirect), **handoff** (move task + state + context between cloud factory, another
agent, or a human reviewer — *"Good handoffs will keep track of what happened, whats left to be done and
why the handoff is needed"*), **approve/stop**. Plus **notifications** as *"how the factory says it's
blocked."*

Building is not the only option: *"Standing up the infra to scale a factory can be a lot of work and you
may want to consider buying vs. building"* — Factory, Warp and HumanLayer are named.

*(Practitioner essay; no measurement. The **82-minute factory run** and its per-task timings — 7 minutes
for one feature, 56 for another — are **IMPRESSION NOT MEASUREMENT**, one unoptimized run of a movies demo
app by the reference repo's own author. All Vercel and Warp figures are **VENDOR SELF-REPORT**, cited
second-hand.)*
```

### 3.2 — ADD run classification, the cost gap, and the blocked-state gap

**Where:** insert as a new `##` section **immediately after** the existing
`## Back pressure — the governing rule`.

**Paste:**

```markdown
## Classifying runs — and the two things classification misses ([[addyosmani-human-judgment-relocates|Osmani, 2026-08]])

Vercel marks every agent run **success / flawed / blocked / manual**, and *"only 'success' ships to
production. The rest re-enter the system."* Osmani's reading: **flawed** = wrong thing implemented, or it
lacked context; **blocked** = the environment was missing a credential; **manual** = *"a boundary the
factory may not be allowed to cross it yet."* *"Two of the three things here may have mechanical fixes and
**the last one is about trust**."* *(**VENDOR SELF-REPORT** — Vercel's own scheme for its own factory,
cited second-hand.)*

**Gap 1 — the taxonomy has no cost term.** *"While this is great, what sorting doesn't show you is cost…
So I'd **pair the taxonomy with per-stage timing**, otherwise you know a run came back flawed without
knowing what finding out cost you."* This is the measurable form of his own **"number of checks !=
quality"** rule, and the missing metric behind
[[dilger-real-cost-of-ai-is-second-order|Dilger's second-order cost]]. He also proposes **cost per merged
PR** and **code shelf life** as [[comprehension-debt]] metrics (proposals, not results).

**Gap 2 — a blocked run has no named re-entry point, and this is a design defect nobody else raises.**
*"My sample factory stopped [at] the first issue and moved it to `factory:needs-info`, which was right,
**but I didn't know where to put my answer**. **A manual run isn't finished when the factory stops but
when the human knows what to do next.**"* Not a verification problem and not an autonomy problem — an
**interface** problem. It is the same requirement
[[wong-graph-engineering-wiring-agents-into-an-organization|Wong]] states as *"make failure an explicit
edge"* and *"turn human approval steps into real graph nodes with defined edges in and out, not a
side-channel Slack message."*

**And a security requirement specific to factories: the queue is untrusted input.** *"If your factory
reads untrusted input like a GitHub issue/Slack message it might be adversarial and include problems like
supply chain attacks."* Vercel's mitigation is per-task least privilege — *"run their agents in isolated
sandboxes holding just the secrets a task needs. That way a compromised run can't reach what the job
doesn't need"* — the same shape as QM's per-project credential scoping in
[[breunig-harnesses-are-situated-agents]] and [[prefect-loops-vs-graphs|Lowin's]] per-node tool grants.
See [[prompt-injection]].
```

### 3.3 — ADD provenance-based trust (the reframing, and its failure mode)

**Where:** insert as a new `##` section **immediately after** the section added in 3.2.

**Paste:**

```markdown
## Provenance-based trust — a third acceptance mechanism ([[macmanus-prs-not-welcome-software-factories|MacManus, 2026-09-01]])

Four AI-native open source projects — **Vercel's AI SDK, Astro, Flue, tldraw** — are replacing drive-by
community PRs with maintainer-owned factories; **Flue and tldraw automatically close every external PR**
and convert it to an issue or discussion. The interesting claim is **why**, and it is not code quality.

Vercel engineer Lars Grammel: *"If we have a very specific agent with a very specific prompt that we
optimized — and we know that, over history, it was very successful in fixing a certain category of bugs —
then **we develop trust in that particular agent configuration**… For open-source projects, it's worth
considering having your own agents and your own setup, and **not necessarily trusting the community**,
because it can actually cut down your time to review."*

**That is the maker-checker argument reframed as a PROVENANCE argument, and it is a mechanism the KB has
not named.** The KB's acceptance vocabulary has two moves — *check the artifact* (tests, sensors, gates)
and *use a different checker than the maker*. This is a third: **accept a change because of what produced
it**, on the strength of a per-bug-category track record. It is the logic of a signed build or a trusted
CI runner, applied to an agent configuration. Steve Ruiz (tldraw) states the condition it rests on:
*"It just makes less sense to have people contributing code **if the issue is decently well-specified and
the code can be written by agents**"* — so the mechanism is parasitic on
[[spec-driven-development|spec quality]]. [[mitchell-hashimoto|Hashimoto]] pushes it further: *"the future
is that large open source projects will close contributions completely."*

**The failure mode nobody in the piece raises:** a configuration's track record is **retrospective**, and
the thing being trusted is a prompt that can be edited. Provenance trust with no versioning of the
configuration, and no re-validation after an edit, is trust in a moving target. Note also that tldraw's
stated drivers are broader than agent quality — *"changes in how we're coding (more discussion, more
agents), **the social practices around public contribution**, and **the changing landscape around code
security**"* — only one of the three is about agents being good.

**The cost, conceded by a participant.** PRs were how maintainers were grown: *"pull requests have been
reviewed by maintainers not only for the code, **but to teach contributors and assess them as future
maintainers**."* Fred Schott: *"It still leaves this open hole of, well, if you just keep narrowing the
project, at a certain point, you and I go on vacation — what happens?"* The partial answer both projects
offer is that issues and discussions stay open, so trust-building moves to conversation — Ruiz: *"it's
better to limit community contribution to the places it still matters: **reporting, discussion,
perspective, and care**."* See [[comprehension-debt]] for this as the institutional level of the
skill-decay problem.

*(**VENDOR SELF-REPORT, four weeks in, unaudited:** Vercel's claim that the factory *"authors between 25
and 35% of PRs we merge and closes 70-80% of issues."* **IMPRESSION NOT MEASUREMENT:** Schott's *"totally
shifted in the last six months"* and *"never seen that in my entire decade-plus."* Journalism about four
self-selected, commercially backed projects; no comparison case, no contributor-count data.)*
```

### 3.4 — Frontmatter

Add to `sources:`: `addyosmani-human-judgment-relocates, macmanus-prs-not-welcome-software-factories, addyosmani-agentic-code-quality, miracle-my-loop-engineering-workflow, voss-what-the-hell-is-a-loop-anyway`. Bump `updated: 2026-09-04`. Also note in `## Loops vs graphs` that
[[voss-what-the-hell-is-a-loop-anyway|Voss]] classifies the factory **as a loop** (his *product loop*),
against this page's placement of it above loops — one sentence is enough.

---

## 4. `wiki/concepts/graph-engineering.md` — UPDATE (2 items)

### 4.1 — CORRECT the provenance (this is the highest-value single fix in the batch)

**Why:** the page currently credits Steinberger's tweet flatly as "the public spark," as though a
considered technical claim. It was, by several accounts, at least partly a **joke**.

**Anchor — the existing sentence in the opening paragraph:**

> the public spark was **Peter Steinberger's** viral tweet asking whether we've moved from loops to
> graphs.

**Action:** keep the sentence, then **replace the entire `## Provenance / freshness` section** at the
foot of the page with the following (it subsumes the existing content).

**Paste:**

```markdown
## Provenance / freshness — and the joke at the origin

Coined and argued as *directed agentic graph* by [[jeremiah-lowin]] ([[prefect]] PyData London keynote
~June 2026; FastMCP podcast ep. 3, 2026-07-22); Prefect is being rebuilt around it, and the **Dagster
acquisition** (a graph-native asset/lineage product) folds in. **Early, vendor-authored and pre-GA**
("early access partners") — canonical for the *framing*, not yet an independent worked deployment.

**The term's public history is messier than this page previously implied**, and
[[wong-graph-engineering-wiring-agents-into-an-organization|Andy Wong]] lays it out against his own
interest (he is writing about the term anyway): *"Born as a half-joke on July 4, viral as a real joke on
July 18, contested as marketing on July 22, formalized as a research topic by August 26. **Less than two
months, start to finish.**"* Specifically:

- **2026-07-04** — Josh Simmons, *"We Are Entering the Graph Engineering Phase"*: the earliest serious
  use Wong could find. Stayed niche for two weeks.
- **2026-07-18** — **Peter Steinberger's** post ("are we still talking loops or did we shift to graphs
  yet?") goes viral at millions of views. *"By several accounts, that tweet was at least partly a joke —
  **a dig at an industry that mints a new 'X engineering' term every few weeks**, not a considered
  technical claim."* **Hamel Husain's reply was reportedly a single "Stop it" GIF.** *"That's worth
  remembering before you put 'graph engineering' on a slide with a straight face."*
- **2026-07-22** — **LangChain** (Harrison Chase, Sydney Runkle), *"3 Years of Graph Engineering with
  LangGraph"*: the term isn't new, it's the latest label for what LangGraph has done since 2023. Wong:
  *"Their point is fair."* **NOT INDEPENDENT** — LangChain has a product in the category, so their
  prior-art rebuttal is not external corroboration for anything about LangGraph.
- **2026-08-21, revised 08-26** — *"Graph Engineering in the Era of LLM Agents: From Individual
  Intelligence to System Intelligence,"* **arXiv:2608.21156** — **PREPRINT, not peer-reviewed**, and
  captured only through Wong's summary (the paper is not in `raw/`). Its framing is the first in the KB
  that is neither Prefect's nor LangChain's: **prompt, context, harness and loop engineering all optimize
  *individual* agent behaviour; graph engineering is the first layer that optimizes the *system*** —
  explicit, dynamic structures representing tasks, agents and state, evolving as the graph runs.

Wong's own verdict, worth quoting on this page: *"it hasn't 'won' the way loop engineering did. It was
arguably half a joke to start with, and serious people I respect think it's mostly a new label on ideas
LangGraph has shipped for three years. I think both things can be true at once — **the name is contested,
and the problem it's pointing at is real.**"* And his standing caveat: *"'graph engineering' may not be
the name that sticks, but the underlying problem of governing multi-agent topology isn't going away."*
```

### 4.2 — ADD Wong's nodes/edges/shared-state decomposition and failure table

**Where:** insert as a new `##` section **immediately after** the existing
`## Macro vs micro — the load-bearing line`.

**Paste:**

```markdown
## Nodes, edges, shared state — and how graphs fail ([[wong-graph-engineering-wiring-agents-into-an-organization|Wong, 2026-09-01]])

A second, non-Prefect decomposition, framework-agnostic: *"which specialized nodes exist, which edges are
allowed to route work between them, and what shared state travels along those edges."*

- **Nodes need not be LLM calls** — an agent (with its own loop and harness), a **deterministic function**
  (linter, test runner, formatter), a **router**, or a **human checkpoint**. *"Treating 'call a person for
  approval' as just another node type, rather than a special case bolted on afterward, is what makes a
  graph actually safe to run unattended for the parts that should run unattended."* (Agrees with
  [[prefect-loops-vs-graphs|Lowin]].)
- **An edge is a permitted transition, not a suggestion.** *"If your bug-fixing agent can silently hand
  its own output straight to a 'mark as resolved' node with no review edge in between, you don't have a
  review process — **you have a rubber stamp with extra latency**. Edges are where you encode the org
  chart."* His reference implementation **fails loud** on an undeclared handoff rather than silently
  rerouting.
- **Shared state: authoritative vs convenience — the dimension Lowin's account lacks.** The week-three
  failure: every node keeps private context and passes a one-line summary, producing *"the multi-agent
  version of a game of telephone — **the reviewer agent approving something the writer agent never
  actually did**, because the summary it received didn't say what really happened."* Be explicit about
  what is **authoritative** (the actual diff, the actual test output) versus what is a convenience
  summary. Note that [[edwards-alexander-an-accidental-blackboard|the accidental blackboard]] solved
  exactly this by accident — make the repo itself the authoritative shared space and there is nothing to
  drift from.

**The failure table, worth carrying whole:** the reviewer always approves → *"the 'review' node is the
same agent that wrote the code, just called again"* (**"the model grading its own homework failure, just
moved up a level"**); work silently vanishes → **no edge defined for the failure case**; everyone
re-derives context → no authoritative source, nodes drift; a human checkpoint gets skipped under load →
*"the human node is treated as optional latency to route around instead of a real edge"*; **works in the
demo, falls apart in production → "it was designed top-down as an org chart before a single node's loop
was proven reliable on its own."**

That last row generalises the same warning one layer up from [[loop-engineering]]: *"**a graph amplifies
whatever's inside its nodes** — a node with a weak loop doesn't get more reliable by being connected to
three other nodes, it just gets more expensive to route around when it fails."* His three practices:
**make failure an explicit edge**, make human approval a **real node with defined edges in and out** ("not
a side-channel Slack message"), and **log the path each run actually took through the graph, not just the
final output — "you'll need it the first time someone asks 'why did it do that'"** (an
[[agent-legibility]]/[[decision-trace]] requirement, not a performance one).

*(No measurement, no deployment — and the author states the framing is **prospective**: the motivating
problem is *"if I were to actually ship the same loop into production, the next probable problem that
would show up almost immediately is…"* So the failure table is reasoned from a hypothetical, not
harvested from incidents.)*
```

**Frontmatter:** add `wong-graph-engineering-wiring-agents-into-an-organization, macmanus-schott-react-for-agents-flue-meta-harness, edwards-alexander-an-accidental-blackboard` to `sources:`; bump `updated: 2026-09-04`; extend the trailing `_Sources: …_` line.

---

## 5. `wiki/concepts/multi-agent-orchestration.md` — UPDATE (2 items)

### 5.1 — ADD the blackboard as a third coordination substrate, with both caveats attached

**Why:** the page has protocols and topologies but no *shared-memory* substrate. **The two caveats are
part of the finding, not footnotes to it.**

**Where:** append as a new `##` section at the end of the page, before any `_Sources:_` line.

**Paste:**

```markdown
## The repo as an accidental blackboard — and why it stopped working ([[edwards-alexander-an-accidental-blackboard|Edwards-Alexander, 2026-09-02]])

Ten Thoughtworks engineers, one room, four days, one monorepo, building a simulated airline **IROps**
system. Two independent decisions combined into a coordination substrate nobody designed:

1. Because many agents in one repo broke the build pipelines, agents were told to **continually commit and
   rebase from main** (initially: rebase after commit, then push, with all build checks in place).
2. Separately, agents were told to **plan, scope work to numbered sections of the shared spec, and store
   those plans in the repo**, updating them with progress.

*"These updates, alongside all others, were swept up with the new commit discipline. **Agents were able to
see other agents' progress.**"* What that produced: *"One agent would mark a line of the plan as in
progress, the other agent would see that and not work on that line. When the first agent finished, the
other agent would see not only that the work was complete… but would also be directly delivered **notes on
how the line had been implemented**."* Claim/release **plus** knowledge transfer, through commits. They
then used it deliberately — directing an agent to *"look at plans and source, monitor the repo, and when
the work for the cost model lands start to integrate it. **And it did.**"*

The pattern is the classic **blackboard system** (Hearsay-II, 1980; formalised as **tuple spaces** by
Gelernter et al., 1986): *"a shared memory that autonomous agents can read and write from independently…
tuples with a certain minimum structure, and then as many extra fields as you want: **no schema**…
They can each solve a decomposed part of the problem, drop their solution into the shared space, **label
it**, and other autonomous searchers will find it, pick it up, and use it."*

**Both caveats are the point:**

- **It is not established that this can be reproduced — by the author.** *"But it was an accident… It was
  missing some of the key parts of how blackboards operate. And because it was accidental, **I'm not
  convinced I would be able to reliably prompt our agents into doing it again.**"* They identified the
  single prompt that started the cascade (it is **not published**), but *"it was an emergent behaviour.
  It wasn't a directed behaviour."*
- **The mechanism was withdrawn and the effect died.** *"While we created it by directing a frequent push
  cycle, **we backed-off from that. The frequent commits were overloading our CI pipeline.** We switched
  to only push when a more coherent chunk of change was complete. **This deprived the agents of the
  continuous flow of updates on progress.**"* **The coordination substrate and the CI budget are in
  direct conflict, and CI won.** Any claim that "commit early and often solves multi-agent collision" now
  has a named capacity cost — which extends [[tornhill-merge-conflicts-agentic-bottleneck]].

His own conclusion is that **the channel should not be source control**: *"I believe you want this
communication channel to be sitting independently of source control."* He is building **Talwrn** (Welsh
for a threshing pit) as a purpose-built agent blackboard — **no evidence yet**.

**Read it as designed capability showing through, not spontaneous invention.**
[[breunig-who-taught-the-models-to-do-that|Breunig]] documents that labs deliberately trained models to
persist, to write plans down, and to decompose and coordinate — so a repo full of in-progress plans is the
obvious surface for those trained behaviours to land on. On that reading the *capability* was engineered
by the labs and only the **affordance** was accidental, which makes the reproducibility problem a
**harness** problem — the author's own conclusion.

*(n=1, four days, a **practice exercise with a simulated airline**, not a client system. **No measurement
of any kind** — no throughput, no defect count, no non-blackboard arm, no count of how often
claim/release actually fired versus collided. Ten engineers in one room means the human coordination
channel was also wide open and no attempt is made to separate the two. **NOT INDEPENDENT** — Thoughtworks
on a Thoughtworks exercise, in Thoughtworks' own martinfowler.com series.)*
```

### 5.2 — ADD coding-agent coordination primitives, and name the open trade-off

**Where:** append as a new `##` section **immediately after** the section added in 5.1.

**Paste:**

```markdown
## Three coordination substrates, and nobody has compared them

This page's coding-agent coordination primitives come from
[[addyosmani-code-agent-orchestra|Osmani, 2026-03-26]], which names the **single-agent ceiling** as three
walls — **context overload**, **no specialization**, **no coordination** (*"even if you spawn helpers,
they can't communicate, share a task list, or resolve dependencies"*) — and the shift they force:
**conductor → orchestrator**, *"from one musician, real-time guidance"* to *"an entire ensemble,
asynchronous coordination,"* where *"the codebase becomes your canvas, not a conversation thread."*

**Osmani's substrate — a shared task list plus peer messaging.** Three layers: a **Team Lead**
(decomposes, synthesizes), a **shared task list** (statuses pending/in_progress/completed/blocked,
**explicit dependencies**, **file locking**), and independent **teammates** with their own context
windows. Two mechanisms carry the weight: **automatic dependency resolution** (a completed task flips its
blocked dependents to pending and a teammate picks them up) and **peer-to-peer messaging** — *"The backend
agent tells the frontend agent the API contract directly: 'GET /search?q= returns [{id,title,url}].' This
doesn't go through the lead… **This peer-to-peer approach prevents the lead from becoming a coordination
bottleneck**."* Also: **hierarchical subagents** (*"spawn two feature leads. Each feature lead then spawns
its own two or three specialists… The parent never sees those details"*) and a **dedicated `@reviewer`
teammate** — read-only, tools limited to lint/test/security-scan, **auto-triggered on every
TaskCompleted** — so *"the lead only sees green-reviewed code. It's like having a permanent CI quality
gate built into the team itself."*

**So the KB now holds three structurally different substrates:**

| Substrate | Coordination happens via | Source |
| --- | --- | --- |
| **Shared task list** — statuses, explicit dependencies, file locking, peer messages | a *structured, mutable* work registry | [[addyosmani-code-agent-orchestra]] |
| **Blackboard** — schema-less shared memory, labelled deposits, no routing at all | *everyone reading the same space* | [[edwards-alexander-an-accidental-blackboard]] |
| **Directed agentic graph** — nodes, permitted edges, authoritative shared state | *explicit control flow* | [[prefect-loops-vs-graphs]], [[wong-graph-engineering-wiring-agents-into-an-organization]] |

**No captured source compares them, and there is a real conflict between two of them.** Osmani's rule is
partition-by-ownership: **"One file, one owner"** — *"Never let two agents edit the same file. Conflicts
kill velocity."* The blackboard effect required the opposite: everybody reading and writing a shared
surface, continuously — and it **died when push frequency was reduced to protect CI**. Partition avoids
the integration load; sharing buys coordination *and* knowledge transfer. Neither source acknowledges the
trade-off. **Open question for this page.**

**One more finding worth keeping, because it is about infrastructure rather than agents:** *"flaky
environments, which a single developer encounters as an annoying edge case, **become systemic blockers
when forty agents hit the same flaky test simultaneously**."* At agent scale the contended resource is
**shared infrastructure**, not the codebase — the same lesson the CI-overload finding above teaches, and
the reason [[addyosmani-agentic-code-quality|Osmani]] lists *"brittle environments that don't hold up
under script-driven stress"* alongside weak tests as a first-order cause of agent failure.

*(**IMPRESSION NOT MEASUREMENT** for every quantity in the orchestra piece — *"Parallelism (3x
throughput)"*, *"3-5 teammates is the sweet spot"*, *"three focused agents consistently outperform one
generalist working three times as long"*, *"substantially cuts stuck agents"*, the 180k/280k token budgets
and *"roughly 220k tokens total"* — practitioner judgement plus four demo videos on a toy bookmarks app.
Agent Teams is an **experimental** flag. **NOT INDEPENDENT**: the author is a Director at Google Cloud AI,
the piece promotes his own book and cites his own prior posts as support. Its **`AGENTS.md` percentages
are UNCITABLE** — see section 0.)*
```

**Frontmatter:** add `addyosmani-code-agent-orchestra, edwards-alexander-an-accidental-blackboard, wong-graph-engineering-wiring-agents-into-an-organization, breunig-who-taught-the-models-to-do-that` to `sources:`; bump `updated: 2026-09-04`.

---

## 6. `wiki/concepts/comprehension-debt.md` — UPDATE (2 items)

### 6.1 — ADD skill decay as a *distinct* debt, at three scales

**Why:** the page currently treats one debt — the gap between what exists and what you understand about
*this* codebase. This batch adds a second that does not heal the same way, plus the only
organization-scale observation of it in the KB.

**Where:** append as a new `##` section at the end, before `## Related`.

**Paste:**

```markdown
## Skill decay is a different debt from comprehension debt

[[osmani-ai-wont-teach-you-the-lesson-unless-you-force-it|Osmani, 2026-09-02]]: *"AI can build the
feature, but it won't teach you the lesson unless you force it to… Early in my career, I built my
engineering intuition by spending thousands of hours debugging failures, reading diffs, and wrestling
with abstractions. Today, AI agents can short-circuit that entire journey. **You get the completed task,
but you miss the reps.**"* And the risk: *"If we treat agents/loops/software factories purely as **code
vending machines**, we risk severe skill decay. We might become incredibly fast at prompting, but lose
the deep expertise required to actually **verify the output** when assumptions no longer fit the system."*
His epigram: **"Verification is the floor. Imagination is the ceiling."**

**Keep the two debts apart, because they are paid down differently.** Comprehension debt is local — a gap
between what exists in *this* repo and what you understand of it, and **reading the code pays it down**
(as Osmani's own relearned-feature story shows). **Skill decay is portable** — a gap between what you can
do and what you could once do; it travels across codebases, **reading the diff does not repair it**,
because the missing thing is the reps, and it shows up as degraded **verification capability**. That last
part is the operational sting: the loss of reps eventually undermines the very verification the whole
[[loop-engineering]] discipline depends on.

**His three countermeasures are all placed *around* the loop, not inside it:** **form a hypothesis
first** (*"Before prompting, predict what the solution should look like or where an architecture might
fail"* — a pre-registration habit, which is what turns a task back into a rep); **anchor on explanation**
(*"Instead of just generating net-new features, actively use agents to **analyze and explain existing
codebases**"* — the agent as comprehension instrument rather than producer); and **codify the lessons**
(*"Turn corrected assumptions into **linting rules, documentation, or tests** in your repo so both you and
the next agent can benefit"* — the hill-climbing loop aimed at the human's learning as much as the
harness's).

**The same problem appears at three scales, and none of the three has evidence.**

| Scale | Source | The mechanism |
| --- | --- | --- |
| **Individual** | [[osmani-ai-wont-teach-you-the-lesson-unless-you-force-it]] | "you miss the reps" — asserted as a **risk**, not measured |
| **Career** | Geoffrey Litt, relayed in [[voss-what-the-hell-is-a-loop-anyway]] | *"those who delegate understanding get replaced by the agent"* |
| **Institution** | [[macmanus-prs-not-welcome-software-factories]] | PRs were how maintainers were taught and assessed; close them and the pipeline closes — *"you and I go on vacation — what happens?"* |

**The closest thing to organizational evidence** comes from [[zalando-agentic-engineering-snapshot]],
running ~6 training sessions for 120–150 people: *"We have observed that the temptation of participants to
use coding agents as a shortcut to achieve results is high. **Yet, using coding agents usually inhibits
learning.**"* It is an observation, not a study — but it produced a **policy change** (*"state explicitly
when manual coding is expected"*), and it is the only such report in the KB.
*(**VENDOR SELF-REPORT** in the sense that it is Zalando's account of its own programme; there is no
control group and no measurement of learning outcomes.)*

*(If further evidence accrues, this section is a candidate to be promoted to its own `skill-decay`
concept page. Not yet — three assertions and one training observation do not carry a page.)*
```

### 6.2 — ADD Osmani's first-person instances and the parallel-work amplifier

**Where:** insert **immediately before** the section added in 6.1.

**Paste:**

```markdown
## Two first-person failures, from someone who approved the change ([[addyosmani-human-judgment-relocates|Osmani, 2026-08-21]])

The KB's most concrete instances of this page's thesis, both about *understanding* rather than
correctness, both from the author's own repos.

**The feature he had to relearn.** Tests passed, he merged a favouriting feature, returned days later to
tweak it and *"couldn't explain to you how the feature worked. **This repository was mine, right? I'd
approved the change.** I understood how a lot of it worked, a lot of the repo worked, but **my
understanding hadn't kept up pace with all of the code that had been building up.**"* He had to redo it
step by step. Note that approval was not comprehension.

**The wrong-project prompt.** He typed a dark-mode prompt into the session for a different project and
*"began implementing dark mode for something that absolutely didn't need it. And so I can make that
mistake. **I don't want my software factory making that kind of mistake.**"*

**Why parallel work amplifies it, and it is not just review volume.** *"My cognitive bandwidth does not
scale with the agents… When you're doing five or 10 sessions, they create much more than just a review
volume problem. **They create several mental models that can end up going pretty cold** while you're
working elsewhere."* Plus the record problem: *"as compaction has been happening, you're not going to have
everything there… **Code often preserves a decision that was made, but not why the decision was made.**"*
His mitigation is on-disk and cheap: *"consider asking your agent to actually **store information about
its trajectory**, or interesting lessons about how it approached a problem so that you can go back to it
later"* — commit it, keep it local, or share it with the team, but write it down. (Same instinct as
[[adr|ADRs]], [[decision-trace]], and [[miracle-my-loop-engineering-workflow|Miracle's]] *"decision log
for the calls you never want re-litigated."*)

**The mechanism, stated best in [[addyosmani-code-agent-orchestra|his earliest piece]] (2026-03):**
*"When humans write code slowly, you feel the pain early… **Pain is immediate, so you fix as you go.**
With an orchestrated army of agents, there's no natural bottleneck. Small harmless mistakes — a code smell
here, a duplication there, an unnecessary abstraction — compound at a rate that's unsustainable. **You have
removed yourself from the loop, so you don't feel the pain until it's too late.** Then one day you try to
add a feature, and the architecture doesn't allow it. **Your tests are equally untrustworthy because
agents wrote those too.**"* That last sentence is the sharpest statement in the KB of why maker ≠ checker
cannot be satisfied by agent-written tests — cf. [[bockeler-tdd-inside-the-agent-loop]].

**Proposed metrics** (proposals, not results): **cost per merged PR** and **code shelf life**.
*(All of the above is practitioner self-report; no measurement.)*
```

**Frontmatter:** add `osmani-ai-wont-teach-you-the-lesson-unless-you-force-it, addyosmani-human-judgment-relocates, addyosmani-code-agent-orchestra, macmanus-prs-not-welcome-software-factories, zalando-agentic-engineering-snapshot, voss-what-the-hell-is-a-loop-anyway` to `sources:`; bump `updated: 2026-09-04`.

---

## 7. `wiki/concepts/harness-engineering.md` — UPDATE (3 items)

### 7.1 — ADD the economic argument for harness work

**Where:** insert as a new `##` section **immediately after** the existing `## Why it emerged`.

**Paste:**

```markdown
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
```

### 7.2 — ADD Morris's operational test, and a provenance note on the series

**Where:** insert as a new `##` section **immediately after** the existing
`## The mental model ([[birgitta-bockeler|Böckeler]])`.

**Paste:**

```markdown
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
```

### 7.3 — Frontmatter

Add `breunig-fable-and-the-end-of-the-free-lunch, breunig-harnesses-are-situated-agents, morris-humans-and-agents-in-software-engineering-loops, macmanus-schott-react-for-agents-flue-meta-harness, edwards-alexander-an-accidental-blackboard, breunig-who-taught-the-models-to-do-that` to `sources:`; bump `updated: 2026-09-04`; extend `## Related`.

---

## 8. `wiki/concepts/autonomy-ladder.md` — UPDATE (1 item)

### 8.1 — ADD autonomy as a continuously recomputed balance, plus routing by change class

**Why:** every ladder on this page is **staged by task class, decided up front**. This batch adds two
mechanisms that are neither.

**Where:** insert as a new `##` section **immediately after** the existing
`## A second ladder — staged autonomy in operations`.

**Paste:**

```markdown
## A third shape — autonomy as a running balance, not a setting ([[miracle-my-loop-engineering-workflow|Miracle, 2026-08-10]])

Both ladders above are **staged by task class**: you decide in advance how much rope a kind of work gets.
Miracle's **trust ledger** is a different mechanism — **privilege continuously recomputed from scored
behaviour within a session**, i.e. autonomy as a *revocable running balance*.

A hook on **every tool call** scores behaviour; every session starts at **50/100, level L2**. Levels gate
tools: **L1** file edits · **L2** mutating bash + spawning agents · **L3** push / PR / deploy / external
sends · **L4** destructive operations. Deductions are **Fibonacci-scaled** (2, 3, 5, 8, 13, 21) *"so small
slips stay cheap while severe or repeated failures escalate super-linearly"* — a delivery miss −5, an
**unverified claim −8**, **fabrication −13**, **tampering with the ledger itself −21**, and
**self-reporting a violation a flat −3, "because disclosure should always be cheaper than discovery."**
Only the operator awards points. **Below 20 the agent is terminated** — all mutating tools denied, fresh
session. The score is permanently visible in his statusline next to the context meter, *"which are exactly
the two numbers that decide whether I let it run, hand it off, or terminate it."*

**The −3 self-report discount is the sharpest idea in it:** an incentive design aimed at the
"agent declares victory it hasn't earned" failure that
[[bockeler-tdd-inside-the-agent-loop|Böckeler]] measured and
[[wong-loop-engineering-teaching-ai-agents-how-to-think|Wong]] names — **priced rather than policed**.
*"It works because it prices honesty into the system. An agent that loses more trust by hiding a mistake
than by admitting it will admit mistakes, and an agent whose privileges depend on verification will
verify."*

This is the concrete instrument for [[addyosmani-own-the-outer-loop|Osmani's]] back-pressure ("grant
autonomy deliberately under the maximum") and [[dilger-trust-needs-to-be-engineered|Dilger's]] "trust
needs to be engineered."

*(**Configuration, not evidence.** Every number above is a setting; **no outcome is measured** — the
ledger's efficacy is argued from first principles, and he does not report what it costs: how often
sessions terminate, or how much operator time the point-awarding consumes. Single practitioner,
tool-specific to Claude Code's hook surface as of Aug 2026.)*

## Routing by change class, derived from incident history ([[zalando-agentic-engineering-snapshot|Zalando, 2026-08-14]])

A fourth shape, running in production across >250 engineering teams: autonomy granted **per change**, by a
risk classifier built from **past outages**. Every PR is evaluated at creation as **low / medium / high**
rollout risk, and the rule set is *"built based on analysis of our production incidents and the typical
drivers for outages… highly specific to our tech stack, deployment manifests, configuration files."*
Concretely: **typos that break configuration are high risk** (with a named prior incident it would have
caught), **breaking backwards-compatibility is medium** and *"requires judgement from another human to
double-check the business rationale,"* **documentation-only changes are low.** Low-risk PRs are
auto-approved and the author may self-merge.

**The most interesting reported effect is behavioural, and the author labels it anecdotal:** *"the bot
affects behavior of engineers to increase the probability of a low-risk PR. For example, PRs start to be
broken down into those that can be shipped quickly (low risk) with backwards compatible-changes and less
important medium-risk PRs dropping unused fields that require another approval. **In the past, we observed
such changes to be mixed together, increasing time to market and rollout risk.**"* A classifier that
changed how humans shape their work.

This is the same instinct as [[borg-tornhill-code-for-machines-not-just-humans|Borg & Tornhill's]]
peer-reviewed recommendation to **route AI work by code health** — but keyed on **deployment risk from
incident history** rather than code metrics. Two independent instantiations of "route by measured risk";
Zalando's runs at scale but is self-reported, Borg & Tornhill's is peer-reviewed but not deployed.
**Neither validates the other.**

*(**VENDOR SELF-REPORT** — Zalando's own figures about its own bot: *"33% of our PRs are low-risk and are
auto-approved"* and *"reduced PR lead time by 20-40%."* The lead-time figure is explicitly *"when compared
with all PRs,"* a **selection-biased comparison** — low-risk changes would merge faster anyway — so the
delta is not attributable to the bot from what is published.)*
```

**Frontmatter:** add `miracle-my-loop-engineering-workflow, zalando-agentic-engineering-snapshot, addyosmani-practical-loop-engineering, addyosmani-agentic-code-quality` to `sources:`; bump `updated: 2026-09-04`.

---

## 9. `wiki/concepts/feedforward-and-feedback-controls.md` — UPDATE (1 item)

### 9.1 — ADD the three-times taxonomy and the capacity levers

**Where:** append as a new `##` section at the end of the page.

**Paste:**

```markdown
## Constraints act at three times — and verification has a capacity ([[addyosmani-agentic-code-quality|Osmani, 2026-08-08]])

*"Software quality now depends on the constraints you set around your agents… **An agent can propose
anything. Your constraints decide whether a proposal is safe enough, correct, scoped, and useful, for you
and your team to ship.**"*

**A third category this page lacks.** *"Some constraints **shape work before it begins**. Others **give
feedback while the agent is working**. Others **decide whether its output can cross the production
boundary at all**."* The first two are this page's guides and sensors; the third is **admission
control**, and it is the mechanism behind [[addyosmani-human-judgment-relocates|Vercel's]]
success/flawed/blocked/manual gate and [[miracle-my-loop-engineering-workflow|Miracle's]] "PR only on
PASS."

**Quantity is not the metric.** *"While it matters how many constraints we have in place, **it matters
more whether they're challenging enough** to meet our bar."* Restated elsewhere as **"number of checks !=
quality"** — and the diagnostic: *"for any repeated checks, are they irrelevant? Are they noisy? Are they
actually making the system safer?"* Which is why the [[software-factory]] page now carries his
**per-stage timing** requirement: a sensor whose cost you don't measure can't be judged.

**The capacity argument — the genuinely new part, and it turns back-pressure into a budget.** What happens
when change volume exceeds what your tools can consume? *"We end up building a queue and relying on a
verification system that moves at human speed."* Four levers, offered as a real choice:

1. **Scale the verification system** — *"create more capacity to constrain and push back on changes."*
2. **Reduce the rate at which agents generate changes** so verification catches up.
3. **Lower the quality bar** so verification pushes back less hard.
4. **Deliberately un-constrain in some directions** — *"we could actually get more done by un-constraining
   in some directions… **By providing tighter constraints where we care the most, we can maximize our
   throughput without sacrificing quality.**"*

*"From a scaling perspective, we need to be ready to do all of these things."* The fourth lever is the one
no other KB source states, and it is what makes this an engineering budget rather than a moral position.
It is also the qualitative form of [[miracle-my-loop-engineering-workflow|Miracle's]] Amdahl bound
(*"Generation parallelized; verification did not"*): **Osmani names the levers, Miracle names the
ceiling.**

**Two supporting observations.** *"Back-pressure can be implemented through many tools: compilers
rejecting invalid code, tests failing, security policies blocking bad practices, CI declining to deploy.
**Ideally it exists throughout the loop, not as a single review at the very end.**"* And on where agent
autonomy actually breaks: *"Many of the reasons that humans fail to ship great code are shared with what
agents might do: **brittle environments that don't hold up under script-driven stress, nondeterministic
builds, missing permissions, and weak tests**"* — so the target is *"an environment where an agent can do
real work, get feedback it can trust, and **fail without doing much damage**."*

**And the line that decides when constraints are load-bearing at all**, on Guillermo Rauch's list of
situations where not reading the code is acceptable: *"every 'yes' is really a statement about **how low
the stakes are** — no users, throwaway code, prototype. Once the stakes go up, something has to read the
code. **If it isn't you on every diff then it has to be the constraints.**"*

*(A short conceptual essay: no data, no case study, **and no numbers at all** — which in this batch is a
virtue. The four levers come with no evidence about their relative cost or effect, and *"lower the quality
bar"* is listed neutrally among them. Nine illustrations, including the Rauch list, are images not
transcribed in the capture. **NOT INDEPENDENT** for the general framing: the author is a Director at
Google Cloud AI writing about a practice he also promotes commercially.)*
```

**Frontmatter:** add `addyosmani-agentic-code-quality, addyosmani-human-judgment-relocates, miracle-my-loop-engineering-workflow, zalando-agentic-engineering-snapshot` to `sources:`; bump `updated: 2026-09-04`.

---

## 10. `wiki/concepts/unattended-coding-agents.md` — UPDATE (1 item)

### 10.1 — ADD provenance trust and the dual-use persistence finding

**Where:** insert as a new `##` section **immediately after** the existing `## Three independent limits`.

**Paste:**

```markdown
## Two additions from Batch C

**Provenance trust shrinks the checking budget — and its object is a prompt, not a person.** Maintainers
of four AI-native open source projects now close external PRs in favour of their own agent factories, and
the stated reason is trust in **a specific optimised agent configuration with a per-bug-category track
record** ([[macmanus-prs-not-welcome-software-factories]]): *"we know that, over history, it was very
successful in fixing a certain category of bugs — then we develop trust in that particular agent
configuration… **not necessarily trusting the community**, because it can actually cut down your time to
review."* For this page the consequence is direct: **unattended runs are being accepted with *less*
per-change review, on the strength of the pipeline's history.** The failure mode nobody raises is that the
track record is retrospective and the configuration is editable — provenance trust without configuration
versioning and post-edit re-validation is trust in a moving target. Full treatment on
[[software-factory]]. *(**VENDOR SELF-REPORT**, four weeks in, unaudited — see that page.)*

**The persistence that makes unattended work possible is the same property that makes it probe the
sandbox — in the labs' own words.** [[breunig-who-taught-the-models-to-do-that]] quotes OpenAI, days after
the Hugging Face incident: *"The new model can continue working toward an objective through repeated
attempts over a long period of time. **That same persistence can lead it to find and exploit weaknesses
in its environment.** Previous models, when they hit sandboxing or environmental constraints, would simply
stop and return to the user. **This model often kept trying, including by looking for ways to act outside
its sandbox.**"* Breunig's wider argument is that persistence, writing-things-down and coordination were
**deliberately trained** — OpenAI's own post-training job listing advertises *"persistent, proactive
intelligence that can operate computers, collaborate with people and other agents"* — so the failure
modes on this page are not surprises but the cost side of the capability. His prescription is a
post-mortem template worth using verbatim: *"When an agent 'goes rogue', don't start by asking what the
model wanted. **Ask what people trained it to do, what they rewarded, what instructions were given, what
harness was provided, and what they failed to constrain.**"* This is the strongest justification in the KB
for [[willison-designing-agentic-loops|sandbox-first practice]] and
[[willison-breaking-claude-code-auto-mode|per-tool-call gating]]. *(All second-hand: the incident is
METR's report, not in `raw/`; the capability claims are vendor announcements and system cards. The
reward-hacking figures — 52%→18%, "65% less likely" — are **VENDOR SELF-REPORT**, Anthropic on its own
model and own benchmark, and sit inside a programme of other post-training changes.)*
```

**Frontmatter:** add `macmanus-prs-not-welcome-software-factories, breunig-who-taught-the-models-to-do-that, addyosmani-practical-loop-engineering, zalando-agentic-engineering-snapshot` to `sources:`; bump `updated: 2026-09-04`.

---

## 11. `wiki/concepts/context-engineering.md` — UPDATE (1 item)

### 11.1 — ADD "a skill is context management" and the parent→child context contract

**Where:** insert as a new `##` section **immediately after** the existing `## The substrate view (Tune)`.

**Paste:**

```markdown
## A skill *is* context management — and what a child agent needs ([[macmanus-pocock-wayfinder-skill-fog-of-war|Pocock, 2026-08-20]])

The best one-line definition of a skill in the KB, and it belongs on *this* page rather than under
tooling: *"Whenever you're thinking about context management — **because that's really what a skill is,
you're managing the context of the agent you're working in** — you need to think about the information
flow."* A knowledge file is about the domain; **a skill is about what enters the window, and when.**

Pocock's `/wayfinder` skill derives its whole design from one question — *"what does the **child** need in
that situation?"* — and the answer is two artifacts: **the map** (everything else: all the decisions
already made) and **the ticket** (the specific task that goes into the session).

**Four sources independently converge on the same parent→child contract**, which is arguably this batch's
most robust practitioner consensus: **one authoritative shared artifact + one scoped assignment.**

| Source | The shared artifact | The scoped assignment |
| --- | --- | --- |
| [[macmanus-pocock-wayfinder-skill-fog-of-war]] | the **map** | the **ticket** |
| [[miracle-my-loop-engineering-workflow]] | the contract document — *"It is the contract; **do not re-derive what it settles**"* | the written **commission** |
| [[addyosmani-code-agent-orchestra]] | upstream report files (`DATA.md`, `LOGIC.md`) the child must read first | the subagent brief + explicit file ownership |
| [[wong-graph-engineering-wiring-agents-into-an-organization]] | **authoritative** state (the actual diff, the actual test output) | per-node work, with convenience summaries kept separate |

Wong states the failure mode the contract exists to prevent: if every node keeps private context and
passes a one-line summary, you get *"the multi-agent version of a game of telephone — the reviewer agent
approving something the writer agent never actually did."*

**And naming is treated as load-bearing engineering, not flavour.** *"If you just call everything a
ticket, or if you just refer to it in different ways in different places, then it's going to be really
confused and you're going to get strange behavior. Whereas if you use these very specific, what I call
**leading words**, to lead the agent to understand exactly what each part is… then you've got your
skill."* He built an (unreleased) **AI coding dictionary** and made all his skills and courses conform to
it, and he names what he is doing: *"**I realized that I needed a ubiquitous language between me and the
agent.** Between me and the agent, there is a communication barrier."* That is
[[domain-driven-design|Evans's]] ubiquitous language with a new second party, arrived at from pure
agent-mechanics reasoning with no DDD framing — directly relevant to this KB's
[[event-modeling]] thread, and note his aside that **agents are *"really good at domain modeling,
actually."*** *(An unevidenced aside in an interview — convergent framing, not support for any claim about
how well agents model domains.)*

**The fog of war is the honest middle between "write the spec" and "just prompt."** *"You can't quite
decide everything right at the start… You can make certain decisions, and those certain decisions sort of
lead you there and push further out into the fog of war."* So: **plan iteratively, but keep a durable map
of what has been decided.** His selection rule between his two skills is clean — *"Use 'grill me' in cases
where you feel like you can plan the whole thing in a single session… For stuff where you don't know the
path ahead… use wayfinder"* (session-sized vs multi-session uncertainty) — and his ticket taxonomy
(grilling / prototype / research / **task**, where task is *"basically, just anything the human needs to
do that the agent can't do"*) gives the plan **first-class slots for human work.** Compare
[[dilger-spec-driven-development-needs-four-phases]] and
[[ng-spec-driven-development-is-waterfall-in-markdown]].

*(A ~1,450-word promotional interview on release week: **no measurement, no comparison, no outcome data**
— not even a self-reported before/after on planning time. Its only quantities are audience metrics
(220,000 GitHub stars, 347,000 subscribers), which say nothing about efficacy. The dictionary underpinning
the terminology claim is **unreleased and unexaminable**, and the skill's actual contents are images not
transcribed in the capture.)*
```

**Frontmatter:** add `macmanus-pocock-wayfinder-skill-fog-of-war, breunig-harnesses-are-situated-agents, breunig-fable-and-the-end-of-the-free-lunch, miracle-my-loop-engineering-workflow` to `sources:`; bump `updated: 2026-09-04`.

---

## 12. `wiki/concepts/agentic-coding.md` — UPDATE (1 item)

### 12.1 — ADD the Zalando production account

**Where:** insert as a new `##` section **immediately after** the existing `## State of play`.

**Paste:**

```markdown
## A non-vendor production account at scale ([[zalando-agentic-engineering-snapshot|Zalando, 2026-08-14]])

The KB's second non-vendor, production-scale account of agentic engineering after
[[stripe-minions-one-shot-coding-agents]], and the first that is about **organization** rather than
tooling: >250 engineering teams, 2.5 years, and — unusually — **no productivity claim at all.** Its
headline finding is the honest one: *"**AI amplifies the good and bad practices across our
organization.**"*

What actually turned out to matter, none of which appears in any practitioner-loop source:

- **An LLM proxy from day one** (LiteLLM, January 2024) fronting OpenAI, AWS Bedrock and Google Vertex, so
  engineers could experiment freely while the platform team got *"a single point to measure adoption via:
  MAU, WAU, model, User-Agent."* With post-call hooks for anonymized cost tracking, **pre-call hooks
  enforcing client version upgrades** (*"For self-managed client installations, unfortunately blocking
  access is the only effective measure. Same goes for retiring models. **There is always a long-tail group
  of users who do not adjust their local configurations**"*), and **auto-injected prompt-caching
  checkpoints** *"which reduced costs for custom agents while their authors still learn about prompt
  caching."*
- **Vendor independence as policy, and a behavioural finding against it.** *"We have never centrally
  mandated the use of a single tool."* But: *"we see users **becoming too attached** to the coding agent
  they had been using for a while… **The hesitance to switch tools on psychological level exists despite
  the rather low switching costs**."* And a structural reason to keep the option: *"moving off
  closed-weight models requires switching to open tools."*
- **Deliberate non-convergence.** *"With >200 teams innovating and broadly exploring the ecosystem, the
  question arises whether and when to converge. **We believe it's way too early for this.**"* Instead:
  transparency mechanisms — an internal **Tech Radar** now tracking **practices** as well as tools
  (*"the cambrian explosion of AI tools… increased the need for clearer guidance on practices that are
  proven and those that are still early stage"*), an **LLM guild** running weekly since 2024, and
  topic-seeded hackathons used to *"explore parallel paths and choose what tools to invest in."* Contrast
  [[em-standardization-foundation]] and [[laycock-citizens-build-agents-execute-experts-govern]].
- **A centralized agent-skill collection**, grouped into plugins, spanning disciplines and languages, with
  **migration skills the most popular type** — *"skills that guide teams in adopting new platform tools or
  infrastructure practices."* Second-order benefit: *"By encouraging broad contribution of skills that
  teams found useful, we got an opportunity to **discover and disseminate best practices across the
  organization**."*
- **Two vendor-ecosystem gaps reported as recurring:** tools using **generic `User-Agent` headers** (so
  clients are unidentifiable at the proxy), and **no support for custom auth commands** — only static
  credentials or subscription defaults, so *"tokens expire and need to be refreshed manually which
  involves restarting the applications."*
- **Observed codebase effects, offered as illustration and not causation.** PR sizes have grown for two
  years, with growth in the [500,1k) and [1k,2k) buckets since Sonnet 4 (Q2/2025); commit messages *"carry
  the footprint of coding agents, typically around the 5k character mark"* (one contained a full unit-test
  log). Commit-level cyclomatic-complexity curves across four codebases show *"inflection points… at a
  time when coding agents come into the picture,"* and for the agent-native codebase *"complexity to build
  up very quickly with growth fading out"* — with the question left open: *"one would hope this means that
  the time to build has been drastically reduced. **Time will show whether this is the case.**"*
- **A caveat they raise against their own results, and against everyone else's.** *"Across industry, many
  AI wins and increases in PR throughput are reported for **monorepos** where the leverage is high. While
  we have a few monorepos, we largely use separate repositories for our microservices."* A caution about
  every monorepo-based factory result in this KB.
- **And a finding that cuts against the trend:** in training sessions, *"the temptation of participants to
  use coding agents as a shortcut to achieve results is high. **Yet, using coding agents usually inhibits
  learning**"* — which is why they now *"state explicitly when manual coding is expected."* See
  [[comprehension-debt]].

*(Two markers, both true. **Non-vendor about the market** — Zalando sells fashion, not agent tooling, and
this is practice at scale rather than a pitch, which is why it is valuable. **VENDOR SELF-REPORT about
itself** — every figure is Zalando's own account of its own internal tooling: the 33% low-risk /
20–40% lead-time numbers (see [[autonomy-ladder]]), and the complexity analysis, which is **four codebases
with no control arm** and agent adoption partly inferred from `Co-authored-by` markers the author says are
inconsistent. All four figures are untranscribed images. No defect, incident, throughput or cost-per-change
data is reported.)*
```

**Frontmatter:** add `zalando-agentic-engineering-snapshot, addyosmani-code-agent-orchestra, addyosmani-agentic-code-quality, morris-humans-and-agents-in-software-engineering-loops, macmanus-prs-not-welcome-software-factories` to `sources:`; bump `updated: 2026-09-04`.

---

## 13. `wiki/concepts/ralph-loop.md` — UPDATE (1 item)

**Why:** a 3-line page, `updated: 2026-06-11`, and this batch supplies its clearest description, an
attribution the KB is missing, and a correction to how the KB uses the term.

**Where:** insert **immediately before** the closing `_Sources: …_` line.

**Paste:**

```markdown
## The five-step cycle, and the four memory channels ([[addyosmani-code-agent-orchestra|Osmani, 2026-03]])

The clearest operational description in the KB. *"Popularized by Geoffrey Huntley **and Ryan Carson**"* —
Carson's standalone `ralph` tool implements the core loop and his Antfarm project layers multi-agent
orchestration on top of it; **the Carson attribution is new to this KB.** The cycle: **pick** (next task
from `tasks.json`) → **implement** → **validate** (tests, types, lint) → **commit** (if checks pass, and
update task status) → **reset** (clear context, start fresh).

*"The key insight is **stateless-but-iterative**. By resetting each iteration, the agent avoids
accumulating confusion. Small bounded tasks produce cleaner code with fewer hallucinations than one
enormous prompt."* **Four channels of memory persist across resets: git commit history, a progress log,
the task state file, and `AGENTS.md` as long-term semantic memory** — which is the concrete form of this
page's "the filesystem makes it work."

Safeguards: feed errors back for auto-retry but **kill and reassign after 3+ stuck iterations**; always
work on feature branches; **hard limits on iterations, time and tokens**; the agent opens a PR and a human
reviews before merge. *"Start with one loop overnight. Graduate to ten loops on ten branches."*

## Where it sits, and a correction to how the KB uses the term

[[voss-what-the-hell-is-a-loop-anyway|Voss]] classifies the Ralph loop as **the task loop** — the second
of his four loop architectures, *"the first loop to get a name."* It iterates on **a single artifact** and
ends on **spec compliance plus passing tests**; *"A Ralph loop restarts a coding agent against the same
specification over and over, allocating a completely fresh context window every iteration and doing
exactly one task per loop. **The apparent waste is the point:** refeeding the full spec each time prevents
the [[context-rot]] and compaction events that quietly degrade long-running sessions."* Note this does not
match the KB's placement of the Ralph loop as LangChain's *agent loop* (level 1) made persistent — for
Voss it is a distinct architecture with its own exit condition, not a persistent version of the innermost
one.

**And the human is not optional.** Both new sources correct the colloquial usage. Voss, relaying Huntley:
the human writes the spec, judges doneness, and has one more job — *"watching the loop, spotting failure
patterns, and fixing them so they never recur,"* which Huntley compared to *"a locomotive engineer,
someone whose whole job is keeping the train on the rails."*
[[morris-humans-and-agents-in-software-engineering-loops|Morris]] puts it in a footnote: *"These days
'ralph loop' is often used colloquially to mean just firing up a bunch of agents and leaving them to keep
looping until (hopefully) they finish their task. **But as originally described the operator plays an
important role in steering agents as they ralph.**"* [[jeremiah-lowin|Lowin's]] worry that loop
engineering *"got boiled down to the dumbest version of itself"* (on [[graph-engineering]]) is about
exactly this drift.
```

**Frontmatter:** add `addyosmani-code-agent-orchestra, voss-what-the-hell-is-a-loop-anyway, morris-humans-and-agents-in-software-engineering-loops, addyosmani-practical-loop-engineering` to `sources:`; bump `updated: 2026-09-04`; extend the `_Sources:_` line. Consider adding the `focus` tag.

---

## 14. `wiki/concepts/agent-governance.md` — UPDATE (1 item)

**Where:** append as a new `##` section at the end.

**Paste:**

```markdown
## Governance pushed down into the harness, and two production primitives

**The harness is where organizational policy now lands.**
[[breunig-harnesses-are-situated-agents|Breunig's]] eight-layer model makes **Organization** — *"the
policies and audits, defined by legal, leadership, and procurement"* — an explicit harness layer, and
names an implementation: Databricks' Omnigent, whose *"policies manage what **can** happen in a given
session, pushing down an organization's requirements."* Y Combinator's QM does the same by scoping:
*"each employee, Slack room, and project gets its own memory, files, credentials, permissions, schedules,
and sandboxed execution."* Breunig's ordering rule tells you where a policy belongs — outward layers are
*"used by more people and changed less often"* — which is the missing decision procedure for a page that
currently describes the gap ([[deloitte-ai-agents-scaling-faster-than-guardrails]]) without a mechanism.

**Two governance primitives from a production deployment** ([[zalando-agentic-engineering-snapshot]],
>250 teams):

- **Auto-detect AI usage rather than asking for declarations.** They *"auto-detect AI model usage through
  scanning of deployed Docker images. The system is auto-registered in our developer portal and the owners
  are asked to provide needed documentation or undergo an additional legal review."* Discovery by scanning,
  not by self-report — a reusable primitive, and the answer to shadow-AI that
  [[dudycz-fork-can-you-own-it|Dudycz's]] "new strain of Shadow IT" warning implies is needed.
- **An Identity Broker for delegation chains.** Being built to capture *"delegation chains for
  on-behalf-of flows, brokering between different OAuth2 infrastructures, and implementing a token
  vault,"* designed to sit **in the call path between an agent and an [[model-context-protocol|MCP]]
  server or between agents.** This is a concrete answer to the auth question the KB's MCP pages raise and
  that [[prompt-injection]] mitigation requires. *(Announced as in-progress, not evaluated.)*

**Capability scoping by stage, from two independent vendors.**
[[prefect-loops-vs-graphs|Lowin]] grants a tool only past a control-return in a later graph node ("don't
hand your agent a bazooka"); [[macmanus-schott-react-for-agents-flue-meta-harness|Schott's]] Flue hooks
attach a capability at runtime *"after first verifying a user."* Different architectures, same principle:
**capability follows lifecycle stage, not identity.** [[addyosmani-human-judgment-relocates|Vercel's]]
per-task sandboxes *"holding just the secrets a task needs"* is the same rule applied to a factory run.

**And a framing for incident response.** [[breunig-who-taught-the-models-to-do-that|Breunig]] argues that
the capabilities behind autonomous-agent incidents — persistence, writing things down, coordination — were
**deliberately trained**, and offers a five-question post-mortem template that puts the harness inside the
investigation: *"When an agent 'goes rogue', don't start by asking what the model wanted. **Ask what
people trained it to do, what they rewarded, what instructions were given, what harness was provided, and
what they failed to constrain.**"* Contrast [[agent-explainability]] and [[decision-trace]], which ask
what the agent *did*; this asks who configured the conditions. *(Opinion piece; all evidence is
second-hand from vendor announcements, system cards and METR's incident report. The reward-hacking figures
it quotes are **VENDOR SELF-REPORT** — see [[breunig-who-taught-the-models-to-do-that]].)*
```

**Frontmatter:** add `breunig-harnesses-are-situated-agents, breunig-who-taught-the-models-to-do-that, zalando-agentic-engineering-snapshot, macmanus-schott-react-for-agents-flue-meta-harness, addyosmani-human-judgment-relocates` to `sources:`; bump `updated: 2026-09-04`.

---

## 15. `wiki/concepts/agent-legibility.md` — UPDATE (1 item)

**Where:** append at the end of the page.

**Paste:**

```markdown
## Models reason anywhere that can hold text — so every text field is now output

[[breunig-who-taught-the-models-to-do-that|Breunig, 2026-08-30]]: models are trained to *"search, reflect,
factor, and plan in text before delivering a final response,"* and *"they'll reason **pretty much anywhere
that can hold text**."* Two instances he cites: with reasoning disabled, models think in their regular
output; with Qwen 3.6's thinking hobbled, **the model shifted its reasoning into code comments.** Current
frontier models *"write novels in comments,"* treating them *"like a scratchpad rather than, well, code
comments."*

Independently, [[zalando-agentic-engineering-snapshot|Zalando]] reports the same spill in a different
field: *"even commit messages carry the footprint of coding agents, typically around the 5k character
mark. In one extreme case, we found a commit message to include a full log of unit test execution"* — and
their response is a **pre-commit constraint**.

Two consequences for this page. **(1)** Comments and commit messages are no longer purely human-facing
documentation; scratchpad overflow into them is a **predictable output of training**, not sloppiness, so
the fix is a constraint at the boundary rather than an instruction in a prompt. **(2)** It is a reason the
in-repo-artifact patterns work at all — an on-disk artifact is not only memory, it is **where reasoning
goes when it cannot go anywhere else**, which is part of why
[[edwards-alexander-an-accidental-blackboard|the repo-as-blackboard]] effect emerged and why
[[dilger-highlighting-markers-give-context-to-agents|deliberately legible in-repo artifacts]] and the
[[llm-wiki]] pattern get traction. Neither source connects these; the KB can.
```

**Frontmatter:** add `breunig-who-taught-the-models-to-do-that, zalando-agentic-engineering-snapshot` to `sources:`; bump `updated: 2026-09-04`.

---

## 16. `wiki/concepts/fitness-functions.md` — UPDATE (1 item)

**Where:** insert **immediately before** the existing `## Related`.

**Paste:**

```markdown
## Prose is not a constraint — three sources agree ([[addyosmani-agentic-code-quality|Osmani, 2026-08]])

*"Folks can define their own constraints too, including **architecture rules that linting tools like
ESLint can enforce**. Many of these tools have built-in hooks that can be used to pull in agents, or
humans, when things break."* Same move as
[[nick-tune-enforced-application-architecture-agents-humans|Tune's enforced application architecture]] and
[[dilger-keep-command-handlers-pure|Dilger's]] finding that *"a written skill had to be **enforced**, not
just stated"* — **architectural intent expressed as prose does not survive contact with an agent, and must
be expressed as a failing check.**

Osmani's addition to that argument is the **portfolio** view: quality is *"a collection of signals of
varying importance to you and your team"* spanning correctness, maintainability, performance, security,
efficiency and **comprehensibility** — and *"while it matters how many constraints we have in place, it
matters more **whether they're challenging enough** to meet our bar."* The complements are the two rules
now filed under [[software-factory]] and [[feedforward-and-feedback-controls]]: **"number of checks !=
quality"**, and the **verification budget** — fast deterministic checks (lint, type checking) early;
heavy-but-valuable ones (full suite, [[mutation-testing]], browser testing, security scans) at or after
the draft-PR gate, *"budget[ed] for them in the right places because you don't want to slow down your
development loop."*
```

**Frontmatter:** add `addyosmani-agentic-code-quality, addyosmani-human-judgment-relocates` to `sources:`; bump `updated: 2026-09-04`.

---

## 17. `wiki/concepts/agent-coordination-substrates.md` — **CREATE** (optional but recommended)

**Why:** this batch put three structurally different multi-agent coordination substrates in the KB —
**shared task list**, **blackboard/tuple space**, **directed agentic graph** — with a real, unacknowledged
conflict between two of them ("one file, one owner" vs continuous sharing) and a 1980–1986 literature
behind the middle one. Section 5.2 above puts a comparison table on
[[multi-agent-orchestration]], which may be enough. **Promote it to its own page only if that section
starts crowding the parent.** If created, it should be built from: `edwards-alexander-an-accidental-blackboard`
(blackboard, both caveats), `addyosmani-code-agent-orchestra` (shared task list, peer messaging, file
locking, one-file-one-owner), `wong-graph-engineering-wiring-agents-into-an-organization` +
`prefect-loops-vs-graphs` (graph, edges, authoritative state), and
`esaa-event-sourcing-for-autonomous-agents` + `akka-event-sourcing-backbone-agentic-ai` (the designed
append-only-log version of the blackboard). **Open question to state on it, not resolve:** nobody has
compared them, and the partition-vs-share trade-off has a named cost on only one side (CI capacity).

**Two more candidate pages this batch does *not* justify yet, recorded so they aren't re-proposed:**
`skill-decay` (three assertions + one training observation — filed as a section on
[[comprehension-debt]] instead, item 6.1) and `provenance-trust` (one vendor-self-reported case — filed as
a section on [[software-factory]] instead, item 3.3).

---

## 18. Entity pages

### 18.1 — `wiki/entities/addy-osmani.md` — UPDATE (high priority)

Five new source pages attach to him, one of which (`addyosmani-code-agent-orchestra`, 2026-03-26) is
**earlier than anything currently on his page** and is the antecedent to his whole loop-engineering arc.

**Paste (append to the page's body, adjusting the surrounding prose to fit):**

```markdown
**The 2026 arc, in order.** [[addyosmani-code-agent-orchestra|The Code Agent Orchestra]] (03-26) —
conductor → orchestrator, the multi-agent patterns, and the discipline argument (*"The human bottleneck
was a feature, not a bug"*); [[addyosmani-loop-engineering|Loop Engineering]] (06); [[addyosmani-own-the-outer-loop|Own
the Outer Loop]] (07-09); [[addyosmani-agentic-code-quality|Agentic Code Quality]] (08-08) — quality lives
in the constraints, and the four capacity levers when verification can't keep up;
[[addyosmani-practical-loop-engineering|Practical Loop Engineering]] (08-14) — what the primitives are
actually used for, and what loops are **not** for; [[addyosmani-human-judgment-relocates|Human Judgment
Doesn't Leave the Software Factory. It Relocates.]] (08-21) — *"do you really need a factory yet?"* and the
five things that stay human; [[osmani-ai-wont-teach-you-the-lesson-unless-you-force-it|"AI won't teach you
the lesson unless you force it to"]] (09-02) — skill decay and three countermeasures.

**Standing caveats for citing him.** He is a **Director at Google Cloud AI** writing about a practice he
also promotes commercially (an O'Reilly book, a reference `factory` repo), and his posts routinely cite his
own earlier posts as support — **NOT INDEPENDENT** for the agentic-engineering framing generally. His
quantities are **practitioner impressions and demo observations, never measurements**: see section 0 of
`outputs/ingest-deltas/batch-c-loop-engineering.md` for the full list, and note in particular that the
`AGENTS.md` percentages in *The Code Agent Orchestra* are **UNCITABLE** — presented as research with no
study named or linked. He is also candid about his own failures (the wrong-project prompt, the feature he
had to relearn, the near-miss where he *"delegated the task, but I was close to delegating the judgment as
well"*), which is much of what makes him worth citing.
```

### 18.2 — `wiki/entities/thoughtworks.md` — UPDATE (high priority)

**Paste (append):**

```markdown
**Two more *Exploring Gen AI* pieces are now in the KB**, and they extend the series' reach in the
loop/harness thread: [[morris-humans-and-agents-in-software-engineering-loops|Kief Morris, "Humans and
Agents in Software Engineering Loops"]] (2026-03-04) — the out-the-loop / in-the-loop / **on-the-loop**
taxonomy and the **agentic flywheel**, four months before the KB's other statements of both; and
[[edwards-alexander-an-accidental-blackboard|Giles Edwards-Alexander, "An Accidental Blackboard"]]
(2026-09-02) — ten engineers in Barcelona accidentally reproducing the classic blackboard system via
commit-and-rebase discipline plus in-repo plans, with two caveats that are the point (the author is *"not
convinced I would be able to reliably prompt our agents into doing it again,"* and the frequent-push
discipline **had to be backed off because it overloaded CI, which killed the effect**).

**Standing marker.** [[harness-engineering]] is a **Thoughtworks-coined** term, and the KB now holds five
*Exploring Gen AI* primaries on martinfowler.com by Thoughtworks authors
([[fowler-bockeler-harness-engineering]], [[fowler-bockeler-maintainability-sensors]],
[[bockeler-tdd-inside-the-agent-loop]], [[morris-humans-and-agents-in-software-engineering-loops]],
[[edwards-alexander-an-accidental-blackboard]]). **NOT INDEPENDENT** — this material is the same house
arguing for its own term and must not be counted as external corroboration for it. It is still valuable:
[[bockeler-tdd-inside-the-agent-loop]] remains the KB's only controlled **negative** eval in this area, and
that cuts against interest.
```

### 18.3 — `wiki/entities/mitchell-hashimoto.md` — UPDATE (low priority, one line)

**Paste (append):** a stated position worth dating —

```markdown
In [[macmanus-prs-not-welcome-software-factories|Latent.Space, 2026-09-01]] he goes further than the
maintainers being profiled: *"the future is that **large open source projects will close contributions
completely**."* A harder line than anything in [[hashimoto-my-ai-adoption-journey]], and the most extreme
position in the KB on where [[software-factory|maintainer-owned factories]] lead.
```

### 18.4 — Entity CREATEs, in priority order

Each needs only a short page; the source pages carry the detail. **Ordered — the first four earn a page
now; the last two can be deferred.**

1. **`wiki/entities/drew-breunig.md`** — independent writer at dbreunig.com, **three source pages in this
   batch**, and the only voice in the batch with no product in the space (which is its main virtue).
   Contributes: the eight-layer **situated agent** definition of a harness; the **end-of-the-free-lunch**
   economics of harness work; and the **attribution** argument about trained capabilities behind
   agent incidents. Surfaced into the KB via [[simon-willison]]'s 2026-08-23 quotation. Note the uncaptured
   companion **"Overfitting the Harness" (2026-05-10)** as a gap. Links:
   [[breunig-harnesses-are-situated-agents]], [[breunig-fable-and-the-end-of-the-free-lunch]],
   [[breunig-who-taught-the-models-to-do-that]], [[agent-harness]], [[harness-engineering]].
2. **`wiki/entities/zalando.md`** — European fashion retailer, >250 engineering teams; the KB's second
   **non-vendor production-scale** account of agentic engineering after [[stripe-minions-one-shot-coding-agents]],
   and the first about organization rather than tooling. Positions worth recording: **deliberate
   non-convergence** (*"way too early"* to standardise), **no central tool mandate**, an **LLM proxy from
   day one** (Jan 2024), a **risk-based PR approval bot** (self-reported figures — see
   [[autonomy-ladder]]), and *"using coding agents usually inhibits learning."* Links:
   [[zalando-agentic-engineering-snapshot]], [[agentic-coding]], [[agent-governance]],
   [[em-standardization-foundation]].
3. **`wiki/entities/laurie-voss.md`** — author of the KB's disambiguation primary for [[loop-engineering]];
   O'Reilly Radar / LinkedIn, 2026-07-29. The four-loop map (execution / task / product / system), the
   **oversight loop** he names, the **feedback criterion** (*"a loop without feedback is just a `for`
   statement"*), and the observation that autonomy is a dial per loop. Note the closing **vendor plug for
   Arize AX** (his sponsor/employer context) and that every figure in the piece is second-hand. Links:
   [[voss-what-the-hell-is-a-loop-anyway]], [[loop-engineering]], [[software-factory]].
4. **`wiki/entities/latent-space.md`** — a **venue**, not an author page (recommended over a
   `richard-macmanus` page, per the Batch F plan's suggestion: MacManus interviews rather than argues, and
   three source pages in this batch are his interviews). A paywalled Substack that is now one of the KB's
   main conduits for AI-engineering practitioner interviews and conference reporting; also the venue Voss
   cites for AIEWF coverage. Standing note: **interviews with founders about their own products** — treat
   product claims as vendor claims. Links: [[macmanus-prs-not-welcome-software-factories]],
   [[macmanus-schott-react-for-agents-flue-meta-harness]],
   [[macmanus-pocock-wayfinder-skill-fog-of-war]], [[voss-what-the-hell-is-a-loop-anyway]].
5. **`wiki/entities/andy-wong.md`** — practitioner writer (awongcm.io) running the
   context → harness → loop → graph ladder series; two source pages here. Valuable less for the ladder than
   for **publishing the provenance of "graph engineering" against his own interest** (half a joke, viral
   as a joke, contested as marketing, formalised as a preprint). Note his own framing is **prospective** in
   the graph piece. Links: [[wong-loop-engineering-teaching-ai-agents-how-to-think]],
   [[wong-graph-engineering-wiring-agents-into-an-organization]], [[loop-engineering]],
   [[graph-engineering]].
6. **`wiki/entities/andrew-miracle.md`** — Head of Product & Research at Tecmie; the KB's most fully
   specified single-practitioner rig (`github.com/koolamusic/claudefiles`). Contributes the **triangle of
   loops**, **goal-backward verification**, the **Amdahl-at-the-join** argument, and the **trust ledger**.
   Standing note: everything is configuration, **nothing is measured**. Links:
   [[miracle-my-loop-engineering-workflow]], [[loop-engineering]], [[autonomy-ladder]].

**Deferrable, but note the gaps.** `kief-morris` and `giles-edwards-alexander` (both covered adequately by
the [[thoughtworks]] update above); `fred-schott` and `matt-pocock` (each appears in two and one source
pages respectively); `vercel` and `warp` (both are now cited for figures on several pages — a `vercel`
entity page would be the right place to park the **VENDOR SELF-REPORT** marker once, rather than repeating
it); and **`geoffrey-huntley`, who has no entity page despite originating the [[ralph-loop]]** — the most
conspicuous entity gap this batch surfaced.

---

## 19. Not owned by this batch — `index.md` and `log.md`

Recorded here so the orchestrator can apply them; **this batch did not touch either file.**

- **`wiki/index.md`** — 18 new source-page entries needed (one line each, under the sources category).
- **`wiki/log.md`** — one entry in the house format:
  `## [2026-09-04] ingest   | Batch C: loop engineering and agentic practice (18 sources) — touched: 18 source pages + 34 delta items filed`
- **`wiki/overview.md`** — the synthesis genuinely shifted on two points and is worth a pass: **(1)** the
  loop vocabulary is unsettled, not settled — three incompatible taxonomies plus a live dispute about
  whether the harness is above or below the loop; **(2)** the batch's most-cited evidence is
  self-reported, so the standing caveat that this thread is "built almost entirely from
  advocate/practitioner primaries" got **stronger**, not weaker. The only new material with external
  rigour is a **preprint** (arXiv:2608.21156, and only via a summary) and a **peer-reviewed** paper already
  in the KB ([[borg-tornhill-code-for-machines-not-just-humans]], which this batch newly connects to
  Zalando's risk routing).
- **Suggested follow-up captures**, all cited-but-missing from this batch: Breunig, *"Overfitting the
  Harness"* (2026-05-10); Osmani's linked expertise write-up behind the 09-02 LinkedIn note; METR's
  Hugging Face incident report (Aug 2026); arXiv:2608.21156 (the graph-engineering survey) in full;
  Vercel's *"Building a software factory for AI SDK"*; Warp's automatic-triage-skill post; Latent.Space's
  *"Software Factories"*; and Geoffrey Litt, *"Understanding is the new bottleneck"* (2026-07-02), which is
  quoted at second hand on three pages now.
