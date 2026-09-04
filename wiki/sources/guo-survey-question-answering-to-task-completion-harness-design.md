---
title: "Source: From Question Answering to Task Completion — A Survey on Agent System and Harness Design (Guo et al.)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [guo-survey-question-answering-to-task-completion-harness-design]
raw_file: [raw/papers/guo-survey-question-answering-to-task-completion-harness-design.md]
tags: [harness-engineering, agent-harness, survey, academic, model-harness-coupling, focus]
---

# Source: From Question Answering to Task Completion — A Survey on Agent System and Harness Design

**Guo, Hao, Wang, Fan, Luo, Li, Gao, Mei, Peng, Xu, Dong, Wu, Zheng, Han, Wang, Xu & Wang — arXiv:2606.20683, submitted 2026-06-14. 17 authors across City University of Hong Kong, University of Sydney, Peking University and TokenRhythm Technologies. arXiv PREPRINT — NOT PEER-REVIEWED; arXiv is not peer review, and that caveat travels with every claim below.** Raw capture: `raw/papers/guo-survey-question-answering-to-task-completion-harness-design.md`. Paper collection at github.com/ggjy/Awesome-Agent-Engineering. CC BY 4.0.

**Title note carried from the capture:** the paper is sometimes referenced as "From Question Answering to Task Completion: Agent System and Harness Design". The title arXiv actually carries includes **"A Survey on"** — cite it in full.

## Summary

The **later of two independent surveys published 27 days apart** (with [[ning-code-as-agent-harness|Ning et al., arXiv:2605.18747]], submitted 2026-05-18 - i.e. *before* this one, which is 2026-06-14) written specifically to organise the [[harness-engineering]] literature — and the strongest single piece of evidence that harness optimisation is a research **field** rather than a handful of candidate papers. Its organising question is the one this KB has been circling: *"where does the bottleneck in agent performance reside, in the foundation model, in the execution harness, or in the coupling between them?"* The survey's answer is the coupling. It reads LLM-based agents "through a model-harness lens", defines an agent implementation-wise as **a foundation model coupled with an execution harness**, and argues that agent quality — "success, efficiency, safety, and generalization" — "emerges from the interaction between model capability, runtime infrastructure, task structure, and evaluation design", explicitly "rather than treating agents as models with auxiliary tools".

Two of its structures are ready-made spines for this wiki: a **four-paradigm ladder** of agent engineering and a **six-responsibility decomposition** of the [[agent-harness]] runtime.

## Key points

- **The four paradigms of agent engineering** (§4), verbatim from the capture's excerpts — a ladder, each rung changing the unit of optimisation:
  1. **Prompt Engineering** — "optimizes the single-turn instruction sent to the model. Prompting fundamentally addresses an expression problem."
  2. **Workflows and [[context-engineering|Context Engineering]]** — "shifts the unit of optimization from a single prompt to the information lifecycle surrounding multi-step execution. Context engineering remains fundamentally **feedforward**."
  3. **[[harness-engineering|Harness Engineering]]** — "**closes the loop.** Beyond assembling the right context, the harness introduces feedback-driven execution: the model acts, observes environment responses, and reasons over observations to decide its next step."
  4. **Agent-Native Training and Co-Evolution** — "builds on the learnable multi-model harness view. Its first direction is **internalization**; agentic behaviors are increasingly trained into model parameters. Its second direction is **co-evolution**."
  This is an academic restatement of the KB's [[feedforward-and-feedback-controls]] distinction: paradigm 2 is *guides*, paradigm 3 is *guides plus sensors*. And paradigm 4 is the academic form of the absorption thesis that [[mcateer-evolution-of-the-agent-harness|McAteer]] argues from the practitioner side.
- **The six coupled runtime responsibilities of the execution harness** (§5, "Anatomy of the Execution Harness"), verbatim:
  - **Observation interface** — "transforms raw environment signals into model-usable observations"
  - **Context manager** — "determines what information enters the model context, when and in form"
  - **Control loop** — "orchestrates the observe-reason-act-feedback cycle"
  - **Action interface** — "maps model outputs to executable operations"
  - **State and artifact store** — "persists execution state and products"
  - **Verification and governance layer** — "checks, constrains, and repairs execution"
  The word the survey keeps using is **coupled**: it devotes a subsection to "Cross-Layer Interactions in the Harness", which is the same non-additivity that [[ahe-agentic-harness-engineering|AHE]] measured empirically (single-component gains summing to more than the whole).
- **A responsibility decomposition, not a component list.** This is orthogonal to AHE's seven *editable files* (system prompt, tool description, tool implementation, middleware, skill, sub-agent config, long-term memory) — Guo et al. name **what the harness must do**, AHE names **what you can edit**. They are complements, and holding both is more useful than choosing.
- **Model-centric scaling has limits, and the survey names two** (§3): a **resource-performance boundary** and a **measurement boundary**. The second matters for this KB's [[agent-observability-and-evals]] thread — the claim is that we are partly bottlenecked on our ability to *measure*, not only on capability.
- **Harness configuration is task-dependent** (§6): a "harness-aware task taxonomy", harness adaptation by domain, and an explicit mapping "from task properties to harness configurations". The survey does not claim one best harness — a direct academic echo of [[birgitta-bockeler|Böckeler]]'s "not every codebase is equally harnessable".
- **It treats evaluation as part of the object of study** (§7 analyses harness effects on SWE-bench Verified, Terminal-Bench 2.0 and WebArena separately) and lists **open challenges in "value-aware evaluation, safety, harness generalization, and model-harness co-evolution"** (§8, incl. "Harness Generalization Versus Specialization"). Filed here without numbers — see Limits.

## Limits

- **PREPRINT, NOT PEER-REVIEWED.** arXiv is not peer review. Every structure and claim on this page carries that caveat, including the two decompositions, which are the survey's *proposals* and not established taxonomy.
- **It is a survey, so it is secondary evidence.** It organises other groups' results; it produces none of its own. Its authority is as a map of a corpus, not as a measurement.
- **The capture is an extended abstract plus an outline, not the survey.** Captured verbatim: title, authors, abstract, the affiliation block, the complete heading list, the six-responsibility definition list, and the four-paradigm excerpts. **NOT captured:** the body prose of all nine sections, all figures and tables, the harness-aware task taxonomy tables, and — critically — **the per-benchmark empirical analyses** (SWE-bench Verified, Terminal-Bench 2.0, WebArena). The full PDF was not retrieved. **Therefore: no number, score or benchmark delta may be cited to this page.** If the wiki ever needs Guo et al.'s empirical read of harness effects, that requires a new capture of the body.
- One author group includes an industrial lab (TokenRhythm Technologies); the survey is not a product pitch, but it is not a wholly academic author list either.

## Connections / contrast

- **[[agent-harness]] / [[harness-engineering]]** — this is the best available *spine* for both pages: the four-paradigm ladder gives [[harness-engineering]] a placement story that currently rests on practitioner chronology, and the six responsibilities give [[agent-harness]] a functional decomposition to sit beside its primitive list.
- **[[ning-code-as-agent-harness]]** — the sibling survey, **27 days earlier** (2026-05-18 vs. 2026-06-14), 42 authors, no author overlap. Same object, different cut (Ning et al. centre *code* as the substrate; Guo et al. centre the *model-harness coupling*). Two surveys with disjoint author sets is the field evidence.
- **[[graph-engineering-era-of-llm-agents-system-intelligence]]** — **a taxonomy conflict worth keeping open.** Feng et al. name the same ladder but with a different fourth rung: prompt → context → harness → **[[loop-engineering|loop engineering]]**, then graph engineering as a fifth. Guo et al.'s fourth rung is **agent-native training and co-evolution** and has no graph or loop rung at all. Both are preprints; neither is settled. The wiki should record both ladders as *competing proposals*, not merge them.
- **[[ahe-agentic-harness-engineering]]** — the method paper Guo et al.'s paradigm 3 describes. AHE's seven components vs. Guo's six responsibilities is a complement, not a contradiction (see Key points).
- **[[wang-rethinking-evaluation-of-harness-evolution-for-agents]]** — Guo et al. flag "value-aware evaluation" and "harness generalization" as *open challenges*; Wang et al. turn the same worries into a negative result against the evaluation protocol harness-evolution papers actually use. Read them together: the survey says the evaluation question is open, the critique says the current answers do not hold up.
- **[[mcateer-evolution-of-the-agent-harness]]** — paradigm 4 ("internalization; agentic behaviors are increasingly trained into model parameters") is the academic statement of McAteer's train → absorb → shed loop.
- **[[context-engineering]]** — the survey's "context engineering remains fundamentally feedforward" is the crispest one-line placement of that page relative to this one that the KB holds.
- **[[agent-engineering]]** — the survey's own GitHub collection is literally named *Awesome-Agent-Engineering*, which is a small datum that the KB's chosen umbrella term matches the literature's.

_Source page: [[guo-survey-question-answering-to-task-completion-harness-design]]._
