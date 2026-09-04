---
title: "Ingest deltas — Batch B: the harness literature (10 captures)"
type: output
created: 2026-09-04
updated: 2026-09-04
sources: [guo-survey-question-answering-to-task-completion-harness-design, ning-code-as-agent-harness, wang-rethinking-evaluation-of-harness-evolution-for-agents, harnessx-composable-adaptive-evolvable-agent-harness-foundry, harnessforge-joint-harness-and-policy-evolution, sbco-verifier-grounded-harness-optimization, evo-bench-can-language-models-improve-agent-harness, mcateer-evolution-of-the-agent-harness, cao-agentic-software-restructuring-software-paradigm, graph-engineering-era-of-llm-agents-system-intelligence]
tags: [ingest-deltas, harness-engineering, work-order]
---

# Ingest deltas — Batch B: the harness literature

**Work order for the orchestrator. 24 delta items across 18 target pages, most-important-first.**
Ten source pages are written and complete (`wiki/sources/`, all ten carrying `raw_file:`); nothing in
`wiki/entities/`, `wiki/concepts/`, `wiki/index.md`, `wiki/overview.md` or `wiki/log.md` has been touched.
Every item below is ready to paste.

## Three rules that govern every item in this file

1. **Everything in this batch except the McAteer essay is an arXiv PREPRINT — including the critique.**
   The marker belongs at **every use of every number**, not once per page. arXiv is not peer review.
2. **There is a live methodological dispute and it must not be resolved in favour of the positive results.**
   [[wang-rethinking-evaluation-of-harness-evolution-for-agents|Wang et al. (arXiv:2607.12227v2)]] find that
   against matched-budget test-time-scaling baselines, automatic harness evolution "does not consistently
   outperform simple test-time scaling methods and exhibits limited generalization." **HarnessX's +14.5% and
   HarnessForge's +12.0% must never appear on this wiki as settled gains, and AHE's 69.7 → 77.0 must not
   either** — items 1, 4 and 5 below fix the two pages that currently carry the last of those undisputed.
3. **One thing must never be quoted.** Cao (arXiv:2606.05608) is widely cited for naming three roles
   ("intent architects, agent coordinators, and outcome auditors"). The capture records that the phrase is
   present in the paper but could **not** be returned as a clean verbatim sentence, so it was not filed as a
   quote. **Do not put that phrasing in quotation marks anywhere.** Use the verified abstract wording instead:
   *"its human role (intent architect rather than code author)"*.

---

## 1. `wiki/concepts/harness-engineering.md` — UPDATE (highest priority: it currently carries a contested number as settled)

### 1a. Attach the dispute to the AHE gain

**Anchor.** In the "How it shows up in practice" list, the bullet beginning
`- **The harness as a self-evolving surface** ([[ahe-agentic-harness-engineering|AHE, Lin et al. 2026]]):`
ends with the sentence `This is [[loop-engineering|loop engineering's]]` / `hill-climbing loop applied *to the harness itself*.`
**Insert the following bullet immediately after that bullet, at the same list level.**

```
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
```

*Why:* this page presents AHE's Terminal-Bench gain as an established result. It is the single most important
factual correction in the batch.

### 1b. Replace the "candidate papers" framing with "this is a field"

**Anchor.** Insert a new section **immediately before** the line `## Relationship to neighbours`.

```
## It is a research field now, not three candidate papers (2026-09-04)

The KB's watch config treated harness optimisation as a handful of named candidate papers. The evidence says
otherwise, and it is not close. **All of it is preprint evidence — arXiv is not peer review — but the *shape*
of a literature does not depend on peer review:**

- **Two independent surveys, two months apart, disjoint author sets**, both written to organise this literature:
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
  self-supervision ([[sbco-verifier-grounded-harness-optimization|SBCO]]).
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
```

*Why:* the batch settles the field question, corrects the config's assumption about Ning et al., and hands this
page an external placement it previously derived from practitioner chronology alone.

### 1c. Add the generality limit the batch establishes

**Anchor.** Insert immediately before the line `## Open questions`.

```
## Where automatic harness improvement does *not* reach

Two findings bound the practice, and both cut against the assumption that harness self-improvement generalises:

- **It is weakest where the workflow is prescribed.** [[evo-bench-can-language-models-improve-agent-harness|Evo-Bench]]
  finds autonomous evolution beats a hand-built harness on *General* tasks and excels at *Search*, but
  "struggles in **Office** tasks that demand highly specific processing workflows" *(arXiv preprint, not
  peer-reviewed)*. That is most enterprise work — and it is the closest thing to an experiment on
  [[dilger-harness-is-20-percent-requirements-are-80|Dilger's "the harness is the easy 20%"]] counterpoint
  below: a loop cannot discover a workflow nobody specified.
- **Self-improvement is only cheap where doing the task and editing the system need the same skill.**
  [[sbco-verifier-grounded-harness-optimization|SBCO]] names the precondition behind the Gödel-machine
  lineage: **self-referential** self-improvement "require[s] that the competence required to perform the task
  coincides or aligns well with the competence required for self-modification **which is the case for coding
  tasks**" *(arXiv preprint, not peer-reviewed)*. Outside coding it fails, and the workarounds are expensive.
  **Every harness-evolution result in this KB comes from coding or agent-benchmark tasks**, so the pattern's
  reach beyond them is unestablished. SBCO's own answer is *self-supervised rather than self-referential*:
  learn a decomposed bank of verifiers plus a harness policy from graded feedback, meta-agent fixed, no human
  labels — sensors as learned artifacts rather than authored ones.
```

*Why:* the KB's harness-improvement material is entirely coding-agent evidence and nothing currently says so.

### 1d. Extend the open questions

**Anchor.** The `## Open questions` section, at the end of its existing paragraph (which ends
`…the gain shrinks as the base saturates).`). **Append this paragraph.**

```
The batch adds three, all now stated by the field itself. **Can any of the reported gains survive a fair
protocol?** — the matched-budget and held-out-task objections in
[[wang-rethinking-evaluation-of-harness-evolution-for-agents]] are unanswered, and
[[evo-bench-can-language-models-improve-agent-harness|Evo-Bench]] answers two of the three concerns by
construction (auxiliary-task evolution to isolate harness gains from base-model strength; sensitivity-aware
stratified splitting against task-set overfitting) while leaving the budget objection open. **Can a harness be
improved without regression?** — [[ning-code-as-agent-harness|Ning et al.]] list "self-evolving harnesses
without regression" and "harness-level evaluation and **oracle adequacy**" as open problems, which is the
field's own maps agreeing with AHE's measured *regression blindness*. **Should the model be frozen?** — AHE
freezes it so gains are attributable; [[harnessforge-joint-harness-and-policy-evolution|HarnessForge]] argues
that freezing it is exactly what leaves harness–reasoner **compatibility** unoptimised, and co-evolves the
harness–policy pair instead. *(All preprints.)* These are opposed commitments, not a progression.
```

*Why:* the page's open questions were derived from one paper; the field has now formulated them itself.

### 1e. Frontmatter

Add to `sources:` — `guo-survey-question-answering-to-task-completion-harness-design`,
`ning-code-as-agent-harness`, `wang-rethinking-evaluation-of-harness-evolution-for-agents`,
`harnessx-composable-adaptive-evolvable-agent-harness-foundry`,
`harnessforge-joint-harness-and-policy-evolution`, `sbco-verifier-grounded-harness-optimization`,
`evo-bench-can-language-models-improve-agent-harness`, `mcateer-evolution-of-the-agent-harness`,
`graph-engineering-era-of-llm-agents-system-intelligence`. Bump `updated: 2026-09-04`.

---

## 2. `wiki/concepts/agent-harness.md` — UPDATE (the batch's biggest structural gift)

### 2a. The six runtime responsibilities — a functional spine the page lacks

**Anchor.** Insert a new section **immediately before** the line
`## Architecture patterns ([[firecrawl-what-is-an-agent-harness]])`.

```
## What the harness is *responsible for* — six coupled runtime duties (Guo et al. 2026)

The primitive list above says what a harness *contains*. [[guo-survey-question-answering-to-task-completion-harness-design|Guo
et al. (arXiv:2606.20683)]] decompose what it must *do*, in a survey whose organising question is "where does
the bottleneck in agent performance reside, in the foundation model, in the execution harness, or in the
coupling between them?" Their answer is the coupling: an agent is "a foundation model **coupled with** an
execution harness", and agent quality "emerges from the interaction between model capability, runtime
infrastructure, task structure, and evaluation design." *(arXiv preprint — not peer-reviewed.)* The six
responsibilities, verbatim:

| Responsibility | What it does |
| --- | --- |
| **Observation interface** | "transforms raw environment signals into model-usable observations" |
| **Context manager** | "determines what information enters the model context, when and in form" ([[context-engineering]]) |
| **Control loop** | "orchestrates the observe-reason-act-feedback cycle" ([[react-loop]], [[loop-engineering]]) |
| **Action interface** | "maps model outputs to executable operations" ([[model-context-protocol]]) |
| **State and artifact store** | "persists execution state and products" ([[long-running-agents]], [[decision-trace]]) |
| **Verification and governance layer** | "checks, constrains, and repairs execution" ([[feedforward-and-feedback-controls]], [[agent-governance]]) |

Read this as **orthogonal to, not competing with**, [[ahe-agentic-harness-engineering|AHE]]'s seven editable
component files above: Guo et al. name *what the harness must do*, AHE names *what you can edit*. Holding both
is more useful than choosing. The survey's own emphasis is on the word **coupled** — it devotes a subsection to
cross-layer interactions, which is the same non-additivity AHE measured empirically.

**The four-paradigm ladder** the same survey draws puts this page in sequence: **prompt engineering → workflows
and context engineering → harness engineering → agent-native training and co-evolution.** The rung boundaries
are crisply stated: prompting "addresses an expression problem"; context engineering "remains fundamentally
**feedforward**"; **harness engineering "closes the loop"** — "the model acts, observes environment responses,
and reasons over observations to decide its next step"; and paradigm 4 is "**internalization**; agentic
behaviors are increasingly trained into model parameters", plus co-evolution. That last rung is the academic
form of [[harness-absorption]]. *(Preprint.)* [[graph-engineering-era-of-llm-agents-system-intelligence|Feng et
al.]] independently name the same first three rungs but a different fourth ([[loop-engineering]]) and a fifth
([[graph-engineering]]) — see [[harness-engineering]] for both ladders.
```

### 2b. Harness absorption — the section the 2026-08-31 lint said was missing

**Anchor.** Insert a new section immediately after the section added in 2a (i.e. still before
`## Architecture patterns`).

```
## The harness is not a fixed surface — it gets absorbed ([[harness-absorption]])

[[mcateer-evolution-of-the-agent-harness|McAteer (Latent.Space, 2026-08-22)]] argues the harness and the model
improve on **two curves** — "what the harness asks of the model, and what the model can deliver in practice" —
whose gap *is* agent effectiveness, and that the 2025-26 jump in agent usefulness was the two curves crossing
rather than either one leaping. The consequence is a loop: **train → absorb → shed → repeat.** Models trained
inside their harness absorb harness capabilities into their weights (his cleanest instance: the
GPT-5.1-Codex-Max launch line, "The first model natively trained to operate across multiple context windows
through compaction" — auto-compaction migrating out of harness code into weights), after which the harness can
delete the scaffold. His metric follows: **"the measure of the pace of agent harness evolution is how much of
the harness you get to delete, while retaining the same capability level."** *(Practitioner essay, not a
paper.)*

Two things to hold with it. First, **the KB holds the opposite trend claim too**: [[langchain]]'s Harrison
Chase argues better models *expand* what harnesses must do rather than shrinking them (Claude Code 512k+ LOC
and growing — [[langchain-anatomy-of-an-agent-harness]]). Both can be true (prompt shrinks, codebase grows),
and the wiki should not pick. Second, **his numbers are all secondhand and must carry that marker**: the
much-quoted **Harness-Bench** spread — same model, 106 tasks, different harnesses, **52.4 → 76.2, a 23.8-point
spread with zero model change**, glossed "half the agent is the harness" — appears in the capture with no
author, venue or link, and **no primary capture of Harness-Bench exists in this KB**; the ARC-AGI-3 tripling
(GPT-5.6 Sol, 13.3% → 38.3% from retained reasoning + compaction) is [[openai]]'s own result about its own
model (**vendor self-report**, also relayed); the "deleted 80% of Claude Code's system prompt" claim is
[[anthropic]]'s about its own product, and is at least corroborated first-hand in
[[willison-fireside-chat-claude-code-team]] (per frontier model, not globally). Where he predicts the harness
**inverts** into an interface to scarce human attention, see [[attention-interface]].
```

### 2c. Code as the harness's substrate

**Anchor.** Insert immediately before the line `## Related`.

```
## The substrate claim: code, not prose ([[ning-code-as-agent-harness]])

A 42-author survey ([[ning-code-as-agent-harness|Ning et al., arXiv:2605.18747]] — **preprint, not
peer-reviewed**) frames the harness by its medium: "code is no longer only a target output. It increasingly
serves as an **operational substrate** for agent reasoning, acting, environment modeling, and execution-based
verification." Three layers — harness *interface* (code for reasoning / acting / environment modelling),
harness *mechanisms* (planning, memory, tool use, feedback-driven control), and *scaling* the harness to
multi-agent settings "where shared code artifacts support multi-agent coordination, review, and verification."
Its §3.4 headings land almost verbatim on this KB's vocabulary — "**Planning as Contract Formation**",
"Sandboxed Execution and Permissioned State Transition", "**Verification through Deterministic Sensors**"
(cf. [[feedforward-and-feedback-controls]], [[esaa-event-sourcing-for-autonomous-agents]]) — reached by a
different community. It closes by calling for a "**science of harness engineering**", i.e. a large survey
declaring the topic real and underdeveloped rather than new. Being a survey, it corroborates *no number*.
```

### 2d. Frontmatter

Add to `sources:` — `guo-survey-question-answering-to-task-completion-harness-design`,
`ning-code-as-agent-harness`, `mcateer-evolution-of-the-agent-harness`,
`wang-rethinking-evaluation-of-harness-evolution-for-agents`. Bump `updated: 2026-09-04`.

*Why (2a–2d):* the 2026-08-31 lint recorded that this page "cannot carry Breunig or McAteer" and that harness
absorption had zero wiki presence. This batch supplies both the absorption thesis and an external functional
decomposition, which together fix the page's shape rather than just adding to its list.

---

## 3. `wiki/concepts/harness-evolution.md` — **CREATE**

A new concept page, so the dispute lives in **one** place that four source pages and three concept pages can
link to instead of restating it. Suggested full content:

```
---
title: Harness Evolution
type: concept
created: 2026-09-04
updated: 2026-09-04
sources: [ahe-agentic-harness-engineering, harnessx-composable-adaptive-evolvable-agent-harness-foundry, harnessforge-joint-harness-and-policy-evolution, sbco-verifier-grounded-harness-optimization, evo-bench-can-language-models-improve-agent-harness, wang-rethinking-evaluation-of-harness-evolution-for-agents, ning-code-as-agent-harness, guo-survey-question-answering-to-task-completion-harness-design]
tags: [harness-engineering, agent-harness, loop-engineering, harness-evolution, contested, focus]
---

# Harness Evolution

**Automatic improvement of the [[agent-harness]] by an agent, with the base model usually frozen.** The
[[loop-engineering|hill-climbing loop]] pointed at the harness itself. As of 2026-09 it is a genuine research
field with four competing methods, a purpose-built benchmark, two organising surveys — and **a live dispute
about whether any of its reported gains are real**. Every source below is an **arXiv preprint; arXiv is not
peer review**, and that applies to the critique as much as to the results.

## Four methods, four bets

| Method | Bet | Reported *(all preprint, all contested — see below)* |
| --- | --- | --- |
| [[ahe-agentic-harness-engineering\|AHE]] (Lin et al., 2604.25850) | observability over **seven decoupled component files**; base model frozen; falsifiable change manifest + file-granular rollback | Terminal-Bench 2 pass@1 69.7% → 77.0% |
| [[harnessx-composable-adaptive-evolvable-agent-harness-foundry\|HarnessX]] (Chen et al., 2606.14249) | **typed primitives + a substitution algebra**; AEGIS trace-driven evolution; trajectories become harness updates *and* model training signal | avg **+14.5%** (max +44.0%) over five benchmarks |
| [[harnessforge-joint-harness-and-policy-evolution\|HarnessForge]] (Chen et al., 2606.01779v1) | the unit is a **harness–policy pair**; fault-guided harness tailoring + harness-conditioned policy alignment; *rejects* freezing the model | up to **12.0%** over strongest baseline (Qwen3-4B/8B) |
| [[sbco-verifier-grounded-harness-optimization\|SBCO]] (Kulkarni et al., 2608.10157) | **self-supervised, not self-referential**; learn a decomposed **bank of verifiers** + a harness policy by block coordinate ascent; fixed meta-agent, no human labels | matches/exceeds a self-modifying baseline at **4–5.5× less compute** |

Four groups, no shared authors, three countries, one problem. That plurality — not any single result — is the
evidence this is a field ([[harness-engineering]]).

## The dispute — read this before citing any number above

[[wang-rethinking-evaluation-of-harness-evolution-for-agents|Wang et al. (arXiv:2607.12227v2, 2026-08-27)]]
attack the **protocol**, not any one system: these methods "use unit test cases to search for harness
configurations and then report final performance on the same public benchmark." Two objections. **(1) Wrong
baseline** — harness evolution "is itself an iterative search procedure", so it must be compared with
task-level search / test-time-scaling baselines "under **matched feedback and inference budgets** to determine
whether its gains arise from improved harness design or from **additional search alone**." **(2) Same task set
for search and score** — so "the reported gains risk overfitting to that specific task set." Their result, on
**Terminal-Bench 2.1** with GPT-5.4 and Claude Opus 4.6: automatic harness evolution "**does not consistently
outperform simple test-time scaling methods and exhibits limited generalization**." Code is public.

**How the wiki treats this:** the four gains above are **contested claims cited with the dispute attached**,
never settled gains. Read the critique precisely too — "does not *consistently* outperform" is not "does not
work". And the dispute is genuinely unresolved, in both directions:

- Wang et al. test **frontier** bases (GPT-5.4, Opus 4.6). Both AHE and HarnessX report **largest gains where
  baselines are lowest / bases are weakest**, so a null result on frontier models is compatible with a real
  effect on weaker ones. Neither side has run the other's regime.
- **HarnessForge's heading list shows an explicit "Baselines and Fairness Protocol" (Appendix E)** and claims
  "favorable rollout-efficiency tradeoffs" — the nearest thing to a pre-emptive answer. *That appendix is not
  captured*; capturing it is the concrete next step if this dispute ever needs resolving.
- **[[evo-bench-can-language-models-improve-agent-harness|Evo-Bench]] answers two of the three concerns by
  construction** (auxiliary-task evolution isolates harness gains from base-model strength;
  sensitivity-aware stratified splitting targets cross-suite generalisation) and leaves the **budget**
  objection open.
- **SBCO's claim is already budget-relative** (equal-or-better output at 4–5.5× less compute), which is the
  *form* of claim the critique demands — though against a self-modifying baseline, not a test-time-scaling one.
- The critique is itself an **un-reviewed preprint** on a single benchmark family.

## What the field says about itself

Both surveys list the same worries as open problems, which is the strongest sign the dispute is internal rather
than adversarial: [[ning-code-as-agent-harness|Ning et al.]] name "**self-evolving harnesses without
regression**" and "harness-level evaluation and **oracle adequacy**";
[[guo-survey-question-answering-to-task-completion-harness-design|Guo et al.]] name "value-aware evaluation"
and "harness generalization versus specialization". AHE's own measured **regression blindness** (it predicts
which tasks an edit will *fix* ~5× better than random, which it will *break* only ~2× random) is the same
problem from inside a method paper.

## Where it does not reach

**Prescribed workflows:** Evo-Bench finds autonomous evolution beats hand-built harnesses on *General* and
*Search* tasks but "struggles in **Office** tasks that demand highly specific processing workflows" — i.e.
most enterprise work, and an experiment on [[dilger-harness-is-20-percent-requirements-are-80|Dilger's
"harness is the easy 20%"]]. **Non-coding domains:** SBCO's precondition — self-referential self-improvement
needs task competence and self-modification competence to coincide, "which is the case for coding tasks" —
means every result here is coding-or-benchmark evidence and its reach beyond that is unestablished. **Own
plateau:** Evo-Bench reports "critical temporal anomalies like early saturation"; AHE reports non-additive
component interactions capping the aggregate gain.

## Related

[[harness-engineering]] · [[agent-harness]] · [[loop-engineering]] · [[harness-absorption]] ·
[[agent-observability-and-evals]] · [[feedforward-and-feedback-controls]] · [[fitness-functions]]

_Sources: [[ahe-agentic-harness-engineering]] · [[harnessx-composable-adaptive-evolvable-agent-harness-foundry]] · [[harnessforge-joint-harness-and-policy-evolution]] · [[sbco-verifier-grounded-harness-optimization]] · [[evo-bench-can-language-models-improve-agent-harness]] · [[wang-rethinking-evaluation-of-harness-evolution-for-agents]]._
```

*(Note for the orchestrator: the `[[ahe-agentic-harness-engineering\|AHE]]` style escapes inside the table above
are an artifact of quoting a markdown table inside a fenced block — write them as normal `[[page|alias]]`
links in the real file.)*

*Why:* four method papers, a benchmark and a critique need one canonical home, or the dispute gets restated
five times and drifts. Also gives [[harness-engineering]] somewhere to point instead of growing further.

---

## 4. `wiki/concepts/loop-engineering.md` — UPDATE (second page carrying the contested number as settled)

### 4a. Mark the hill-climbing evidence as contested at the point of the number

**Anchor.** In the numbered loop-type list, item **4. Hill-climbing loop** ends with
`turned into a measured experiment (see the dedicated section below).` **Append immediately after that
sentence, inside the same list item.**

```
**Since 2026-07 those gains are contested.** [[wang-rethinking-evaluation-of-harness-evolution-for-agents|Wang
et al. (arXiv:2607.12227v2)]] argue automatic harness evolution is itself a search and must be compared against
test-time scaling under **matched feedback and inference budgets**, and that searching and reporting on one
benchmark risks overfitting to it; on Terminal-Bench 2.1 with GPT-5.4 and Claude Opus 4.6 it "does not
consistently outperform simple test-time scaling methods and exhibits limited generalization" *(also a
preprint, not peer-reviewed)*. Cite AHE's 69.7% → 77.0% with the dispute attached. The full picture — four
competing methods, a purpose-built benchmark, and both sides of the argument — is on [[harness-evolution]].
```

### 4b. Add the two limits at the end of the measured-loop section

**Anchor.** The `## The hill-climbing loop, measured ([[ahe-agentic-harness-engineering|AHE, Lin et al. 2026]])`
section ends `…that links this loop to` / `[[event-sourcing]] and the [[llm-wiki]].` **Append this paragraph
after it.**

```
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
```

### 4c. Frontmatter

Add to `sources:` — `wang-rethinking-evaluation-of-harness-evolution-for-agents`,
`evo-bench-can-language-models-improve-agent-harness`, `sbco-verifier-grounded-harness-optimization`,
`harnessx-composable-adaptive-evolvable-agent-harness-foundry`,
`harnessforge-joint-harness-and-policy-evolution`, `mcateer-evolution-of-the-agent-harness`. Bump `updated`.

*Why:* this page's hill-climbing section is the KB's most detailed treatment of harness self-improvement and
currently reads as settled. It is also the page most likely to be quoted into a deliverable.

---

## 5. `wiki/sources/ahe-agentic-harness-engineering.md` — UPDATE (source page, listed here rather than edited, since it predates this batch)

**Anchor.** The `## Caveats` section, at the end of its paragraph (ends `…qwen-3.6, gemini-3.1, deepseek-v4).`).
**Append.**

```

**Superseding context (added 2026-09-04, Batch B):** AHE's evaluation protocol — search against task feedback,
report on the benchmark searched against — is the specific target of
[[wang-rethinking-evaluation-of-harness-evolution-for-agents|Wang et al. (arXiv:2607.12227v2)]], who argue such
gains must first be shown to beat **matched-budget** test-time-scaling baselines and to hold on **held-out**
tasks, and who report on Terminal-Bench 2.1 (GPT-5.4, Claude Opus 4.6) that automatic harness evolution "does
not consistently outperform simple test-time scaling methods and exhibits limited generalization" *(also an
arXiv preprint, not peer-reviewed)*. **The 69.7% → 77.0% result on this page is therefore contested and must be
cited with the dispute attached.** Two counter-considerations keep it open rather than refuted: AHE's own
finding that gains are largest on *weaker* bases predicts a small effect in exactly the frontier regime Wang et
al. test, and the critique has not re-run AHE. AHE also no longer stands alone — three further methods
([[harnessx-composable-adaptive-evolvable-agent-harness-foundry|HarnessX]],
[[harnessforge-joint-harness-and-policy-evolution|HarnessForge]],
[[sbco-verifier-grounded-harness-optimization|SBCO]]), a purpose-built benchmark
([[evo-bench-can-language-models-improve-agent-harness|Evo-Bench]]) and two surveys
([[guo-survey-question-answering-to-task-completion-harness-design|Guo et al.]],
[[ning-code-as-agent-harness|Ning et al.]], whose §3.5 names AHE's pattern as a category) place it in a field.
See [[harness-evolution]]. Note also that **HarnessForge rejects AHE's frozen-model commitment** as leaving
harness–reasoner compatibility unoptimised — a live design disagreement, not a progression.
```

*Why:* this is the page every downstream citation of the 69.7 → 77.0 number goes through. Leaving it
undisputed defeats items 1a and 4a.

---

## 6. `wiki/concepts/graph-engineering.md` — UPDATE

**Anchor.** Insert a new section **immediately before** the line `## Relationship to neighbours`.

```
## Independent academic support — and a rival ladder (Feng et al. 2026)

This page's primary is a vendor one ([[prefect-loops-vs-graphs|Lowin/Prefect]], who sell orchestration).
[[graph-engineering-era-of-llm-agents-system-intelligence|Feng et al. (arXiv:2608.21156, 35 authors)]] reach
the same boundary independently — an **arXiv preprint survey, not peer-reviewed**, and a *position* rather
than a measurement, so it corroborates the argument and no result. Their version: individual intelligence hits
"a fundamental limit: many tasks require heterogeneous expertise, interdependent subtasks, parallel execution,
**independent verification**, and **persistent state**, exceeding any single agent's organizational capacity.
**Augmenting one agent's capabilities or context cannot resolve this architectural mismatch**; intelligence
must instead be distributed across specialized agents and organized at the system level." They name that
property **System Intelligence**, and Graph Engineering as its substrate: "explicit, dynamic, evolving graph
structures representing tasks, agents, and system states." Note the two named drivers of the mismatch are this
KB's own rules — *maker≠checker* (independent verification) and state outliving a context window
([[long-running-agents]]).

They also state the paradigm ladder outright: "**Prompt Engineering** to elicit model capabilities, **Context
Engineering** to manage information access, **Harness Engineering** to organize external tools and resources,
and **Loop Engineering** to support continual reflection and self-improvement" — this KB's sequence, from a
source unconnected to the practitioners who coined it, with graph engineering proposed as the fifth rung.
**But the ladder is contested:** [[guo-survey-question-answering-to-task-completion-harness-design|Guo et al.
(arXiv:2606.20683)]], two months earlier, agree on the first three rungs and make the fourth **"agent-native
training and co-evolution"**, with no loop or graph rung at all. Two independent surveys agree on
prompt → context → harness and diverge on what follows: one goes *up* into orchestration structure, one
*inward* into the model. They may not be rivals — coordination and internalisation can both be true — but the
wiki records both proposals and merges neither. Also worth holding against
[[mcateer-evolution-of-the-agent-harness|McAteer]], who expects **multi-agent orchestration to be absorbed
into model weights** next: two 2026-08 claims about the same near future pointing opposite ways.
```

Frontmatter: add `graph-engineering-era-of-llm-agents-system-intelligence`,
`guo-survey-question-answering-to-task-completion-harness-design`,
`mcateer-evolution-of-the-agent-harness` to `sources:`; bump `updated`.

*Why:* upgrades the page from vendor-thesis to vendor-thesis-with-independent-support, and records a taxonomy
conflict that would otherwise be silently resolved.

---

## 7. `wiki/concepts/harness-absorption.md` — **CREATE**

The 2026-08-31 lint recorded this concept as having *zero* wiki presence. Content outline (write it out
following house style; the substance is already drafted in item 2b, which this page should own and
[[agent-harness]] then summarise in two sentences):

- **Definition.** Harness capabilities migrating into model weights, after which the harness deletes the
  scaffold: **train → absorb → shed → repeat** ([[mcateer-evolution-of-the-agent-harness]]).
- **The two curves** — what the harness asks of the model vs. what the model delivers; the gap is agent
  effectiveness; the 2025-26 usefulness jump was a crossing, not a leap. Includes the four eras (ReAct →
  AutoGPT premature autonomy → IDE retreat → Claude Code) and the loop-amplification argument ("a loop
  amplifies the capability a model has"; 95% per step over 20 steps ≈ 36%).
- **The metric:** progress = how much harness you can delete at equal capability.
- **The academic form:** [[guo-survey-question-answering-to-task-completion-harness-design|Guo et al.]]'s
  paradigm 4 — "internalization; agentic behaviors are increasingly trained into model parameters" *(preprint)*.
  The mechanism as engineering: [[harnessx-composable-adaptive-evolvable-agent-harness-foundry|HarnessX]]
  "closes the harness-model loop by turning trajectories into both harness updates and model training signal";
  [[harnessforge-joint-harness-and-policy-evolution|HarnessForge]] co-evolves the harness–policy pair
  *(preprints, gains contested — [[harness-evolution]])*.
- **Evidence, every item marked:** compaction into weights (GPT-5.1-Codex-Max launch line — vendor);
  Claude Code system prompt −80% ([[anthropic]] self-report, first-hand in
  [[willison-fireside-chat-claude-code-team]], per frontier model); codex-1 RL-in-environment (vendor);
  Harness-Bench 52.4 → 76.2 across harnesses on 106 tasks (**secondhand, unlinked, no primary capture in this
  KB** — flag at every use); ARC-AGI-3 13.3% → 38.3% ([[openai]] self-report, relayed).
- **The counter-claim, given equal weight:** [[langchain-anatomy-of-an-agent-harness]] — better models expand
  what harnesses must do; Claude Code 512k+ LOC and growing.
- **What absorption leaves:** permissions, identity, trust, [[agent-legibility|legibility]] → [[attention-interface]].
- Related: [[agent-harness]] · [[harness-engineering]] · [[harness-evolution]] · [[context-engineering]] ·
  [[token-budget-quality-cliff]].

*Why:* a named, lint-flagged gap that this batch fills with a primary and an academic corroborator; it is also
the frame that decides whether harness investment is durable or temporary.

---

## 8. `wiki/concepts/attention-interface.md` — **CREATE**

- **Definition.** Once the model absorbs the computer-facing harness, the harness **inverts**: "The harness was
  born as the human interface to the model… The harness becomes the model's interface to our human attention"
  ([[mcateer-evolution-of-the-agent-harness]]). "Absorption doesn't end the harness. Absorption inverts the
  harness."
- **The scarcity premise**, quoting Ryan Lopopolo via the same piece: "The only fundamentally scarce thing is
  the **synchronous human attention** of my team." Tokens became abundant; attention did not — so the
  model↔harness gap "migrates across the human boundary" and becomes "the space between what the agent asks of
  the human, and what the human is able to answer."
- **The falsifiable prediction, with a date:** made 2026-08-22 — within a year every agentic-AI company ships
  a **human attention policy surface** as universally as AGENTS.md, governing "when it's allowed to interrupt
  you, when it should keep working, which decisions it can make alone and which decisions need your approval",
  and it becomes learnable ("every correction becomes useful data"). **Diarise a check for ~2027-08.**
- **Current sparks:** [[anthropic-effective-harnesses-long-running-agents]] progress files; agentic approval
  queues; and the KB's own [[append-and-review-note]] / [[decision-trace]] patterns as human-facing surfaces.
- **Caveats:** a practitioner prediction in an essay, no evidence, and the author's framing device (two curves)
  is narrative rather than measured.
- Related: [[agent-legibility]] · [[agent-governance]] · [[harness-absorption]] · [[agent-harness]] ·
  [[autonomy-ladder]] · [[unattended-coding-agents]] · [[guardian-agents]].

*Why:* a coined term with a dated, testable prediction, and the only page in the KB that would hold "what
harness work survives absorption" — which is a where-to-invest claim, not a curiosity.

---

## 9. `wiki/concepts/agent-engineering.md` — UPDATE

**Anchor.** The page's last body paragraph ends
`The "context engineering" mentioned above now has its own page:` / `[[context-engineering]].`
**Insert the following immediately after it, before the `_Source pages: …_` footer line.**

```
## An academic definition arrives — and a relocation of judgement (2026-06)

[[cao-agentic-software-restructuring-software-paradigm|Cao (arXiv:2606.05608)]] proposes **"Agentic
Engineering"** as "an expansion of the software engineering discipline into a new paradigm, distinct in its
**core object of study** (agent systems rather than static source code), its **control model** (LLM-driven
rather than human-predefined), and its **human role (intent architect rather than code author)**." It is a
**single-author arXiv position preprint — not peer-reviewed** — from a private company rather than an academic
lab, arguing a paradigm rather than reporting an experiment, and it was **retitled between versions** (v1: "The
End of Software Engineering…"; v2, current: "Agentic Software…"), which is itself a datum about how strongly the
claim survived a week.

Its significance here is narrow and real: **the KB's relocation-of-judgement thesis is no longer
practitioner-only.** [[addyosmani-earning-taste-and-judgment]], [[dilger-harness-is-20-percent-requirements-are-80]],
[[dilger-describing-without-solving-burns-you-out]], [[spec-driven-development]] and [[event-modeling]] all hold
that the human's work has moved from producing the artifact to specifying intent and adjudicating quality. Cao
states that as an academic claim. **It is an academic *statement* of the thesis, not academic *evidence* for
it.** His four "new human differentiators" — **intent articulation** ("specify goals with sufficient clarity
and constraint that agents can operate autonomously"), **architectural oversight** ("how multiple agents should
coordinate, what memory should be shared, and where human judgment must intervene"), **quality calibration**
("defining what 'good' looks like and building evaluation frameworks that agents can use for self-correction")
and **ethical governance** — map almost one-to-one onto [[spec-driven-development]],
[[multi-agent-orchestration]], [[agent-observability-and-evals]] and [[agent-governance]]. Treat that neatness
with some suspicion: a four-item list of virtues is easy to write and hard to falsify.

**Do not quote the three-role phrasing** ("intent architects, agent coordinators, and outcome auditors") often
attributed to this paper — the capture could not verify it as a verbatim sentence, so it is not filed as a
quote here. Use the abstract's own wording above. One tension to record rather than resolve: Cao's "the agent
itself is the software, and its decision logic is generated at runtime" cuts against this KB's substrate thread
([[event-sourcing]], [[decision-trace]], [[agent-readable-model-artifacts]]), which argues agent behaviour must
leave durable inspectable artifacts.
```

Frontmatter: add `cao-agentic-software-restructuring-software-paradigm`,
`guo-survey-question-answering-to-task-completion-harness-design`,
`mcateer-evolution-of-the-agent-harness` to `sources:`; bump `updated: 2026-09-04`.

*Why:* the page currently defines its own subject purely through [[langchain]]'s framing; and this is the
specific connection the batch was asked to make.

---

## 10. `wiki/concepts/agent-observability-and-evals.md` — UPDATE

**Anchor.** Insert a new section immediately before `## Production reference (PRINCE, 2026-06)`.

```
## Benchmark hygiene in the agent era (2026-07/08)

Two lessons from the harness-evolution literature that generalise well past harnesses. **All preprint
evidence — arXiv is not peer review.**

- **A search procedure must be compared against a budget-matched baseline.**
  [[wang-rethinking-evaluation-of-harness-evolution-for-agents|Wang et al. (arXiv:2607.12227v2)]] point out
  that if a method repeatedly evaluates and revises candidates using task feedback, it is *doing test-time
  scaling*, and its gains must be separated from "additional search alone" by giving a simple baseline the
  same feedback and inference budget. On Terminal-Bench 2.1 (GPT-5.4, Claude Opus 4.6) automatic harness
  evolution "does not consistently outperform simple test-time scaling methods". **Rule: whenever a result
  comes from iterating, ask what an equally expensive non-clever baseline scores.**
- **Searching and scoring on the same benchmark is contamination.** Same paper: "because the search and the
  final evaluation share the same benchmark, the reported gains risk overfitting to that specific task set" —
  hence held-out tasks. [[evo-bench-can-language-models-improve-agent-harness|Evo-Bench]] builds against this
  directly with "auxiliary-task evolution to identify tasks genuinely sensitive to framework improvements,
  followed by sensitivity-aware stratified splitting to ensure robust cross-suite generalization."
- **Verifiers can be learned rather than authored.** [[sbco-verifier-grounded-harness-optimization|SBCO]]
  learns "a decomposed bank of verifiers and a harness policy" from the agent's own graded feedback, "with a
  fixed meta-agent and no human labels" — evals as a co-optimised component. Useful and double-edged: a
  self-graded eval suite is precisely where a grader leak hides, and the capture gives no evidence about how
  that is controlled.

Both surveys list the same worry as unsolved: "harness-level evaluation and **oracle adequacy**"
([[ning-code-as-agent-harness]]), "value-aware evaluation" ([[guo-survey-question-answering-to-task-completion-harness-design]]).
The whole dispute lives on [[harness-evolution]].
```

Frontmatter: add `wang-rethinking-evaluation-of-harness-evolution-for-agents`,
`evo-bench-can-language-models-improve-agent-harness`, `sbco-verifier-grounded-harness-optimization`,
`ning-code-as-agent-harness`; bump `updated`.

*Why:* the budget-matched-baseline rule is reusable craft, and this is the page a future reader checks before
believing an agent benchmark number.

---

## 11. `wiki/concepts/multi-agent-orchestration.md` — UPDATE

**Anchor.** Insert a new section immediately before `## Capability-aligned decomposition — CEAD (deVadoss, 2026-05)`.

```
## Why one agent is not enough — the architectural-mismatch argument (Feng et al. 2026)

[[graph-engineering-era-of-llm-agents-system-intelligence|Feng et al. (arXiv:2608.21156)]] give the clearest
statement in the KB of why orchestration is architecture rather than plumbing — an **arXiv preprint survey,
not peer-reviewed**, and a position rather than a result. Some tasks "require heterogeneous expertise,
interdependent subtasks, parallel execution, **independent verification**, and **persistent state**, exceeding
any single agent's organizational capacity. Augmenting one agent's capabilities or context **cannot resolve
this architectural mismatch**." Note what two of those five drivers are: *maker≠checker*, and state that must
outlive a context window ([[long-running-agents]]). Their answer is [[graph-engineering]] — "explicit, dynamic,
evolving graph structures representing tasks, agents, and system states" — and the property they name is
**System Intelligence**.

The hard part is the shared state, and a second survey names it as an open problem from the code side:
[[ning-code-as-agent-harness|Ning et al.]] take an explicit position on a "Shared Code-Centric Harness
Substrate" with "harness-state convergence", and list "**Transactional Shared Program State and Semantic
Conflict Resolution**" among their open problems *(preprint)*. **That is ground the event-sourcing tradition
already claims to hold** — total ordering, an append-only log, conflicts detected before effects apply
([[esaa-event-sourcing-for-autonomous-agents]], [[agentic-event-driven-systems]],
[[event-sourced-agentic-patterns]]). The most direct research-gap-meets-existing-answer seam this batch
surfaces.
```

Frontmatter: add `graph-engineering-era-of-llm-agents-system-intelligence`, `ning-code-as-agent-harness`;
bump `updated`.

*Why:* two independent 2026 surveys converge on multi-agent shared state as *the* open problem, and one of the
KB's core threads is a candidate answer.

---

## 12. `wiki/concepts/event-sourced-agentic-patterns.md` — UPDATE

**Anchor.** Insert immediately before the line `## The unifying claim`.

```
## The gap the harness literature names, from the other side (2026-05/08)

Two large surveys of agent harnesses independently arrive at this page's problem statement as an **unsolved
research problem** — both **arXiv preprints, not peer-reviewed**. [[ning-code-as-agent-harness|Ning et al.
(arXiv:2605.18747, 42 authors)]] list "**Transactional Shared Program State and Semantic Conflict
Resolution**" and "**Human-in-the-Loop Safety and Accountability as Harness State**" among their open
problems, and take an explicit position on a shared harness substrate with "harness-state convergence";
[[graph-engineering-era-of-llm-agents-system-intelligence|Feng et al. (arXiv:2608.21156)]] argue multi-agent
systems demand explicit structures "to maintain **evolving execution states**". Ning et al. also list
"**verification through deterministic sensors**" and "**planning as contract formation**" as harness
mechanisms — which is [[esaa-event-sourcing-for-autonomous-agents|ESAA]]'s boundary-contract design in
different vocabulary.

That is worth stating plainly and with its limits: **the harness field's open problem is this thread's claimed
answer.** Total ordering, an append-only log, conflict detection before effects apply, and accountability as
*stored state* rather than asserted process are exactly what event sourcing supplies. What the KB does **not**
have is any evidence that the harness community has tried it and found it wanting, or tried it at all — no
paper in the harness batch cites event sourcing. So this is an *unexploited* seam and a research question
("does an event-sourced substrate solve harness-state convergence?"), not a settled advantage.
```

Frontmatter: add `ning-code-as-agent-harness`, `graph-engineering-era-of-llm-agents-system-intelligence`;
bump `updated`.

*Why:* highest-value cross-thread link in the batch, and it needs its "unexploited, not proven" caveat written
in from the start.

---

## 13. `wiki/concepts/context-engineering.md` — UPDATE

**Anchor.** The `## Relationship to harness engineering` section — append at its end.

```
An external, non-practitioner statement of the same boundary arrived in 2026-06:
[[guo-survey-question-answering-to-task-completion-harness-design|Guo et al. (arXiv:2606.20683)]] make
"workflows and context engineering" paradigm 2 of four and harness engineering paradigm 3, with the dividing
line stated in one word — **context engineering "remains fundamentally feedforward"**, whereas the harness
"**closes the loop**: the model acts, observes environment responses, and reasons over observations to decide
its next step." *(arXiv preprint — not peer-reviewed.)* That is [[feedforward-and-feedback-controls]]'s
guides-vs-sensors distinction reached independently by an academic group, and it is the crispest available
formulation of why these are two pages. In the same survey's decomposition, context engineering owns exactly
one of six harness responsibilities — the **context manager**, which "determines what information enters the
model context, when and in form" (see [[agent-harness]]). One further wrinkle from
[[mcateer-evolution-of-the-agent-harness|McAteer]]: context management is the clearest case of
[[harness-absorption]] — compaction has begun migrating from harness code into model weights, moving a
context-engineering concern inside the model.
```

Frontmatter: add `guo-survey-question-answering-to-task-completion-harness-design`,
`mcateer-evolution-of-the-agent-harness`; bump `updated`.

*Why:* the page's boundary with [[harness-engineering]] was argued from Böckeler alone; now it has an
independent formulation, plus a shrinking-scope warning.

---

## 14. `wiki/concepts/agent-legibility.md` — UPDATE

**Anchor.** Append immediately before the final `_Sources: …_` footer line.

```
**What survives absorption.** [[mcateer-evolution-of-the-agent-harness|McAteer (2026-08-22)]] argues that as
models absorb harness capabilities into their weights ([[harness-absorption]]), what is left is the set of
things no model can absorb — **permissions, identity, trust and legibility** — because "a model that absorbs
permissions into itself has dissolved permissions." On that reading this page describes the *durable* part of
harness work and much of the rest is temporary scaffolding. It is a practitioner prediction in an essay, not
evidence — but it is a direct claim about where to invest, and it converges with
[[cao-agentic-software-restructuring-software-paradigm|Cao]]'s academic version of the same relocation
(architectural oversight, quality calibration, ethical governance as the human differentiators — *single-author
arXiv position preprint, not peer-reviewed*). Where the surviving harness becomes a surface aimed at the human
rather than the model, see [[attention-interface]].
```

Frontmatter: add `mcateer-evolution-of-the-agent-harness`,
`cao-agentic-software-restructuring-software-paradigm`; bump `updated`.

*Why:* gives a somewhat descriptive page a stake in an argument about investment priority.

---

## 15. `wiki/concepts/agent-vs-workflow.md` — UPDATE

**Anchor.** Append at the end of the `## Why it matters` section.

```
**The far end of the distinction.** [[cao-agentic-software-restructuring-software-paradigm|Cao
(arXiv:2606.05608 — single-author position preprint, not peer-reviewed)]] pushes it past "the agent chooses
the path": "in [traditional software], code is the carrier of pre-written decision logic; in [agentic
software], **the agent itself is the software, and its decision logic is generated at runtime**", with code
"dynamically generat[ed] and discard[ed] as an instrumental resource". His delivery arc — licensed software →
SaaS → **Agent-as-a-Service** — reads each step as transferring complexity away from the user, "with the
agentic shift transferring not just operational complexity but **decision-making complexity itself**."
Record the tension rather than adopting the claim: if decision logic is generated at runtime and discarded,
auditability cannot live in the code, and has to come from a log
([[decision-trace]], [[event-sourced-agentic-patterns]], [[agent-explainability]]).
```

Frontmatter: add `cao-agentic-software-restructuring-software-paradigm`; bump `updated`.

*Why:* the page's own distinction gets its strongest formulation, and the auditability consequence is the KB's
own thread.

---

## 16. `wiki/entities/dan-mcateer.md` — **CREATE**

Flagged as needed by `outputs/batch-f-plan-2026-08-31.md`. Minimal entity page: **Dan McAteer**, agentic
engineer, writes *Attention Heads* ("essays on AI, human attention, philosophy, and contemplative practice");
guest author at *Latent.Space*. One KB source: [[mcateer-evolution-of-the-agent-harness]] (2026-08-22). Known
for the **two-curves / train→absorb→shed** account of model–harness co-evolution ([[harness-absorption]]) and
for coining the **[[attention-interface]]**. Note he is a commentator relaying others' figures rather than a
primary researcher — every number in his piece is secondhand, and the Harness-Bench figure he popularised has
**no primary capture in this KB**.

*Why:* he is now cited on several concept pages; and the entity page is the right place to record that his
numbers are relayed.

---

## 17. `wiki/index.md` — UPDATE (add ten source lines)

Add under the sources catalog, in the existing `- [[slug]] — one-line summary` style:

```
- [[guo-survey-question-answering-to-task-completion-harness-design]] — Guo et al. (arXiv 2606.20683, 17 authors, CityU HK/Sydney/Peking): survey, PREPRINT — agent = foundation model *coupled with* an execution harness; four paradigms (prompt → workflows/context → harness → agent-native training & co-evolution) and six runtime responsibilities (observation, context, control, action, state, verification); no numbers captured (focus)
- [[ning-code-as-agent-harness]] — Ning et al. (arXiv 2605.18747, 42 authors, UIUC/Meta/Stanford): survey, PREPRINT — "code as agent harness": code as the operational substrate for reasoning, acting, environment modelling and execution-based verification; calls for a "science of harness engineering"; open problems incl. regression-free harness evolution + transactional shared program state. NOT the method paper the config assumed (focus)
- [[wang-rethinking-evaluation-of-harness-evolution-for-agents]] — Wang et al. (arXiv 2607.12227v2): NEGATIVE RESULT, PREPRINT — harness evolution is itself a search, so must be compared under matched feedback/inference budgets, and searching+reporting on one benchmark risks overfitting; on Terminal-Bench 2.1 (GPT-5.4, Opus 4.6) it "does not consistently outperform simple test-time scaling methods and exhibits limited generalization". The dispute every harness-evolution number now carries (focus)
- [[harnessx-composable-adaptive-evolvable-agent-harness-foundry]] — Chen et al. (arXiv 2606.14249v3): PREPRINT — typed harness primitives via a substitution algebra + AEGIS trace-driven evolution; closes the harness–model loop both ways; avg +14.5% (max +44.0%) over five benchmarks — *CONTESTED, cite with the dispute*; affiliations not captured (focus)
- [[harnessforge-joint-harness-and-policy-evolution]] — Chen et al. (arXiv 2606.01779v1, Beihang/Tsinghua): PREPRINT — the agent system as a **harness–policy pair**, co-evolved via fault-guided harness tailoring + harness-conditioned policy alignment; rejects AHE's frozen-model commitment; up to 12.0% over strongest baseline (Qwen3-4B/8B) — *CONTESTED*; metadata gap: abs page unfetchable, no DOI/version history (focus)
- [[sbco-verifier-grounded-harness-optimization]] — Kulkarni et al. (arXiv 2608.10157): PREPRINT — verifier-grounded, **self-supervised rather than self-referential** harness optimisation for planning agents; learns a decomposed bank of verifiers + harness policy, fixed meta-agent, no human labels; matches/exceeds a self-modifying baseline at 4–5.5× less compute; names the limit that self-referential self-improvement only works where task and self-modification competence coincide ("the case for coding tasks") (focus)
- [[evo-bench-can-language-models-improve-agent-harness]] — Huang et al. (arXiv 2608.09096v2): PREPRINT — first benchmark for *harness-evolving capability* (Search/Office/General), built against base-model confounds and task-set overfitting; nine models, top gains 16.6 pts "closely approaching" (not beating) human-engineered baselines; **struggles on Office tasks with highly specific workflows**; early saturation (focus)
- [[graph-engineering-era-of-llm-agents-system-intelligence]] — Feng et al. (arXiv 2608.21156, 35 authors): survey/position, PREPRINT — names the ladder prompt → context → harness → **loop** engineering and proposes **graph engineering** as the fifth rung; "System Intelligence"; one agent's organisational capacity is the limit and augmenting it "cannot resolve this architectural mismatch". Independent academic support for [[graph-engineering]], whose primary was a vendor (focus)
- [[mcateer-evolution-of-the-agent-harness]] — McAteer (Latent.Space, 08-22): the model and harness curves *crossed*, they didn't leap; **train → absorb → shed → repeat**, so progress = how much harness you can delete; Harness-Bench 52.4→76.2 on 106 tasks with zero model change (*secondhand, no primary capture in the KB*); the harness inverts into an **attention-interface** for scarce human attention (focus)
- [[cao-agentic-software-restructuring-software-paradigm]] — Cao (arXiv 2606.05608v2): single-author position PREPRINT, retitled from "The End of Software Engineering…" — "the agent itself is the software, and its decision logic is generated at runtime"; licensed → SaaS → Agent-as-a-Service; "Agentic Engineering" with the human as **"intent architect rather than code author"** — the academic statement of the KB's relocation-of-judgement thesis. Do NOT quote its three-role phrasing (unverifiable in capture)
```

**Also fix an existing line while you are here.** Line ~115 describes AHE as a "**peer-review** primary". AHE
is an arXiv preprint (2604.25850v1); its source page says "peer-review-*grade*", which is a different claim.
Suggested replacement for that phrase: `the most rigorous primary (still a PREPRINT) for the self-improving
loop` — and append to that line: `— gains CONTESTED since 2026-07 by [[wang-rethinking-evaluation-of-harness-evolution-for-agents]]`.

*Why:* the index is the entry point every query starts from, and it currently overstates AHE's status in the
one word that matters.

---

## 18. `wiki/overview.md` — UPDATE

The synthesis shifted in three ways worth writing in (phrasing left to the orchestrator, since I have not read
the page):

1. **Harness optimisation is a research field, not three candidate papers** — two independent surveys, shared
   decomposition vocabulary across groups with no common authors in three countries, four distinct methods, a
   purpose-built benchmark, and internal methodological policing. All preprint evidence.
2. **And its headline results are contested.** No harness-evolution gain in this KB should be stated as
   settled; the wiki's position is *plural methods, disputed gains, unsolved regression problem*
   ([[harness-evolution]]).
3. **The relocation-of-judgement thesis now has an academic statement** ([[cao-agentic-software-restructuring-software-paradigm]]),
   and a competing prediction about the harness's future shape (absorption into weights →
   [[attention-interface]], vs. LangChain's "harnesses keep growing"). Also: the harness literature's own open
   problem — transactional shared state across agents — is this KB's substrate thread's claimed answer, and
   nobody in that literature has tried it.

---

## 19. `wiki/log.md` — APPEND one line

```
## [2026-09-04] ingest   | Batch B — the harness literature (10 captures: Guo + Ning surveys, HarnessX, HarnessForge, SBCO, Evo-Bench, Wang critique, Graph Engineering, McAteer, Cao) — touched: 10 source pages + 24 delta items across 18 pages (see outputs/ingest-deltas/batch-b-harness-papers.md). Settles the field question (harness optimisation is a research field, not 3 candidate papers) and opens a live methodological dispute: Wang et al. 2607.12227v2 find automatic harness evolution "does not consistently outperform simple test-time scaling methods" under matched budgets, so AHE/HarnessX/HarnessForge gains are now cited as CONTESTED. Ning et al. reclassified: survey, not method paper. Cao retitled between versions; its three-role phrase is NOT quotable.
```

---

## Notes for the orchestrator that are *not* page edits

- **`watch-config.json` needs correcting**, and this batch has the evidence: `candidate_primaries` treats
  harness optimisation as three named papers, and treats `ning-code-as-agent-harness` as a method paper. It is
  a field, and Ning et al. is a survey. Suggest replacing the three-paper list with a topic entry pointing at
  [[harness-evolution]] plus a watch on the dispute (any reply to arXiv:2607.12227).
- **Highest-value follow-up capture: Harness-Bench.** The batch's most-quoted number (52.4 → 76.2, 106 tasks,
  one model, many harnesses) reaches this KB only through McAteer, with no author, venue or link. Until a
  primary is captured, every use must be marked secondhand — and the number is load-bearing for the "half the
  agent is the harness" claim.
- **Second follow-up: HarnessForge Appendix E ("Baselines and Fairness Protocol") and Appendix G.** It is the
  one document in the batch that might already answer Wang et al.'s matched-budget objection, and it is
  uncaptured. Third: Guo et al. §7 (the per-benchmark harness-effect analyses) — the only place in the batch
  where an *independent* read of harness effects on SWE-bench Verified / Terminal-Bench 2.0 / WebArena might
  be found. Fourth: Cao §2.3 (the formal model), and the §4.1/§4.3 pages carrying the three-role phrase, so it
  can either be quoted properly or dropped.
- **Consistency sweep after applying:** grep the wiki for `77.0`, `69.7`, `14.5`, `12.0`, `16.6` and
  `Harness-Bench` and confirm each occurrence carries both the *preprint* marker and either the dispute or the
  secondhand marker.
