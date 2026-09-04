---
source_url: https://arxiv.org/abs/2605.18747
title: "Code as Agent Harness"
author: Xuying Ning, Katherine Tieu, Dongqi Fu, Tianxin Wei, Zihao Li, Yuanchen Bei, Jiaru Zou, Mengting Ai, Zhining Liu, Ting-Wei Li, Lingjie Chen, Yanjun Zhao, Ke Yang, Bingxuan Li, Cheng Qian, Gaotang Li, Xiao Lin, Zhichen Zeng, Ruizhong Qiu, Sirui Chen, Yifan Sun, Xiyuan Yang, Ruida Wang, Rui Pan, Chenyuan Yang, Dylan Zhang, Liri Fang, Zikun Cui, Yang Cao, Pan Chen, Dorothy Sun, Ren Chen, Mahesh Srinivasan, Nipun Mathur, Yinglong Xia, Hong Li, Hong Yan, Pan Lu, Lingming Zhang, Tong Zhang, Hanghang Tong, Jingrui He
publication: arXiv (cs.CL; cs.AI), arXiv:2605.18747
published: 2026-05-18
retrieved: 2026-09-04
type: paper
capture_note: >
  PREPRINT — NOT PEER-REVIEWED. arXiv preprint; arXiv is not peer review, and this
  caveat travels with any claim drawn from it.

  PARTIAL VERBATIM CAPTURE. Captured verbatim from the arXiv abstract page
  (arxiv.org/abs/2605.18747): title, author list, abstract in full, comments,
  subject classes, cite-as line, DOI and submission history. Additionally
  captured from the HTML version (arxiv.org/html/2605.18747v1): the affiliation
  list and the complete section/subsection heading tree. NOT captured: the body
  prose of all five sections, every figure and table, the per-method summary
  tables, and the references. This is a very large survey (five sections, ~50
  subsections); what is here is its abstract plus its map, not its content. The
  full PDF was not retrieved.

  Note on affiliations: the HTML lists three institutions (University of Illinois
  Urbana-Champaign, Meta, Stanford University) without a per-author marker
  mapping that this capture reproduces, so no author is attributed to a specific
  institution here.
---

# Code as Agent Harness

Computer Science > Computation and Language

[Submitted on 18 May 2026]

Xuying Ning, Katherine Tieu, Dongqi Fu, Tianxin Wei, Zihao Li, Yuanchen Bei, Jiaru Zou, Mengting Ai, Zhining Liu, Ting-Wei Li, Lingjie Chen, Yanjun Zhao, Ke Yang, Bingxuan Li, Cheng Qian, Gaotang Li, Xiao Lin, Zhichen Zeng, Ruizhong Qiu, Sirui Chen, Yifan Sun, Xiyuan Yang, Ruida Wang, Rui Pan, Chenyuan Yang, Dylan Zhang, Liri Fang, Zikun Cui, Yang Cao, Pan Chen, Dorothy Sun, Ren Chen, Mahesh Srinivasan, Nipun Mathur, Yinglong Xia, Hong Li, Hong Yan, Pan Lu, Lingming Zhang, Tong Zhang, Hanghang Tong (corresponding author), Jingrui He (corresponding author)

Affiliations: University of Illinois Urbana-Champaign; Meta; Stanford University

## Abstract

Recent large language models (LLMs) have demonstrated strong capabilities in understanding and generating code, from competitive programming to repository-level software engineering. In emerging agentic systems, code is no longer only a target output. It increasingly serves as an operational substrate for agent reasoning, acting, environment modeling, and execution-based verification. We frame this shift through the lens of agent harnesses and introduce code as agent harness: a unified view that centers code as the basis for agent infrastructure. To systematically study this perspective, we organize the survey around three connected layers. First, we study the harness interface, where code connects agents to reasoning, action, and environment modeling. Second, we examine harness mechanisms: planning, memory, and tool use for long-horizon execution, together with feedback-driven control and optimization that make harness reliable and adaptive. Third, we discuss scaling the harness from single-agent systems to multi-agent settings, where shared code artifacts support multi-agent coordination, review, and verification. Across these layers, we summarize representative methods and practical applications of code as agent harness, spanning coding assistants, GUI/OS automation, embodied agents, scientific discovery, personalization and recommendation, DevOps, and enterprise workflows. We further outline open challenges for harness engineering, including evaluation beyond final task success, verification under incomplete feedback, regression-free harness improvement, consistent shared state across multiple agents, human oversight for safety-critical actions, and extensions to multimodal environments. By centering code as the harness of agentic AI, this survey provides a unified roadmap toward executable, verifiable, and stateful AI agent systems.

Comments: GitHub: this https URL

Subjects: Computation and Language (cs.CL); Artificial Intelligence (cs.AI)

Cite as: arXiv:2605.18747 [cs.CL]

https://doi.org/10.48550/arXiv.2605.18747

## Submission history

From: Xuying Ning
- [v1] Mon, 18 May 2026 17:59:03 UTC (7,860 KB)

---

## Section structure (headings verbatim, from the HTML version)

1. Introduction
2. Harness Interface: Code for Reasoning, Acting, and Environment Modeling
   - 2.1 Code for Reasoning — 2.1.1 Program-Delegated Reasoning; 2.1.2 Formal Verification and Symbolic Reasoning Interfaces; 2.1.3 Iterative Code-Grounded Reasoning
   - 2.2 Code for Acting — 2.2.1 Grounded Skill Selection; 2.2.2 Programmatic Policy Generation; 2.2.3 Lifelong Code-Based Agents
   - 2.3 Code for Environment — 2.3.1 Structured World Representations; 2.3.2 Execution-Trace World Modeling; 2.3.3 Code-Grounded Evaluation Environments; 2.3.4 Verifiable Environment Construction
3. Harness Mechanisms: Planning, Memory, Tool Use, Control, and Optimization
   - 3.1 Planning for Agent Harness — 3.1.1 Linear Decomposition Planning; 3.1.2 Structure-grounded Planning; 3.1.3 Search-based Planning; 3.1.4 Orchestration-based Planning
   - 3.2 Memory and Context Engineering for Agent Harness — 3.2.1 Working Memory; 3.2.2 Semantic Memory; 3.2.3 Experiential Memory; 3.2.4 Long-Term Memory; 3.2.5 Multi-Agent Memory; 3.2.6 Context Compaction and State Offloading
   - 3.3 Tool Use for Agent Harness — 3.3.1 Function-Oriented Tool Use; 3.3.2 Environment-Interaction Tool Use; 3.3.3 Verification-Driven Tool Use; 3.3.4 Workflow-Orchestration Tool Use
   - 3.4 Harness Control through the Plan, Execute, and Verify Loop — 3.4.1 From Debugging to Harness-Level Control; 3.4.2 Planning as Contract Formation; 3.4.3 Sandboxed Execution and Permissioned State Transition; 3.4.4 Verification through Deterministic Sensors
   - 3.5 Agentic Harness Engineering for Adaptive Harness Optimization — 3.5.1 Deep Telemetry as the Optimization Substrate; 3.5.2 The Evolution Agent; 3.5.3 Governed Harness Mutation
4. Scaling the Harness: Multi-Agent Orchestration over Code
   - 4.1 Improved Coding Support through Multi-agent Collaboration — 4.1.1 Functional Role Specialization and Human-Guided Planning; 4.1.2 Diverse Interaction Modes Grounded in Shared Program State; 4.1.3 Optimized Workflow Topology for Agentic Coordination
   - 4.2 Execution Feedback and Shared-Harness Synchronization — 4.2.1 Execution Feedback Integration; 4.2.2 Shared-Harness Synchronization
   - 4.3 Position: The Shared Code-Centric Harness Substrate — 4.3.1 Shared Harness Representation; 4.3.2 Harness-State Convergence
   - 4.4 Patterns and Trends
5. Emerging Fields and Open Problems
   - 5.1 Emerging Fields and Tangible Applications — 5.1.1 Code Assistants; 5.1.2 GUI/OS Agents as a Program World; 5.1.3 Autonomous Embodied Agents; 5.1.4 Agents for Scientific Discovery as Program Worlds; 5.1.5 Agent Personalization
   - 5.2 Open Problems — 5.2.1 Harness-Level Evaluation and Oracle Adequacy; 5.2.2 Semantic Verification Beyond Executable Feedback; 5.2.3 Self-Evolving Harnesses without Regression; 5.2.4 Transactional Shared Program State and Semantic Conflict Resolution; 5.2.5 Human-in-the-Loop Safety and Accountability as Harness State; 5.2.6 Multimodal Code-Harness Systems; 5.2.7 Toward a Science of Harness Engineering
