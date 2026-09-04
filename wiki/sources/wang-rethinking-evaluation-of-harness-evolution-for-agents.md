---
title: "Source: Rethinking the Evaluation of Harness Evolution for Agents (Wang et al.) — negative result"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [wang-rethinking-evaluation-of-harness-evolution-for-agents]
raw_file: [raw/papers/wang-rethinking-evaluation-of-harness-evolution-for-agents.md]
tags: [harness-engineering, agent-harness, agent-observability-and-evals, negative-result, academic, focus]
---

# Source: Rethinking the Evaluation of Harness Evolution for Agents (Wang et al.)

**Wang, Zhu, Hu, Yuan, Chen, Senthil, Hajishirzi, Tsvetkov, Dasigi & Xiao — arXiv:2607.12227, v1 2026-07-14, v2 (current) 2026-08-27. arXiv PREPRINT — NOT PEER-REVIEWED.** Raw capture: `raw/papers/wang-rethinking-evaluation-of-harness-evolution-for-agents.md`. Code at github.com/rethinking-harness-evolution. CC BY 4.0.

**This is a NEGATIVE RESULT, and the caveat cuts both ways.** It is an un-reviewed preprint arguing that other un-reviewed preprints' evaluation protocol is unsound. Its critique does not inherit extra authority from being a critique — but the KB must not resolve the dispute by preferring the positive results either. **Both sides are preprints. The dispute is live.**

## Summary

The paper the rest of this batch has to be read against. It revisits **automatic harness evolution** for LLM agents and attacks the *protocol*, not any single system: existing methods "use unit test cases to search for harness configurations and then report final performance on the same public benchmark." Wang et al. raise two objections and then run the experiment the objections imply.

**Objection 1 — the comparison is against the wrong baseline.** "Harness evolution is itself an iterative search procedure that repeatedly evaluates and revises candidate harnesses using task feedback. As in agentic test-time scaling, it should therefore be compared with simple **task-level search baselines under matched feedback and inference budgets** to determine whether its gains arise from **improved harness design or from additional search alone**." In other words: spend the same compute on plain test-time scaling and see if you get the same lift.

**Objection 2 — the search and the scoreboard are the same benchmark.** "Because the search and the final evaluation share the same benchmark, the reported gains risk **overfitting to that specific task set**." So: hold out tasks and re-check.

**The result, verbatim:** "Experiments on **Terminal-Bench 2.1** with **GPT-5.4** and **Claude Opus 4.6** show that automatic harness evolution **does not consistently outperform simple test-time scaling methods and exhibits limited generalization**." *(Preprint, not peer-reviewed.)* They conclude by calling for "fairer evaluation protocols and benchmarks for automatic harness design."

## Key points

- **The target is the protocol shared by the whole harness-evolution cluster** — search against task feedback, report on the public benchmark you searched against. That protocol is used by [[ahe-agentic-harness-engineering|AHE]] (Terminal-Bench 2), [[harnessx-composable-adaptive-evolvable-agent-harness-foundry|HarnessX]] and [[harnessforge-joint-harness-and-policy-evolution|HarnessForge]]. **Every gain those papers report is inside the scope of this critique.** *(All four are preprints, none peer-reviewed.)*
- **The alternative explanation is search, not design.** If a matched-budget baseline that does no harness engineering at all reaches the same score, then "the harness got better" is not the demonstrated conclusion — "we spent more inference" is. This is the single most important epistemic move in the batch.
- **Generalisation is the second, independent failure.** Even setting the baseline question aside, evolved harnesses evaluated on **held-out tasks** show "limited generalization" *(preprint, not peer-reviewed)*. That directly undercuts the transfer story harness-evolution papers lean on, including the "harnesses are transferable reasoning structures" claim in [[evo-bench-can-language-models-improve-agent-harness|Evo-Bench]] and the frozen-harness transfer result in [[ahe-agentic-harness-engineering|AHE]] — though note neither of those specific results was itself re-run here, as far as this capture can establish.
- **"Does not consistently outperform" is not "does not work."** Read precisely: the claim is inconsistency and weak generalisation under fair budgets, not that harness evolution never helps. The honest wiki formulation is *contested*, not *refuted*.
- **It is measured on newer/better ground than the papers it critiques:** Terminal-Bench **2.1** with **GPT-5.4** and **Claude Opus 4.6**, i.e. frontier bases where any harness lift has less headroom. That is a fair criticism of the critique too — a method that helps a weak base (AHE's largest gains were on its *weakest* bases) may legitimately fail to help a strong one without the method being worthless. This tension is unresolved and should be stated as such wherever the dispute is cited.
- **v2 (2026-08-27) is a substantive revision window, not a typo pass** — v1 was 2026-07-14. The capture cannot say what changed, only that the current version is v2.
- **Code is public** (github.com/rethinking-harness-evolution), which makes this a falsifiable critique rather than a position piece — the one respect in which it is stronger than most of the batch.

## Limits

- **PREPRINT, NOT PEER-REVIEWED, and self-referentially so:** a non-reviewed paper judging non-reviewed papers' methodology. State this every time the critique is used to discount someone else's number.
- **The capture is the abstract page only** (v2): title, authors, abstract, subject class, cite-as, DOI, submission history. **NOT captured:** author affiliations (not shown on the abstract page — so **do not attribute this paper to any institution**, even where author names suggest one), the paper body, the experimental setup, all figures and tables, and every per-baseline result. The HTML fetch was rate-limited; the PDF was not retrieved.
- **Consequently the wiki cannot state which specific systems were re-evaluated, which test-time-scaling baselines were used, what the numeric deltas were, or how the held-out split was built.** The scope of the critique as filed here is what the abstract asserts. Anyone relying on this dispute for a decision needs the body.
- Single benchmark family (Terminal-Bench 2.1) and two frontier models — the same narrowness the paper criticises in others applies to its own evidence base as captured.

## Connections / contrast

- **[[harnessx-composable-adaptive-evolvable-agent-harness-foundry]]** — HarnessX's **average +14.5% (up to +44.0%)** across five benchmarks *(HarnessX's own figure, preprint, not peer-reviewed)* is exactly the kind of result this paper says has not been shown to beat a matched-budget baseline. **The KB must not carry that number as a settled gain.**
- **[[harnessforge-joint-harness-and-policy-evolution]]** — same: **up to 12.0% over the strongest baseline** *(HarnessForge's own figure, preprint, not peer-reviewed)* is contested by this paper. HarnessForge's abstract does claim a "fairness protocol" appendix (Appendix E) and "favorable rollout-efficiency tradeoffs", which is the nearest thing in the batch to a pre-emptive answer — but that appendix was not captured, so the KB cannot say whether it meets Wang et al.'s matched-budget bar.
- **[[ahe-agentic-harness-engineering]]** — **the standing KB claim this contradicts.** [[harness-engineering]] and [[loop-engineering]] both currently present AHE's Terminal-Bench 2 pass@1 **69.7% → 77.0%** as an established gain (correctly marked *preprint*, but with no dispute attached). AHE searched with task feedback and reported on the benchmark it searched against — the protocol under attack. Those pages need the dispute added; see the deltas file.
- **[[evo-bench-can-language-models-improve-agent-harness]]** — the interesting case, because Evo-Bench was *built* against one of the **two** concerns raised here - task-specific overfitting, via sensitivity-aware stratified splitting - and separately against base-model-strength confounding, which is Evo-Bench's own third framing and not one of the two concerns this paper raises. It does **not** obviously address the matched-inference-budget objection. So the batch contains a benchmark designed against overfitting and a critique saying overfitting persists — both preprints, unreconciled.
- **[[ning-code-as-agent-harness]]** — the 42-author survey independently lists "**harness-level evaluation and oracle adequacy**" and "**self-evolving harnesses without regression**" among its open problems. The critique is not an outlier: the field's own maps say this is unsettled.
- **[[guo-survey-question-answering-to-task-completion-harness-design]]** — names "value-aware evaluation" and "harness generalization versus specialization" as open challenges. Same agreement.
- **[[agent-observability-and-evals]]** — this is a benchmark-hygiene argument in the agent era: search-on-the-test-set, and budget-matched baselines as the control condition. It belongs on that page as a general lesson, independent of harnesses.
- **[[loop-engineering]]** — the hill-climbing loop's standing open question on that page is whether a self-improving loop "optimizes for the grader rather than the goal." Wang et al. are the strongest evidence yet that the answer is *partly yes, and the field's protocol cannot currently tell*.
- **[[fitness-functions]] · [[mutation-testing]]** — the same species of problem the testing tradition already knows: an oracle you optimise against stops measuring the thing.

_Source page: [[wang-rethinking-evaluation-of-harness-evolution-for-agents]]._
