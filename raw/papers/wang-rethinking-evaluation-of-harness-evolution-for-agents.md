---
source_url: https://arxiv.org/abs/2607.12227
title: "Rethinking the Evaluation of Harness Evolution for Agents"
author: Yike Wang, Huaisheng Zhu, Zhengyu Hu, Yige Yuan, Zhengyu Chen, Shakti Senthil, Hannaneh Hajishirzi, Yulia Tsvetkov, Pradeep Dasigi, Teng Xiao
publication: arXiv (cs.AI), arXiv:2607.12227
published: 2026-07-14
retrieved: 2026-09-04
type: paper
capture_note: >
  PREPRINT — NOT PEER-REVIEWED. arXiv preprint; arXiv is not peer review, and this
  caveat travels with any claim drawn from it. Note that this is a negative-result
  paper about other preprints' evaluation protocols, so the caveat cuts both ways:
  its critique is itself un-reviewed.

  PARTIAL VERBATIM CAPTURE. Captured verbatim from the arXiv abstract page
  (arxiv.org/abs/2607.12227, v2 the current version): title, author list,
  abstract in full, subject class, cite-as line, DOI and submission history. NOT
  captured: author affiliations (not shown on the abstract page), the paper body,
  the experimental setup, all figures, tables and per-baseline results, and the
  references. The HTML version was not retrieved (the fetch was rate-limited);
  the full PDF was not retrieved. Same scope as the existing evo-bench and sbco
  captures: abstract page only.
---

# Rethinking the Evaluation of Harness Evolution for Agents

Computer Science > Artificial Intelligence

[Submitted on 14 Jul 2026 (v1), last revised 27 Aug 2026 (this version, v2)]

Yike Wang, Huaisheng Zhu, Zhengyu Hu, Yige Yuan, Zhengyu Chen, Shakti Senthil, Hannaneh Hajishirzi, Yulia Tsvetkov, Pradeep Dasigi, Teng Xiao

## Abstract

We revisit the evaluation of automatic harness evolution for LLM agents. Existing harness evolution methods use unit test cases to search for harness configurations and then report final performance on the same public benchmark. This protocol raises two fundamental concerns. First, harness evolution is itself an iterative search procedure that repeatedly evaluates and revises candidate harnesses using task feedback. As in agentic test-time scaling, it should therefore be compared with simple task-level search baselines under matched feedback and inference budgets to determine whether its gains arise from improved harness design or from additional search alone. Second, because the search and the final evaluation share the same benchmark, the reported gains risk overfitting to that specific task set. To address these concerns, we conduct an extensive evaluation comparing harness evolution with simple test-time scaling and discovery baselines under comparable feedback and inference budgets, and also evaluate evolved harnesses on held-out tasks to assess whether the discovered improvements generalize. Experiments on Terminal-Bench 2.1 with GPT-5.4 and Claude Opus 4.6 show that automatic harness evolution does not consistently outperform simple test-time scaling methods and exhibits limited generalization. Our results raise important questions about the effectiveness of automatic harness evolution and highlight the need for fairer evaluation protocols and benchmarks for automatic harness design. Our code is available at https://github.com/rethinking-harness-evolution.

Subjects: Artificial Intelligence (cs.AI)

Cite as: arXiv:2607.12227 [cs.AI] (or arXiv:2607.12227v2 [cs.AI] for this version)

https://doi.org/10.48550/arXiv.2607.12227

License: CC BY 4.0

## Submission history

From: Yike Wang
- [v1] Tue, 14 Jul 2026 00:18:42 UTC (113 KB)
- [v2] Thu, 27 Aug 2026 12:13:50 UTC (113 KB)
