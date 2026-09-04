---
title: "Source: SBCO — Self-Supervised, Verifier-Grounded Harness Optimization for Planning Agents (Kulkarni et al.)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [sbco-verifier-grounded-harness-optimization]
raw_file: [raw/papers/sbco-verifier-grounded-harness-optimization.md]
tags: [harness-engineering, agent-harness, loop-engineering, harness-evolution, verification, academic, focus]
---

# Source: SBCO — Self-Supervised, Verifier-Grounded Harness Optimization for Planning Agents

**Vivek Kulkarni, Sudipta Paul, Aounon Kumar, Nicholas Tzou & Srinivas Chappidi — arXiv:2608.10157v1, 2026-08-10. arXiv PREPRINT — NOT PEER-REVIEWED; arXiv is not peer review, and that caveat travels with every claim and every number below.** Raw capture: `raw/papers/sbco-verifier-grounded-harness-optimization.md` (abstract page captured verbatim; surfaced via an X keyword sweep on "agent harness", 2026-08-17, and confirmed against the arXiv API listing).

## Summary

The fourth of the batch's **four distinct methods** on the harness-optimisation problem, and the one that attacks *cost* and *domain reach* rather than power. Its starting observation is a real limitation of the Gödel-machine lineage (**Darwin Gödel Machine**, **Huxley Gödel Machine**), where "a coding agent edits its own code": such **self-referential** self-improvement "require[s] that the competence required to perform the task coincides or aligns well with the competence required for self-modification **which is the case for coding tasks**." Outside coding, that alignment fails. The workarounds — drop the self-reference, or add an explicitly self-modifying meta-agent — are "both computationally expensive, relying on **population or self-modification search over many candidate agents**."

SBCO (**Self-supervised Block Coordinate Optimizer**) is offered as "a far cheaper alternative" for "planning tasks with explicit constraints": "a **verifier-grounded harness optimizer** in the same closed-loop, improve-from-experience family as the Gödel-machine methods, but **self-supervised rather than self-referential**." Given an agentic harness, it "learns a **decomposed bank of verifiers** and a **harness policy** via **approximate block coordinate ascent**, improving the agent's outputs from its own graded feedback — with a **fixed meta-agent and no human labels**."

Reported: "Across **two domains** SBCO **matches or exceeds** a customized self-modifying baseline while using **4–5.5 times less compute budget**." *(SBCO's own figure; arXiv preprint, not peer-reviewed. Note this is an efficiency claim on top of parity — see Key points and the dispute note.)*

## Key points

- **The self-referential/self-supervised distinction is the durable contribution, independent of any number.** Self-referential self-improvement only works where *doing the task* and *modifying the system* need the same competence — true for coding agents, false for planning, scheduling, support triage, or domain modelling. That is a **precise limit on how far the "agent improves itself" story generalises**, and the KB does not currently hold it anywhere. It is also a caution for [[loop-engineering]]'s hill-climbing loop, whose entire evidence base is coding agents.
- **Verifiers are learned, decomposed, and are the optimisation target.** "A decomposed bank of verifiers **and** a harness policy" — the harness's [[feedforward-and-feedback-controls|sensors]] are not hand-written and fixed; they are *learned artifacts co-optimised with the policy*. This extends the KB's sensor story: [[fowler-bockeler-maintainability-sensors|Böckeler]] hand-builds computational sensors; SBCO learns a bank of them. For [[agent-observability-and-evals]], it is graders-as-a-learned-component.
- **"Self-supervised … from its own graded feedback … with a fixed meta-agent and no human labels"** — the harness improves from self-grading, with the *editor* held constant. That is the opposite governance choice from [[harnessforge-joint-harness-and-policy-evolution|HarnessForge]] (which co-evolves the policy) and a stricter one than [[ahe-agentic-harness-engineering|AHE]] (whose evolve agent is fixed but whose action space is the whole harness). **Self-grading with no human labels is also the exact place a grader leak would hide** — the paper's framing does not tell us how that is controlled, and the capture cannot say.
- **The headline result is parity plus efficiency, not superiority.** "Matches or exceeds … while using 4–5.5 times less compute budget." Read plainly: the contribution is **the same quality for a fifth of the compute**, against *one customized self-modifying baseline* in *two domains*. That is a narrower and more modest claim than the batch's other method papers make, and correspondingly harder to dismiss.
- **Efficiency claims are the one axis the batch's methodological critique does *not* undercut.** [[wang-rethinking-evaluation-of-harness-evolution-for-agents|Wang et al.]]'s objection is that harness-evolution gains may be bought with extra search under an unmatched budget. SBCO's claim is *explicitly budget-relative* (4–5.5× less compute for equal or better output), which is the form of claim Wang et al. ask for. **It is not thereby exempt** — the baseline is a self-modifying agent, not the simple test-time-scaling baseline Wang et al. propose, and the domains are planning tasks rather than Terminal-Bench — but it is the batch's closest structural match to the fairness standard the critique demands, and worth flagging as such wherever the dispute is discussed.
- **Planning agents, not coding agents** — the batch's only method paper aimed away from [[agentic-coding]], which is why it can see the self-reference limit at all.

## Limits

- **PREPRINT, NOT PEER-REVIEWED.** Applies to the method and to the 4–5.5× figure.
- **The capture is the abstract page only.** NOT captured: **author affiliations** (not shown; so **this paper is attributed to no institution on this wiki** — note the author names alone are not evidence of an employer), the paper body, the block-coordinate-ascent algorithm, the verifier bank's construction, all figures, tables and per-domain results, and the references. The full PDF was not retrieved.
- **"Two domains" are not named in the capture, and neither is the "customized self-modifying baseline".** So the wiki cannot say what SBCO was tested on, against what, or how "matches or exceeds" splits between *matches* and *exceeds*. **Both the parity claim and the 4–5.5× compute figure are abstract-level self-reports with no visible breakdown, no variance and no seeds.**
- Two domains and one baseline is a narrow evidence base; the claim is best read as a feasibility-and-cost demonstration, not a general result about planning agents.
- Surfaced via a social-media keyword sweep. Provenance of *discovery* was confirmed against the arXiv API, but no independent commentary, replication or citation of this paper is held in the KB.

## Connections / contrast

- **[[harness-engineering]] / [[agent-harness]]** — the cheap, verifier-grounded end of automatic harness improvement, and the source for the **self-referential vs. self-supervised** distinction those pages should carry.
- **[[loop-engineering]]** — a fourth-loop (hill-climbing) instance that **bounds the pattern's generality**: the loop's coding-agent evidence base does not transfer to domains where doing the task and editing the system need different competences.
- **[[ahe-agentic-harness-engineering]]** — same "improve from experience" family; AHE spends 10 iterations and ~32 hours of rollouts, SBCO's whole pitch is that this class of search is expensive. *(Both preprints.)*
- **[[harnessforge-joint-harness-and-policy-evolution]] · [[harnessx-composable-adaptive-evolvable-agent-harness-foundry]]** — the other two methods; SBCO is the deliberate minimalist among them (fixed meta-agent, no human labels, no model training).
- **[[wang-rethinking-evaluation-of-harness-evolution-for-agents]]** — see Key points: SBCO's budget-relative framing is the batch's nearest thing to the protocol Wang et al. demand, without being an answer to it.
- **[[evo-bench-can-language-models-improve-agent-harness]]** — filed the same day (both 2026-08-10) and the natural pairing: Evo-Bench asks *can models improve harnesses, measured how?*; SBCO asks *can we improve harnesses cheaply, outside coding?*
- **[[feedforward-and-feedback-controls]] · [[fowler-bockeler-maintainability-sensors]]** — sensors as *learned* rather than authored artifacts.
- **[[agent-observability-and-evals]]** — a learned verifier bank is an eval suite that optimises itself, which sharpens that page's grader-independence question.
- **[[guardian-agents]]** — a bank of decomposed verifiers is a structural cousin of the guardian pattern, reached from optimisation rather than governance.

_Source page: [[sbco-verifier-grounded-harness-optimization]]._
