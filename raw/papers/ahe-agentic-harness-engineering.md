---
source_url: https://arxiv.org/abs/2604.25850
title: "Agentic Harness Engineering: Observability-Driven Automatic Evolution of Coding-Agent Harnesses"
author: Jiahang Lin, Shichun Liu, Chengjun Pan, Lizhi Lin, Shihan Dou, Xuanjing Huang, Hang Yan, Zhenhua Han, Tao Gui
publication: arXiv (arXiv:2604.25850v1 [cs.CL])
published: 2026-04-28
retrieved: 2026-07-27
type: paper
---

# Agentic Harness Engineering: Observability-Driven Automatic Evolution of Coding-Agent Harnesses

Jiahang Lin(1*‡), Shichun Liu(1*‡), Chengjun Pan(2*‡), Lizhi Lin(3), Shihan Dou(1), Xuanjing Huang(1), Hang Yan(3), Zhenhua Han(3†), Tao Gui(1†)

1 Fudan University  2 Peking University  3 Shanghai Qiji Zhifeng Co., Ltd

*Equal contributions. †Corresponding authors. ‡Work done during an internship at Shanghai Qiji Zhifeng Co., Ltd. Code: https://github.com/china-qijizhifeng/agentic-harness-engineering

arXiv:2604.25850v1 [cs.CL] 28 Apr 2026

> Note (capture): verbatim capture of the main body (Abstract through Limitations). The References list and Appendices A–E (full experimental setup, prompts/configurations, qualitative trajectory case studies, per-round self-attribution breakdown) are not reproduced here; see the arXiv HTML for those. Inline citation markers have been reduced to plain `[n]` and HTML math-rendering artifacts (doubled numbers/subscripts, e.g. `77.0%77.0%`, `H0H_0`) normalized for readability; wording is otherwise unchanged.

## Abstract

Harnesses have become a central determinant of coding-agent performance, shaping how models interact with repositories, tools, and execution environments. Yet automating harness engineering is hard: a heterogeneous action space, sparse and noisy evaluation signal, multi-million-token trajectories, and edits whose effect is hard to attribute to the next round's outcomes. We introduce Agentic Harness Engineering (AHE), a framework that automates harness-level evolution by instrumenting the three stages of any engineering loop (component editing, trajectory inspection, and decision making) with matched observability pillars: ❶ *component observability* gives every editable harness component a file-level representation so the action space is explicit and revertible; ❷ *experience observability* distills millions of raw trajectory tokens into a layered, drill-down evidence corpus that an evolving agent can actually consume; and ❸ *decision observability* pairs every edit with a self-declared prediction, later verified against the next round's task-level outcomes. Together, these pillars turn every edit into a falsifiable contract, so harness evolution proceeds autonomously without collapsing into trial-and-error. Empirically, ten AHE iterations lift pass@1 on Terminal-Bench 2 from 69.7% to 77.0%, surpassing the human-designed harness Codex-CLI (71.9%) and the self-evolving baselines ACE and TF-GRPO. The frozen harness transfers without re-evolution: on SWE-bench-verified it tops aggregate success at 12% fewer tokens than the seed, and on Terminal-Bench 2 it yields +5.1 to +10.1 pp cross-family gains across three alternate model families, indicating the evolved components encode general engineering experience rather than benchmark-specific tuning. These results position observability-driven evolution as a practical pathway to keep coding-agent harnesses continually improving.

Figure 1: AHE evolves a bash-only seed past every human-designed and self-evolving baseline on Terminal-Bench 2. All three role agents share one base model, isolating the gain to harness edits rather than analyzer or editor capability.

## 1 Introduction

Coding agents are now widely used for long-horizon software-engineering tasks, with measurable progress on real GitHub issue resolution [13, 40, 7] and multi-step terminal workflows [19]. This progress is driven not only by the underlying language model but also by a substantial surrounding *harness* [28, 17, 37, 39, 31, 29], which includes components such as the system prompt, tools, and middleware that mediate the model's interaction with the file system, shell, and external services.

Harness design materially shifts task completion on long-horizon coding benchmarks, even with the base model held fixed [35, 37]. In current practice, human harness developers inspect trajectories, identify recurring failure patterns, and revise prompts, tools, or middleware accordingly. Yet this manual loop has not kept pace with advancing base-model capability: it is expensive, hard to scale, and difficult to study scientifically, with improvements distributed across design decisions [31].

An intuitive direction is to introduce a separate evolution agent that optimizes harness components based on experience [1, 43, 4]. Existing approaches mostly optimize individual harness components, typically the prompt [30, 44, 18] or an in-context playbook [43], with few jointly evolving the full set of editable components [15]. In practice, long and unstructured rollout trajectories offer the evolution agent little machine-consumable signal, and tightly coupled harness frameworks make edits beyond the prompt error-prone. This leaves the central question of agent-driven harness evolution open:

How can an evolution agent stably evolve all components of a coding agent's harness?

Our central insight is that this question is bottlenecked by *observability*, not by agent capability: once the evolution agent receives structured context over a clear action space, it can reliably converge on better harness designs [32, 47]. We implement this in Agentic Harness Engineering (AHE), a closed loop driven by three observability pillars: ❶ *component observability* via a decoupled harness that exposes seven editable component types as files, so each failure pattern maps cleanly to a single component class; ❷ *experience observability* via a layered, drill-down evidence corpus distilled from millions of raw trajectory tokens, so the evolver consumes structured root causes rather than raw logs; and ❸ *decision observability* via a change manifest that pairs every edit with a self-declared prediction, later verified against the next round's task-level outcomes, so each edit becomes a falsifiable contract and ineffective ones are reverted at file granularity.

We empirically validate AHE on Terminal-Bench 2 [19]: ten iterations lift pass@1 from 69.7% to 77.0%, surpassing the human-designed Codex [23] and the self-evolving baselines ACE [43] and TF-GRPO [4]. Without further evolution, the frozen harness transfers to SWE-bench-verified [13] and to four alternate base models, with the largest gains on weaker bases, suggesting that AHE encodes coordination patterns that less capable models lean on more heavily. A component ablation pinpoints where this gain lives: tools, middleware, and long-term memory each carry the improvement on their own, while the system prompt alone regresses, indicating that factual harness structure transfers across tasks and models whereas prose-level strategy does not.

This paper makes three contributions:

- We formulate *agent-driven harness evolution* for coding agents and identify *observability across components, trajectories, and decisions* as the design pivot that enables joint evolution of the full harness rather than prompt-only edits.
- We propose AHE, which turns every harness edit into a falsifiable, file-level contract through three observability pillars: a decoupled component substrate, a layered trajectory-distillation pipeline, and a change manifest whose self-declared predictions are verified by next-round task deltas.
- We empirically show that AHE lifts pass@1 on Terminal-Bench 2 from 69.7% to 77.0%, surpasses hand-written and automated baselines, and produces a frozen harness that transfers across benchmarks and base-model families, with the gain concentrated in tools, middleware, and long-term memory rather than the prompt.

## 2 Related Work

### 2.1 Harness Engineering and Evaluation for Coding Agents

Harness engineering refers to the practice of designing the system surrounding the model, including its tools, interfaces, memory, execution constraints, and feedback loops, which together shape what an agent can do on long-horizon tasks [28, 17, 35, 3, 31, 29]. Concretely, the harness mediates how the model perceives and acts on its environment: it exposes the action and observation interfaces over which tool-augmented reasoning unfolds [3], custom agent-computer interfaces for repository navigation, file editing, and command execution [39], as well as sandboxed execution and orchestration support that keep long-horizon runs reproducible [37].

Verifying that such systems actually help has driven the parallel maturation of coding-agent evaluation along two axes: task horizon and environmental realism. Coverage extends from short-horizon function-level benchmarks focused on contamination and freshness control [46, 11], through repository-scale executable patch resolution [13, 40, 7], to multi-hour, terminal-driven workflows that exercise long-horizon, realistic execution [20, 5, 19]. A parallel infrastructure track packages executable runtimes and verifiers around these benchmarks [26, 12, 41], whose attention to reproducible, traceable, and verifiable execution directly motivates the observation system AHE builds on.

### 2.2 Automated Optimization of LLM Agents

Approaches to automated agent optimization differ in what evidence the optimizer observes and what it can edit. Some revise the agent's own outputs through episodic critique and reflection [18, 30]. Others target prompts and instructions [14]: structured playbooks [43], semantic-advantage priors [4], jointly optimized instruction-demonstration pipelines for multi-stage programs [25], and reflective updates driven by Pareto-frontier traces [1]. A separate line edits program structure itself, in the form of skill libraries [36], scored program and agent archives evolved through mutation [22, 10], and graph-structured workflows searched or learned from rollouts [42, 45].

AHE tunes the full harness as a combinatorial whole rather than a single editable surface, so cross-component trade-offs become legible to the optimizer. It also keeps the human prior minimal, leaving methodology for the optimizer to discover from rollouts rather than fixing it by hand. We describe the substrate, trajectory analysis, and iteration that realize these choices in Section 3.

## 3 Method

AHE turns harness optimization into a closed loop driven by another agent, with the base model held fixed and only the explicit harness edited. Our design principle is that every phase of this loop must be *observable*: AHE faithfully records the artifacts each phase produces (the harness components an iteration writes, the rollout trajectories it generates, the edit decisions it commits) and represents them in structured, layered forms that another agent can read and act on.

Three observability layers implement this principle. Component observability (§3.1) is realized by a decoupled, file-level harness substrate that maps each failure pattern to a single component class. Experience observability (§3.2) is realized by a layered evidence corpus distilled from raw rollouts and indexed for drill-down access. Decision observability (§3.3) is realized by a change manifest that pairs every edit with a self-declared prediction the next round verifies. The three layers compose into the iteration of Algorithm 1, which runs unattended round after round.

### 3.1 NexAU: an editable, decoupled harness substrate

We instantiate the harness H on the NexAU framework [21, 33], which exposes seven orthogonal component types as explicit files at fixed mount points in a single workspace: system prompt, tool description, tool implementation, middleware, skill, sub-agent configuration, and long-term memory. The component types are loosely coupled, so adding a middleware does not require editing the system prompt, and adding a skill does not require touching any tool.

This decoupling is what realizes component observability: each failure pattern maps to a single component class, giving the evolve agent a clean action space and localizing every pass-rate change to one file rather than scattering it across hundreds of lines of unstructured prompt prose. Each logical edit becomes one commit on the workspace's git history, which yields file-level diffs and rollback granularity for free.

Our seed harness H0 is deliberately minimal: a single shell-execution tool, no middleware, no skills, no sub-agents. A seed already fitted to the target benchmark would contaminate every subsequent edit's attribution, since we could not tell whether a gain came from the loop or from the seed. The minimal seed forces every component AHE adds to earn its place against measured rollouts.

### 3.2 Agent Debugger: layered trajectory evidence

We generate k traces for each task in a benchmark using a harness H, which may contain errors resulting from the deficiencies of the harness that can be acted on, but scattered across millions of tokens of raw messages. To extract insights from agent trajectories and enable experience observability, we apply the Agent Debugger [16] framework to use an agent to explore trajectories framed as a navigable, file-based environment where each trajectory message lives in its own file and is reached through generic shell and scripting tools. Traces with the same query are placed in one environment, and the debugger is required to analyze the root cause of the failure or the success pattern, which is stored in a *per-task analysis* report for each task. The analysis also includes pass/fail status of the task to ground the Evolve Agent. Finally, a *benchmark-level overview* is aggregated from every report into a single document as an entry point for every iteration.

In addition to these reports, we also provide *original* traces in case the agents need to verify the claims in the reports. The traces are provided both in raw form and lightly processed to remove unnecessary content. All of this content is provided as files allowing progressive disclosure [27] which saves on tokens and enables better agent decisions.

Figure 2: The AHE pipeline links three observable surfaces into one closed loop. Components, rollout experience, and edit decisions each surface as structured artifacts another agent reads, and every edit becomes a falsifiable prediction the next round verifies.

### 3.3 Evolve Agent: evidence-driven, auditable edits

The Evolve Agent closes the AHE loop. In each round it reads the layered evidence corpus produced by the Agent Debugger, decides which harness components to add, modify, or remove, applies those edits to the workspace, and records the reasoning behind every edit. Two constraints govern these edits, and together they realize decision observability: every edit becomes a falsifiable, file-level claim recorded in a versioned manifest, and the next round's verdict either confirms or reverts it.

The first constraint is controllability: the Evolve Agent writes only inside the harness workspace, while the runs directory, tracer, verifier, and LLM configuration are read-only, and the seed system prompt (Appendix B.1) is marked non-deletable. These restrictions block the shortcuts an unconstrained self-modifier would take, such as disabling the verifier, swapping the model, or raising the reasoning budget, and keep every recorded gain attributable to harness edits.

The second constraint is that every change is evidence-driven and ships with a recorded prediction. Each edit attaches a manifest entry that names the failure evidence, the inferred root cause, the targeted fix, and a predicted impact comprising both expected fixes and at-risk regressions; this manifest is the loop's evidence ledger (see Appendix B.2). In the next round, the loop intersects the predicted-fix and predicted-regression sets with the observed task-level deltas to produce a per-edit verdict. Each edit thereby becomes falsifiable by the next evaluation, which replaces rationale-driven self-justification with a measurable contract between rounds.

Algorithm 1 — AHE outer loop.

```
Input: seed harness H0, base model M, benchmark D, rollouts per task k, max iterations N
1: Hbest ← H0
2: for t = 1 to N do
3:   Tt ← Rollout(M, H_{t-1}, D, k)          ▷ phase 1: k rollouts per task
4:   T̃t ← Clean(Tt)                          ▷ phase 2: drop base64, dedup tool output
5:   if t ≥ 2 then                            ▷ phase 3: attribute prior manifest, then rollback
6:     Vt ← Attribute(C_{t-1}, T_{t-1}, Tt)
7:     H_{t-1} ← Rollback(H_{t-1}, Vt)
8:   else
9:     Vt ← ∅
10:  end if
11:  Rt ← AgentDebugger(T̃t)                   ▷ phase 4: layered distillation
12:  (Ht, Ct) ← Evolve(H_{t-1}, Rt, Vt)       ▷ phase 5: workspace edits + new manifest
13:  Commit(Ht, Ct, t)                        ▷ phase 6: tag iteration in git
14:  if Pass@1(Tt) > Pass@1(Hbest) then Hbest ← Ht
15:  end if
16: end for
17: return Hbest
```

Algorithm 1 composes the three substrates into one iteration: rollout, clean, attribute the prior manifest and revert rejected edits, distill, edit, commit. We run k ≥ 2 rollouts per task so each task carries a pass-rate signal, which stabilizes pass@1 and lets partial-pass tasks anchor comparative diagnosis. Attribution runs *before* distillation, so its verdict lands inside the evidence corpus and binds each prior manifest entry as a contract rather than a rationale. A one-shot explore agent (Appendix B.3) runs in parallel with iteration 1 to seed a small number of reusable skills from the NexAU source and public coding-agent references. These skills receive no special protection: from iteration 2 onward the Evolve Agent may keep, refine, or remove them based on observed rollouts.

## 4 Experiments

We organize our empirical study around three questions: where AHE sits on the map of existing approaches to harness design, whether what it produces is portable beyond its optimization target, and what inside the loop drives the gain.

Research Questions:

1. RQ1 (§4.2): Why agentic harness engineering, rather than human-engineered harnesses or other automated methods?
2. RQ2 (§4.3): Does agentic harness engineering overfit to its optimization target?
3. RQ3 (§4.4): What are agentic harness engineering's strengths and limitations, and what explains them?

### 4.1 Setup

**Evaluation.** We drive evolution on the full 89 tasks of Terminal-Bench 2 [19], split as 4 easy, 55 medium, and 30 hard, with per-task timeout extended to 1 hour. For cross-benchmark transfer we evaluate the AHE harness on SWE-bench-verified [13], 500 tasks across seven repositories. We report two metrics per configuration: pass@1, the mean binary success rate over k rollouts per task; and tokens/trial, the mean per-trial total of prompt plus completion tokens across all LLM calls, in thousands. Infrastructure-aborted or timed-out trials count as failures under pass@1 (matching the official terminal-bench leaderboard) and are excluded from token means to avoid truncated figures. Runtime infrastructure (framework, dispatcher, sandbox, tracer, and concurrency) is detailed in Appendix A.

**Models.** For both the evolution loop and the main experiment of §4.2, all three role agents (the Code Agent, the Agent Debugger, and the Evolve Agent) share one base model, GPT-5.4 [24] at the high reasoning setting. For cross-model transfer (§4.3), we re-evaluate the Code Agent on five alternate bases: GPT-5.4 at medium and xhigh reasoning, qwen-3.6-plus [34, 38], gemini-3.1-flash-lite-preview [8], and deepseek-v4-flash [6].

### 4.2 RQ1: Main Results

Table 1: Pass@1 on Terminal-Bench 2 across 89 tasks, by official difficulty. NexAU0 is the shared seed; ACE, TF-GRPO, and AHE are three self-evolution loops layered on top of it.

| Method | All (89) | Easy (4) | Med. (55) | Hard (30) |
| --- | --- | --- | --- | --- |
| *Human-designed harness* | | | | |
| opencode | 47.2% | 75.0% | 52.7% | 33.3% |
| terminus-2 | 62.9% | 75.0% | 74.5% | 40.0% |
| Codex | 71.9% | 75.0% | 80.0% | 56.7% |
| *Self-evolved from NexAU0* | | | | |
| NexAU0 | 69.7% | 87.5% | 78.2% | 51.7% |
| ACE | 68.9% | 91.7% | 78.2% | 48.9% |
| TF-GRPO | 72.3% | 100.0% | 79.4% | 55.6% |
| AHE | 77.0% | 100.0% | 88.2% | 53.3% |

We run a single AHE campaign of ten iterations from the bash-only NexAU0 seed (§3.1), with k=2 rollouts per task per iteration on Terminal-Bench 2, finishing in roughly 32 hours; the best resulting configuration is reported as AHE. The two self-evolve baselines ACE [43] and TF-GRPO [4] start from the same NexAU0 seed.

**AHE outperforms both human-designed and self-evolve baselines.** AHE outperforms every baseline on our panel: three human-designed harnesses, opencode [2], terminus-2 [9], and Codex [23], and the two self-evolve baselines ACE and TF-GRPO. Figure 1 shows the gain accumulates across iterations, with continued evolution pushing pass@1 further above the NexAU0 seed. By difficulty, the only exception is the Hard tier, where AHE marginally trails Codex. We trace this gap to interference between AHE's components on long-horizon tasks rather than to a missing capability: swapping AHE's long-term memory alone into the NexAU0 seed, without the other AHE components, already surpasses Codex on Hard (§4.4.1).

**Prompt-only self-evolution misses the components that carry AHE's gain.** The gaps to ACE and TF-GRPO trace to a layer mismatch. ACE distills natural-language playbooks the agent reads in-context, and TF-GRPO is a trajectory-feedback variant of GRPO that reinforces successful tool sequences; starting from the same NexAU0 seed as AHE, neither method opens the surrounding scaffolding to edits. AHE jointly evolves system prompt, tools, middleware, and long-term memory across iterations, and §4.4.1 quantifies which of these layers carries the improvement: swapping in AHE's tools, middleware, or long-term memory alone yields +3.3, +2.2, and +5.6 pp, while the system prompt alone is −2.3 pp. The harness components ACE and TF-GRPO never edit are exactly where the gain lives.

### 4.3 RQ2: Generalization to Unseen Tasks and Base Models

AHE's harness is evolved on Terminal-Bench 2 with GPT-5.4 high. We probe whether it encodes general coding-agent experience or overfits to that target by re-using the workspace as-is, without further evolution, in two off-target settings: a different task surface (SWE-bench-verified) and four alternate base models.

Table 2: Cross-benchmark transfer on SWE-bench-verified (all columns run on GPT-5.4; evolved on terminal-bench-long-time, evaluated without in-domain re-evolution).

| Repo | N | ACE | TF-GRPO | NexAU0 | AHE | ACE tok(k) | TF-GRPO tok(k) | NexAU0 tok(k) | AHE tok(k) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| All | 500 | 74.6% | 74.2% | 75.2% | 75.6% | 679 | 582 | 526 | 461 |
| django | 231 | 79.2% | 78.8% | 79.2% | 81.0% | 707 | 583 | 527 | 484 |
| sympy | 75 | 69.3% | 68.0% | 70.7% | 70.7% | 602 | 572 | 494 | 479 |
| sphinx-doc | 44 | 61.4% | 65.9% | 68.2% | 70.5% | 990 | 848 | 731 | 656 |
| matplotlib | 34 | 70.6% | 70.6% | 73.5% | 73.5% | 622 | 530 | 486 | 391 |
| scikit-learn | 32 | 93.8% | 93.8% | 93.8% | 87.5% | 451 | 378 | 307 | 257 |
| pydata | 22 | 77.3% | 77.3% | 77.3% | 72.7% | 563 | 516 | 386 | 338 |
| astropy | 22 | 59.1% | 59.1% | 54.5% | 50.0% | 546 | 470 | 667 | 277 |

**Cross-benchmark generalization.** We re-point the AHE harness at SWE-bench-verified against the seed and the two self-evolve baselines (NexAU0, ACE, TF-GRPO) under identical infrastructure (Table 2). ACE and TF-GRPO both regress below the untouched NexAU0 seed in aggregate success while spending 11% to 29% more tokens than the seed: the playbook ACE injects and the trajectory distribution TF-GRPO reinforces were distilled on terminal-bench traces and ride the prompt at every model call, so on a different task surface that text adds cost without reshaping the underlying policy. AHE instead achieves the highest aggregate, with the seed-relative gain concentrating on django and sphinx-doc, the two largest and most token-expensive repositories whose multi-step edit-and-verify loop matches the structure AHE's tools, middleware, and long-term memory compress on Terminal-Bench 2. Marginal regressions appear only on the three smallest repositories, consistent with pass@1 variance on small repos exceeding the per-repo gain. AHE also cuts aggregate tokens by 32% against ACE, 21% against TF-GRPO, and 12% against the seed: encoding behavior in tools, middleware, and memory rather than in the prompt avoids the per-call re-derivation cost that prompt-only baselines pay.

Figure 3: Cross-model transfer on terminal-bench-long-time, 89 tasks. The AHE workspace evolved on GPT-5.4 high is re-evaluated on each base without further evolution, paired against the NexAU0 seed on the same base.

**Cross-model generalization.** We re-evaluate both the NexAU0 seed and AHE on the five alternate bases listed in §4.1. Figure 3 reports five positive pass@1 gains from +2.3 to +10.1 pp. Cross-family gains dominate within-family ones: deepseek-v4-flash moves +10.1 pp from 51.7% to 61.8%, qwen-3.6-plus +6.3 pp from 56.2% to 62.5%, and gemini-3.1-flash-lite-preview +5.1 pp from 36.5% to 41.6%, all above the +2.3 pp on GPT-5.4 medium and xhigh. We read this as bases further from saturation leaning more on the coordination patterns AHE has fixed inside tools, middleware, and long-term memory, while a stronger base re-derives the same coordination from its prompt at low marginal cost.

Within one family the profile is non-monotone: +2.3 pp on medium, +7.3 pp on high from §4.2, and +2.3 pp on xhigh. AHE's step budget and per-task timeout were fitted to GPT-5.4 high during evolution; medium has more time-per-step slack but loses a reasoning tier of raw capability, while xhigh pushes more trials past the per-task timeout, which our pass@1 convention counts as failures. Either direction discounts the gain. The load-bearing finding is that all five gains land positive: the AHE workspace is not specific to one provider's idioms or one reasoning depth. Their magnitude tracks the evolution operating point rather than raw base capability, so we treat the timeout-budget coupling as a generalization hazard discussed in our Limitations section.

### 4.4 RQ3: Analysis

We analyze the loop along two architectural choices that §3 places weight on: decomposed components (§4.4.1) and self-declared attribution (§4.4.2).

#### 4.4.1 RQ3a: where value accumulates across components

Table 3: Component-level ablations on terminal-bench-long-time. Each "+ X only" row swaps a single AHE component into the NexAU0 seed.

| Variant | All (89) | Easy (4) | Medium (55) | Hard (30) |
| --- | --- | --- | --- | --- |
| NexAU0 | 69.7% | 87.5% | 78.2% | 51.7% |
| + memory only | 75.3% | 50.0% | 83.6% | 63.3% |
| + tool only | 73.0% | 75.0% | 87.3% | 46.7% |
| + middleware only | 71.9% | 100.0% | 81.8% | 50.0% |
| + system_prompt only | 67.4% | 75.0% | 78.2% | 46.7% |
| AHE full | 77.0% | 100.0% | 88.2% | 53.3% |

Table 3 decomposes the AHE gain at the component level. Each "+ X only" row takes the NexAU0 seed and swaps in one component from the fully evolved AHE configuration, namely long-term memory, tools, middleware, or system prompt, leaving the other three at their seed defaults. Three of the four single-component variants outperform the seed; the system-prompt swap is the only regression.

**Each component owns a different failure surface.** Memory adds 12 boundary-case lessons (performance margin, queued-over-limit cancellation, evaluator-style closure, source-packaging layout); on Hard the lessons lift it above full AHE, while on Easy they reduce to superfluous re-verification. Tools become a 1364-line shell that auto-surfaces contract hints from files near each command; on Medium it lands within 0.9 pp of full AHE, while on Hard a built-in publish guard closes the loop too early. Middleware adds a finish-hook that forces one evaluator-isomorphic closure check; on Easy it clears every task, while on Hard it inflates turn count. The system prompt encodes 79 lines of universal discipline whose executability depends on the other three; inserted alone it scores −2.3 pp aggregate.

**Components interact non-additively, capping the aggregate gain.** The three positive single-component gains sum to +11.1 pp against full AHE's +7.3 pp, and on Hard the memory-only variant exceeds full AHE: memory, middleware, and the system prompt all push toward the same closure-style verification, so stacking them spends turns on redundant re-checks within the long-horizon budget. Since the evolve agent optimises an aggregate dominated by 55 Medium tasks, it converges to a Medium-heavy trade-off that returns part of the Hard memory effect, and we leave interaction-aware evolution to future work.

#### 4.4.2 RQ3b: how reliably the loop's self-attribution tracks reality

Each evolution round, our evolve model produces a change manifest naming which Terminal-Bench 2 tasks it expects to fix in the next round and which it flags at risk of regression. We compare the round-(N−1) prediction against the round-N ground truth, computing standard precision and recall over the 89 tasks separately for fixes and regressions.

**Evidence-driven targeting.** The fix panel of Figure 4 shows the evolve model's targeting is evidence-driven rather than guesswork. Cross-iteration fix-precision of 33.7% and fix-recall of 51.4% sit roughly 5x above the random-prediction baselines of 6.5% and 10.6%, so each harness edit lands on a real, agent-anticipated target rather than on an arbitrary subset of the panel.

Figure 4: Cross-iteration mean precision and recall of the evolve model's self-predictions across 9 evaluation rounds of the GPT-5.4 AHE loop on Terminal-Bench 2, alongside the random-prediction baseline. Left: fix predictions. Right: regression predictions.

**Regression blindness.** The regression panel tells the opposite story: cross-iteration regression-precision of 11.8% and regression-recall of 11.1% sit only about 2x above their random baselines of 5.6% and 5.4%, so most upcoming regressions go unforeseen. The agent can justify why an edit should help, but it cannot reliably name the tasks the same edit is about to break, which is what produces the non-monotone steps in the evolution curve of §4.2. Closing this gap is the clearest direction for future self-evolution loops. Appendix D gives the per-round breakdown.

## 5 Conclusion

We introduced Agentic Harness Engineering, a framework for studying harness-level test-time self-evolution in coding agents. Our central claim is that explicit harness components, including prompts, tools, middleware, skills, and configuration, can serve as a learnable adaptation surface even when the underlying model remains fixed. To make this setting operational, we presented a three-agent architecture together with an evidence-driven evolution loop that constrains self-modification through recorded change manifests, next-round attribution, and per-edit rollback.

The broader motivation of this work is methodological. If harness edits can be accumulated, inspected, and transferred across tasks, then a coding agent may externalize experience into explicit artifacts rather than relying solely on hidden parameter updates. This would make test-time learning more auditable and easier to study scientifically. Our ongoing experiments are designed to test exactly this point through task improvement, transfer, and robustness evaluations on terminal-bench-long-time.

At the same time, AHE should be understood as an initial framework rather than a finished answer. Its value depends on whether evidence-driven harness evolution produces robust gains without collapsing into benchmark-specific tuning. We therefore view the final empirical analysis, especially baselines, transfer results, and failure cases, as essential to establishing the scope of the claims made in this paper.

## Limitations

This paper studies a promising but high-variance setting, and the scope of our claims should be interpreted accordingly. First, the current evaluation centers on terminal-bench-long-time. Even if AHE improves performance on this benchmark, such gains do not by themselves establish broad generalization to other coding-agent environments, programming languages, or deployment settings.

Second, AHE increases the adaptation surface of the agent by allowing edits to multiple harness components. This flexibility is useful, but it also creates additional opportunities for benchmark-specific tuning. Our transfer and OOD experiments are designed to measure this risk directly, but negative results remain possible and should be taken seriously.

Third, the current system includes governance mechanisms such as bounded edits, attribution, and rollback, yet it does not provide a complete guardrail stack. In particular, long-horizon harness cleanup and stronger misuse prevention remain incomplete. As a result, AHE should be viewed as a controlled research prototype rather than a fully mature autonomous self-improvement system.

Finally, the method introduces additional engineering and compute overhead. Each iteration requires benchmark execution, trajectory analysis, and workspace management, which may be costly compared with one-shot prompting or manual harness edits. The final paper will report these costs explicitly.
