---
source_url: https://arxiv.org/abs/2606.20683
title: "From Question Answering to Task Completion: A Survey on Agent System and Harness Design"
author: Jianyuan Guo, Zhiwei Hao, Chengcheng Wang, Cheng Fan, Tingzhang Luo, Hongguang Li, Ying Gao, Hefei Mei, Jiankun Peng, Rongjian Xu, Minjing Dong, Han Wu, Mengyu Zheng, Kai Han, Shiqi Wang, Chang Xu, Yunhe Wang
publication: arXiv (cs.AI; cs.CL), arXiv:2606.20683
published: 2026-06-14
retrieved: 2026-09-04
type: paper
capture_note: >
  PREPRINT — NOT PEER-REVIEWED. arXiv preprint; arXiv is not peer review, and this
  caveat travels with any claim drawn from it.

  TITLE NOTE: this paper is sometimes referenced as "From Question Answering to
  Task Completion: Agent System and Harness Design". The title arXiv actually
  carries is "From Question Answering to Task Completion: A Survey on Agent
  System and Harness Design" — the words "A Survey on" are part of it.

  PARTIAL VERBATIM CAPTURE. Captured verbatim from the arXiv abstract page
  (arxiv.org/abs/2606.20683): title, author list, abstract in full, subject
  classes, cite-as line, DOI and submission history. Additionally captured from
  the HTML version (arxiv.org/html/2606.20683v1): the affiliation footnote block,
  the complete section/subsection heading list, the six-item definition list of
  harness runtime responsibilities (§5 / "Anatomy of the Execution Harness"), and
  short verbatim excerpts describing the four paradigms of agent engineering
  (§4). NOT captured: the body prose of all nine sections, all figures and
  tables, the harness-aware task taxonomy tables, the per-benchmark empirical
  analyses (SWE-bench Verified, Terminal-Bench 2.0, WebArena), and the
  references. This is an extended-abstract-plus-outline capture of a long survey,
  not the survey. The full PDF was not retrieved.
---

# From Question Answering to Task Completion: A Survey on Agent System and Harness Design

Computer Science > Artificial Intelligence

[Submitted on 14 Jun 2026]

Jianyuan Guo, Zhiwei Hao, Chengcheng Wang, Cheng Fan, Tingzhang Luo, Hongguang Li, Ying Gao, Hefei Mei, Jiankun Peng, Rongjian Xu, Minjing Dong, Han Wu, Mengyu Zheng, Kai Han, Shiqi Wang, Chang Xu and Yunhe Wang

## Affiliations

- J. Guo, Z. Hao, C. Fan, T. Luo, H. Li, Y. Gao, H. Mei, J. Peng, R. Xu, M. Dong and S. Wang are with the Department of Computer Science, City University of Hong Kong, HKSAR, China.
- C. Wang and C. Xu are with the School of Computer Science, University of Sydney.
- H. Wu is with Peking University.
- M. Zheng, K. Han and Y. Wang are with TokenRhythm Technologies.

## Abstract

LLM-based agents mark a shift from passive question answering to active task completion: they perceive environments, invoke tools, maintain state, and act over extended horizons. As agent systems have evolved from prompt engineering to workflows and context engineering, harness engineering, and agent-native training with co-evolution, a central question has become increasingly important: where does the bottleneck in agent performance reside, in the foundation model, in the execution harness, or in the coupling between them? This survey examines LLM-based agents through a model-harness lens. We first clarify the functional definition of agents and the implementation view of an LLM-based agent as a foundation model coupled with an execution harness. We then analyze the limits of model-centric scaling, trace four paradigms of agent engineering, and decompose the execution harness into six coupled runtime responsibilities: observation, context, control, action, state, and verification. Using this decomposition, we map task properties and domain pressures to harness configurations, review benchmark and evaluation practices, and synthesize model-harness evidence on how runtime design affects long-horizon task completion, efficiency, and reliability. Finally, we identify open challenges in value-aware evaluation, safety, harness generalization, and model-harness co-evolution. Rather than treating agents as models with auxiliary tools, this survey argues that agent quality -- including success, efficiency, safety, and generalization -- emerges from the interaction between model capability, runtime infrastructure, task structure, and evaluation design. A collection of papers discussed in this survey is provided in https://github.com/ggjy/Awesome-Agent-Engineering.

Subjects: Artificial Intelligence (cs.AI); Computation and Language (cs.CL)

Cite as: arXiv:2606.20683 [cs.AI]

https://doi.org/10.48550/arXiv.2606.20683

License: CC BY 4.0

## Submission history

From: Jianyuan Guo
- [v1] Sun, 14 Jun 2026 05:40:16 UTC (625 KB)

---

## Section structure (headings verbatim, from the HTML version)

1. Introduction
   - Harness Design as a Performance Lever
   - Four Paradigms of Agent Engineering
   - Relation to Prior Surveys
   - Scope Boundaries
   - Contributions and Survey Structure
2. Background and Definitions
   - Functional View: What Is an Agent?
   - Implementation View: Model Plus Harness
   - LLM as the Cognitive Engine
   - Harness as the Runtime Substrate
   - Key Infrastructure Primitives
3. The Limits of Model-Centric Scaling
   - Resource-Performance Boundary
   - Measurement Boundary
4. Paradigm Shifts in Agent Engineering
   - Phase 1: Prompt Engineering
   - Phase 2: Workflows and Context Engineering
   - Phase 3: Harness Engineering
   - Phase 4: Agent-Native Training and Co-Evolution
5. Anatomy of the Execution Harness
   - Observation Interface
   - Context Manager
   - Control Loop
   - Action Interface
   - State and Artifact Store
   - Verification and Governance
   - Cross-Layer Interactions in the Harness
6. Task Landscape and Harness Configuration
   - A Harness-Aware Task Taxonomy
   - Harness Adaptation by Domain
   - From Task Properties to Harness Configurations
7. Evaluation and Empirical Analysis
   - Benchmark Landscape and Evaluation Work
   - Evaluation Dimensions Beyond Task Success
   - Harness Effects on SWE-bench Verified
   - Harness Effects on Terminal-Bench 2.0
   - Harness Effects on WebArena
   - Benchmark Insights
8. Outlook and Future Directions
   - From Score to Value-Aware Agent Optimization
   - Learning to Verify, Recover, and Adapt
   - Harness Generalization Versus Specialization
9. Conclusion

## The six harness runtime responsibilities (verbatim excerpt)

> The six components are:
>
> - Observation interface: transforms raw environment signals into model-usable observations
> - Context manager: determines what information enters the model context, when and in form
> - Control loop: orchestrates the observe-reason-act-feedback cycle
> - Action interface: maps model outputs to executable operations
> - State and artifact store: persists execution state and products
> - Verification and governance layer: checks, constrains, and repairs execution

## The four paradigms of agent engineering (verbatim excerpts)

> Prompt Engineering optimizes the single-turn instruction sent to the model. Prompting fundamentally addresses an expression problem.

> Workflows and Context Engineering shifts the unit of optimization from a single prompt to the information lifecycle surrounding multi-step execution. Context engineering remains fundamentally feedforward.

> Harness Engineering closes the loop. Beyond assembling the right context, the harness introduces feedback-driven execution: the model acts, observes environment responses, and reasons over observations to decide its next step.

> Agent-Native Training and Co-Evolution builds on the learnable multi-model harness view. Its first direction is internalization; agentic behaviors are increasingly trained into model parameters. Its second direction is co-evolution.
