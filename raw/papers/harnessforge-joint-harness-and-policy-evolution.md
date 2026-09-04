---
source_url: https://arxiv.org/abs/2606.01779
title: "HarnessForge: Joint Harness and Policy Evolution for Adaptive Agent Systems"
author: Mingju Chen, Can Lv, Guibin Zhang, Heng Chang, Shiji Zhou
publication: arXiv (cs.CL), arXiv:2606.01779
published: 2026-06-01
retrieved: 2026-09-04
type: paper
capture_note: >
  PREPRINT — NOT PEER-REVIEWED. arXiv preprint; arXiv is not peer review, and this
  caveat travels with any claim drawn from it.

  PARTIAL VERBATIM CAPTURE, WITH A METADATA GAP. Captured verbatim from the HTML
  version (arxiv.org/html/2606.01779v1): title, author list, affiliations,
  corresponding/project-lead notes, the abstract in full, and the complete
  section and appendix heading list. NOT captured: the paper body (Introduction
  through Conclusion), all figures, tables and results, appendices A-G, and the
  references. The full PDF was not retrieved.

  METADATA GAP: the arXiv abstract page (arxiv.org/abs/2606.01779) could not be
  fetched — four WebFetch attempts all returned "this PDF is empty or contains no
  machine-readable text" — so the DOI line and the submission history (how many
  versions exist, and their dates and sizes) are NOT captured. The identifier,
  subject class (cs.CL), version (v1) and date (01 Jun 2026) below are read off
  the arXiv identifier stamp printed in the HTML version itself, not off an
  abstract page; the title and identifier were also independently confirmed by
  web search before capture. There may be later versions this capture does not
  know about.
---

# HarnessForge: Joint Harness and Policy Evolution for Adaptive Agent Systems

Mingju Chen, Can Lv, Guibin Zhang, Heng Chang, Shiji Zhou

Beijing Advanced Innovation Center for Future Blockchain and Privacy Computing, School of Artificial Intelligence, Beihang University; Tsinghua University

Project Lead: Heng Chang. Corresponding Author: Shiji Zhou (zhoushiji25@buaa.edu.cn)

## Abstract

LLM agents are increasingly expected to operate across heterogeneous task regimes that require distinct execution paradigms. This challenges fixed agent systems and motivates system-level meta-adaptation beyond isolated component updates. While existing works have adapted external harness or trained underlying reasoning policies, full-system adaptation remains insufficiently characterized. The adaptation space between structure and execution is rarely made explicit, and the compatibility between the external harness and the internal reasoner is not optimized jointly. We propose HarnessForge, a meta-adaptive framework for evolving LLM agent systems. HarnessForge formulates an agent system as a harness–policy pair, defining a stable adaptation space that separates harness-level execution structure from policy-level reasoning behavior. It then performs harness–policy co-evolution through fault-guided harness tailoring and harness-conditioned policy alignment. Experiments across five benchmarks from diverse domains show that HarnessForge consistently improves both Qwen3-4B and Qwen3-8B backbones, outperforming harness-only and policy-only baselines with gains of up to 12.0% over the strongest baseline and achieving favorable rollout-efficiency tradeoffs, demonstrating that harness–policy co-evolution is effective, and that executable compatibility between the harness and reasoning policy is essential for agent-system adaptation.

arXiv:2606.01779v1 [cs.CL] 01 Jun 2026

License: CC BY 4.0

---

## Section structure (headings verbatim, from the HTML version)

1. Introduction
2. Related Work
3. Methodology
4. Experiments
5. Conclusion
6. References
7. Appendix A: Algorithm and Notation
8. Appendix B: Datasets Details
9. Appendix C: Harness Tailoring Details
10. Appendix D: Policy Alignment Details
11. Appendix E: Baselines and Fairness Protocol
12. Appendix F: Reproducibility Artifacts
13. Appendix G: Additional Results and Analysis
