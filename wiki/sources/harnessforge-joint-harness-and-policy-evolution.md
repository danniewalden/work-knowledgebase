---
title: "Source: HarnessForge — Joint Harness and Policy Evolution for Adaptive Agent Systems (Chen et al.)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [harnessforge-joint-harness-and-policy-evolution]
raw_file: [raw/papers/harnessforge-joint-harness-and-policy-evolution.md]
tags: [harness-engineering, agent-harness, loop-engineering, harness-evolution, academic, focus]
---

# Source: HarnessForge — Joint Harness and Policy Evolution for Adaptive Agent Systems

**Mingju Chen, Can Lv, Guibin Zhang, Heng Chang & Shiji Zhou — arXiv:2606.01779v1, 2026-06-01. Beijing Advanced Innovation Center for Future Blockchain and Privacy Computing, School of Artificial Intelligence, Beihang University; Tsinghua University. Project lead Heng Chang; corresponding author Shiji Zhou. arXiv PREPRINT — NOT PEER-REVIEWED; arXiv is not peer review, and that caveat travels with every claim and every number below.** Raw capture: `raw/papers/harnessforge-joint-harness-and-policy-evolution.md`. CC BY 4.0.

**Metadata gap carried from the capture, because it affects citation:** the arXiv **abstract page could not be fetched** (four attempts, all returning "this PDF is empty or contains no machine-readable text"), so **the DOI line and the submission history are missing** — the KB does not know how many versions exist or their dates. The identifier, subject class (cs.CL), version (v1) and date are read off the arXiv stamp **printed inside the HTML version itself**, not off an abstract page (title and identifier were separately confirmed by web search). **There may be later versions this capture does not know about**; treat v1 as "the version we saw", not "the current version".

## Summary

The third of the batch's **four distinct methods** on one problem, and the one that refuses to hold the model fixed. Its diagnosis of the prior work is precise and worth quoting: "While existing works have adapted external harness **or** trained underlying reasoning policies, **full-system adaptation remains insufficiently characterized. The adaptation space between structure and execution is rarely made explicit, and the compatibility between the external harness and the internal reasoner is not optimized jointly.**"

HarnessForge's move is to define the unit of adaptation as a **harness–policy pair** — "a stable adaptation space that separates harness-level **execution structure** from policy-level **reasoning behavior**" — and then **co-evolve** the two through **fault-guided harness tailoring** and **harness-conditioned policy alignment**. The thesis in one line from the abstract: "**executable compatibility between the harness and reasoning policy is essential for agent-system adaptation**."

Reported: "Experiments across **five benchmarks** from diverse domains show that HarnessForge consistently improves both **Qwen3-4B and Qwen3-8B** backbones, outperforming **harness-only and policy-only baselines** with gains of **up to 12.0% over the strongest baseline** and achieving favorable rollout-efficiency tradeoffs." *(HarnessForge's own figure; arXiv preprint, not peer-reviewed; and CONTESTED — see the dispute section. Do not write this up as a settled gain.)*

## Key points

- **It is the batch's direct experimental probe of the model–harness *coupling*** that [[guo-survey-question-answering-to-task-completion-harness-design|Guo et al.]] name as the field's central question. Guo et al. ask "model, harness, or the coupling?"; HarnessForge answers by optimising the coupling explicitly and comparing against optimising either side alone. That ablation shape — **harness-only vs. policy-only vs. joint** — is the most decision-relevant experimental design in the batch, *if the numbers hold*.
- **"Meta-adaptation beyond isolated component updates"** is its own framing of why single-component harness edits plateau — the same non-additivity [[ahe-agentic-harness-engineering|AHE]] measured (positive single-component gains summing to more than the whole) and the same "coupled responsibilities" the Guo survey stresses. *(All preprints.)*
- **Fault-guided harness tailoring** = failures drive the harness edit. This is [[harness-engineering]]'s founding stance ([[mitchell-hashimoto|Hashimoto]]'s "engineer it so the agent can never make that mistake again") turned into an automated search operator, and it is the third independent implementation of failure-evidence-driven harness editing in this batch (with AHE's root-cause corpus and [[sbco-verifier-grounded-harness-optimization|SBCO]]'s graded feedback).
- **Small open-weight backbones, not frontier models.** Qwen3-4B and Qwen3-8B. That makes the result cheap to reproduce and honest about scale — but it also puts it squarely in the "gains largest where headroom is largest" regime, and it means **nothing here speaks to whether the method helps a frontier model** (the regime Wang et al. tested). *(Preprint.)*
- **It claims an explicit fairness protocol** — Appendix E is titled "Baselines and Fairness Protocol", and Appendix F "Reproducibility Artifacts". Of the batch's four methods this is the only one whose *heading list alone* shows a fairness protocol, which is the nearest thing to a pre-emptive answer to the matched-budget critique. **But that appendix was not captured**, so the wiki cannot say whether it meets Wang et al.'s bar. Flag it as the specific thing to check if this dispute ever needs resolving.
- **"Favorable rollout-efficiency tradeoffs"** is a budget claim, and budget is exactly the axis the dispute turns on — another reason the appendix matters.

## The dispute — do not cite 12.0% as an established gain

**[[wang-rethinking-evaluation-of-harness-evolution-for-agents|Wang et al. (arXiv:2607.12227v2)]] argue that automatic harness evolution is itself an iterative search and must be compared against simple task-level search / test-time-scaling baselines under **matched feedback and inference budgets**, and that searching and reporting on the same benchmark risks overfitting to it. On Terminal-Bench 2.1 with GPT-5.4 and Claude Opus 4.6 they report that harness evolution "does not consistently outperform simple test-time scaling methods and exhibits limited generalization."** *(Also an arXiv preprint, not peer-reviewed.)*

HarnessForge's "up to 12.0% over the strongest baseline" is a same-protocol claim and therefore contested. Note the partial mismatch that keeps the dispute genuinely open: HarnessForge's baselines are **harness-only and policy-only adaptation methods**, not test-time scaling, and Wang et al.'s baselines are test-time scaling, not policy training. **Neither paper has answered the other on the other's terms.** State it that way; do not resolve it.

## Limits

- **PREPRINT, NOT PEER-REVIEWED.** Applies to the harness–policy formulation and to every number.
- **METADATA GAP (above): no DOI captured, no submission history, unknown whether later versions exist.** Cite as "arXiv:2606.01779v1 (as captured 2026-09-04)".
- **The capture is the title/authors/affiliations/abstract plus the section and appendix heading list, from the HTML version.** NOT captured: the entire body (Introduction → Conclusion), all figures, tables and results, **appendices A–G** (which include the algorithm and notation, dataset details, harness-tailoring details, policy-alignment details, **the baselines and fairness protocol**, reproducibility artifacts and additional results), and the references. The full PDF was not retrieved.
- **Consequently: the five benchmarks are not named on this page, because the capture does not name them.** Nor are the baselines, the tailoring or alignment mechanisms, the compute budgets, or any per-benchmark number. "Up to 12.0%" is an abstract-level maximum with no distribution behind it in the capture — a maximum, not a typical gain.
- Two open-weight backbones in one family (Qwen3) — no evidence of cross-family or frontier-model generality.

## Connections / contrast

- **[[agent-harness]] / [[harness-engineering]]** — the paper's contribution to those pages is the **harness–policy pair** as the unit of adaptation, and the claim that harness and reasoner must be *compatible*, not merely both good.
- **[[guo-survey-question-answering-to-task-completion-harness-design]]** — the coupling question, asked by the survey and probed here; also an instance of the survey's paradigm 4 (co-evolution).
- **[[ahe-agentic-harness-engineering]]** — the deliberate contrast: AHE **freezes the base model** so the gain is attributable to harness edits; HarnessForge argues that freezing it is precisely what leaves compatibility unoptimised. **These are opposed methodological commitments on the same problem, and the KB should present them as a live design choice rather than a progression.** *(Both preprints.)*
- **[[harnessx-composable-adaptive-evolvable-agent-harness-foundry]]** — closest in ambition (HarnessX also feeds trajectories back as model training signal); different formalisation (algebra of typed primitives vs. structure/behaviour split).
- **[[sbco-verifier-grounded-harness-optimization]]** — the cheap end of the same family; SBCO fixes the meta-agent and learns verifiers instead of co-training a policy.
- **[[wang-rethinking-evaluation-of-harness-evolution-for-agents]]** — see the dispute section.
- **[[loop-engineering]]** — a hill-climbing loop whose search space includes the model's weights, which stretches that page's current framing (the loop rewrites *config*) toward RL.
- **[[feedforward-and-feedback-controls]]** — "fault-guided" tailoring is a feedback control that edits the guides.

_Source page: [[harnessforge-joint-harness-and-policy-evolution]]._
