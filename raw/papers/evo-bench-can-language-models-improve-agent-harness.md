---
source_url: https://arxiv.org/abs/2608.09096
title: "Evo-Bench: Can Language Models Improve Agent Harness?"
author: Lisheng Huang, Chen Yang, Hao Zhou, Huatong Song, Zongchao Chen, Ran Le, Yang Song, Wayne Xin Zhao, Tao Zhang
publication: arXiv (cs.CL), arXiv:2608.09096
published: 2026-08-10
retrieved: 2026-08-17
type: paper
---

# Evo-Bench: Can Language Models Improve Agent Harness?

Computer Science > Computation and Language

[Submitted on 10 Aug 2026 (v1), last revised 11 Aug 2026 (this version, v2)]

Lisheng Huang, Chen Yang, Hao Zhou, Huatong Song, Zongchao Chen, Ran Le, Yang Song, Wayne Xin Zhao, Tao Zhang

## Abstract

Large Language Models (LLMs) have driven rapid progress in autonomous agents, yet standard evaluations remain confined to static task solving. An emerging frontier is harness evolution---the agent's capacity to autonomously optimize its own operating harness. However, systematically benchmarking this capability remains challenging, as existing evaluations fail to isolate harness improvements from base model strength, prevent task-specific overfitting, or capture long-horizon iterative research. To address these challenges, we introduce Evo-Bench, the first benchmark designed to evaluate models' intrinsic harness-evolving capabilities across Search, Office, and General agent domains. To rigorously isolate this capability, Evo-Bench employs a novel harness-guided construction framework: it leverages auxiliary-task evolution to identify tasks genuinely sensitive to framework improvements, followed by sensitivity-aware stratified splitting to ensure robust cross-suite generalization. Extensive evaluations across nine frontier and open-weight models reveal that top models achieve massive absolute gains reaching 16.6 points, closely approaching state-of-the-art human-engineered baselines. Crucially, while autonomous evolution outpeforms artificial harness in General tasks and excels in Search tasks, it struggles in Office tasks that demand highly specific processing workflows. Furthermore, our analysis exposes critical temporal anomalies like early saturation, while demonstrating that the synthesized harnesses act as highly transferable reasoning structures, consistently boosting diverse policy models.

Subjects: Computation and Language (cs.CL)

Cite as: arXiv:2608.09096 [cs.CL] (or arXiv:2608.09096v2 [cs.CL] for this version)

https://doi.org/10.48550/arXiv.2608.09096

## Submission history

From: Lisheng Huang
- [v1] Mon, 10 Aug 2026 03:49:28 UTC (2,374 KB)
- [v2] Tue, 11 Aug 2026 02:53:55 UTC (2,374 KB)

---

*Capture note (not part of the source): abstract page captured verbatim; the full PDF was not retrieved. Typo "outpeforms" is the authors'. Surfaced via an X keyword sweep on "agent harness" (2026-08-17) and confirmed against the arXiv API listing.*
