---
source_url: https://arxiv.org/abs/2606.14249
title: "HarnessX: A Composable, Adaptive, and Evolvable Agent Harness Foundry"
author: Tingyang Chen, Shuo Lu, Kang Zhao, Weicheng Meng, Hanlin Teng, Tianhao Li, Chao Li, Xule Liu, Jian Liang, Zhizhong Zhang, Yuan Xie, Heng Qu, Kun Shao, Jian Luan
publication: arXiv (cs.AI), arXiv:2606.14249
published: 2026-06-12
retrieved: 2026-09-04
type: paper
capture_note: >
  PREPRINT — NOT PEER-REVIEWED. arXiv preprint; arXiv is not peer review, and this
  caveat travels with any claim drawn from it.

  PARTIAL VERBATIM CAPTURE. Captured verbatim from the arXiv abstract page
  (arxiv.org/abs/2606.14249): title, author list, abstract in full, subject class,
  cite-as line, DOI and submission history (three versions). NOT captured: author
  affiliations (not shown on the abstract page and the HTML version was not
  retrieved), the paper body, the substitution algebra and AEGIS method sections,
  all figures, tables and per-benchmark results, and the references. The full PDF
  was not retrieved. Same scope as the existing evo-bench and sbco captures:
  abstract page only.
---

# HarnessX: A Composable, Adaptive, and Evolvable Agent Harness Foundry

Computer Science > Artificial Intelligence

[Submitted on 12 Jun 2026 (v1), last revised 23 Jul 2026 (this version, v3)]

Tingyang Chen, Shuo Lu, Kang Zhao, Weicheng Meng, Hanlin Teng, Tianhao Li, Chao Li, Xule Liu, Jian Liang, Zhizhong Zhang, Yuan Xie, Heng Qu, Kun Shao, Jian Luan

## Abstract

AI agent performance depends critically on the runtime harness, comprising the prompts, tools, memory, and control flow that mediate how a model observes, reasons, and acts. Yet today's harnesses remain largely hand-crafted and static: each new model or task still demands bespoke scaffolding, and the rich traces produced during execution are rarely distilled back into systematic improvement. We introduce HarnessX, a foundry for composable, adaptive, and evolvable agent harnesses. HarnessX assembles typed harness primitives via a substitution algebra, adapts them through AEGIS, a trace-driven multi-agent evolution engine grounded in an operational mirror between symbolic adaptation and reinforcement learning, and closes the harness-model loop by turning trajectories into both harness updates and model training signal. Across five benchmarks (ALFWorld, GAIA, WebShop, tau^3-Bench, and SWE-bench Verified), HarnessX yields an average gain of +14.5% (up to +44.0%), with gains largest where baselines are lowest. These results suggest that agent progress need not come from model scaling alone: composing and evolving runtime interfaces from execution feedback is an actionable and complementary lever. Project homepage: https://darwin-agent.github.io/HarnessX/.

Subjects: Artificial Intelligence (cs.AI)

Cite as: arXiv:2606.14249 [cs.AI]

https://doi.org/10.48550/arXiv.2606.14249

## Submission history

- [v1] Fri, 12 Jun 2026 08:27:11 UTC (1,440 KB)
- [v2] Thu, 2 Jul 2026 03:16:03 UTC (1,454 KB)
- [v3] Thu, 23 Jul 2026 03:12:37 UTC (9,278 KB)
