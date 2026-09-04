---
source_url: https://arxiv.org/abs/2601.02200
title: "Code for Machines, Not Just Humans: Quantifying AI-Friendliness with Code Health Metrics"
author: Markus Borg, Nadim Hagatulah, Adam Tornhill, Emma Söderberg
publication: arXiv (cs.SE); accepted for 3rd ACM International Conference on AI Foundation Models and Software Engineering (FORGE 2026)
published: 2026-01-05
retrieved: 2026-06-16
type: paper
arxiv_id: 2601.02200
doi: 10.48550/arXiv.2601.02200
license: arXiv non-exclusive license to distribute (v1.0)
---

# Code for Machines, Not Just Humans: Quantifying AI-Friendliness with Code Health Metrics

> **Note on this capture:** verbatim transcription of the arXiv abstract page plus the
> Introduction, Background/Related Work, and Method (sections 1–3.2 as available in the
> experimental HTML). MathML markup has been rendered to plain inline notation (e.g.
> `CH≥9`); no wording has been paraphrased or condensed. Results/Discussion sections of
> the full paper are not transcribed here — see the PDF/HTML at the source URL.

**Authors:** Markus Borg, Nadim Hagatulah, Adam Tornhill, Emma Söderberg
**Subjects:** Software Engineering (cs.SE); Artificial Intelligence (cs.AI)
**Comments:** Accepted for the 3rd ACM International Conference on AI Foundation Models and Software Engineering (FORGE 2026)
**Submitted:** Mon, 5 Jan 2026 15:23:55 UTC

## Abstract

We are entering a hybrid era in which human developers and AI coding agents work in the same codebases. While industry practice has long optimized code for human comprehension, it is increasingly important to ensure that LLMs with different capabilities can edit code reliably. In this study, we investigate the concept of ``AI-friendly code'' via LLM-based refactoring on a dataset of 5,000 Python files from competitive programming. We find a meaningful association between CodeHealth, a quality metric calibrated for human comprehension, and semantic preservation after AI refactoring. Our findings confirm that human-friendly code is also more compatible with AI tooling. These results suggest that organizations can use CodeHealth to guide where AI interventions are lower risk and where additional human oversight is warranted. Investing in maintainability not only helps humans; it also prepares for large-scale AI adoption.

## 1. Introduction (excerpt)

In this paper, we investigate the relationship between code quality and AI-friendliness. We measure quality using the CodeHealth (CH) metric, which has been validated as predictive of defects and development effort in previous studies (Tornhill and Borg, 2022; Borg et al., 2024b, a). The metric has also been used in recent industry-facing AI studies (Borg et al., 2025; Meaden et al., 2025). We use the success rate of AI-generated refactoring, i.e., improving the design of existing code without changing its behavior, as a proxy for AI-friendliness. Refactoring lets us use passing unit tests as an oracle for functional correctness. Thus, an AI refactoring is correct if tests pass and beneficial if CH increases.

Our results confirm that human-friendly code is more compatible with AI tooling. LLMs tasked with refactoring have significantly lower break rates on code in the Healthy CodeHealth range (CH≥9), with corresponding risk reductions of 15-30%. Furthermore, we show that CH outperforms perplexity (PPL, an LLM-intrinsic confidence metric) and Source Lines of Code (SLOC) as a predictor of refactoring correctness.

These findings can support software organizations in the adoption of AI-assisted coding. We propose using CH to identify parts of the code that are ready for AI processing, as well as highlighting code with too much risk of breaking. More broadly, this research adds a missing piece to AI adoption: a shared code-quality metric that aligns humans and machines. While earlier research positioned code quality as a business imperative, we posit that code quality is a prerequisite for safe and effective use of AI – which might prove existential for software organizations in the next decade.

## 2. Background and Related Work (excerpt)

### 2.1. Maintainability and CodeHealth

CodeHealth™ (CH) is a quality metric used in the CodeScene software engineering intelligence platform. Its goal is to capture how cognitively difficult it is for human developers to comprehend code. CodeScene identifies code smells (Lacerda et al., 2020), e.g., God classes, deeply nested logic, and duplicated code. For Python, which we target in this paper, CodeScene detects 25 code smells.

CodeScene combines the number and severity of detected smells into a file-level score from 1 to 10. Lower scores indicate higher cognitive load for humans, i.e., higher maintenance effort. CodeScene categorizes files as belonging to one of three CH intervals: Healthy (CH ≥9), Warning (4 ≤ CH < 9), and Alert (CH < 4). In this study, we refer to both Warning and Alert files as Unhealthy.

We have previously validated the CH metric in a series of studies. In a study on the manually annotated Maintainability Dataset (Schnappinger et al., 2020), we reported that CH aligns better with human maintainability judgments than competing metrics and the average human expert (Borg et al., 2024a). Furthermore, we have validated the metric from a business perspective through the association between CH on the one hand and file-level defect density and development time on the other hand (Tornhill and Borg, 2022; Borg et al., 2024b). Building on our previous work, we now investigate the relation between CH and AI-friendliness.

### 2.4. AI Refactoring

During 2025, agentic AI has been a major trend in industry and research. Coding agents are driven by LLMs, but they typically claim to 1) understand codebases beyond limited context windows and to 2) maintain a memory. This enables agents to take on larger tasks and operate more autonomously. The arguably most popular agent in industry at this time of writing is Anthropic's Claude Code, carefully described by Watanabe et al. (2025). We refer to reviews by He et al. (2025) and Wang et al. (2025) for contemporary overviews of the academic literature.

Refactoring is one of the many tasks investigated for coding agents. For example, Xu et al. presented MANTRA, a multi-agent framework for refactoring (Xu et al., 2025). MANTRA organizes three agents into 1) developer, 2) reviewer, and 3) repair roles for the refactoring task, and outperforms direct LLM-usage. However, Claude is also a capable refactoring agent despite not being a multi-agent solution. In this study, we study Claude (v2.0.13) as a representative example of contemporary agentic AI refactoring. Moreover, MANTRA is not publicly available at the time of this writing.

## 3. Method (excerpt)

Our goal is to explore how code characteristics influence the capabilities of AI refactoring, with a particular focus on CH. We formulate three Research Questions (RQs) that explore code characteristics in light of AI-friendliness. First, we take an LLM-intrinsic perspective and study PPL. This connects to related work and provides a baseline. Second, we look at how the CH is associated with the success rate of a downstream AI task. Third, we examine the predictive power of CH compared to SLOC and PPL.

- RQ1: How does perplexity differ between Healthy and Unhealthy code?
- RQ2: How does the AI refactoring break rate differ between Healthy and Unhealthy code?
- RQ3: To what extent can CodeHealth predict the AI refactoring break rate?

### 3.1. Dataset Creation

We sample from the CodeContests dataset hosted on GitHub by Google DeepMind. The dataset was introduced by Li et al. (2022) as training data for AlphaCode and contains more than 12 million solutions (correct and incorrect) to competitive programming problems from five sources. We study code in this domain because the problems come with carefully crafted test cases that verify functional correctness, providing a practical oracle after refactoring.

We construct a dataset of 5,000 solutions based on four design choices. First, we decided to focus on solutions written in Python to increase novelty and convenience. While CodeContests also contains solutions in Java and C++, Java has been extensively studied in refactoring research, and C++ has a more complex compile-and-test procedure. Second, we require at least one CodeScene code smell in the solutions. Removing code smells is a realistic refactoring goal. Third, we chose to only study solutions containing between 60 and 120 SLoC. There is a strong correlation between maintainability and size (Sjoberg et al., 2013), thus we control for this, at least partly, already during the sampling. Fourth, we actively seek diversity in the dataset, as many solutions are highly similar.

### 3.2. Selection of Large Language Models

We select six LLMs for evaluation. Five are open-weight models with about 20-30B parameters, runnable on our local datacenter. We select four models based on popularity and download statistics from Hugging Face and complement them with an LLM recently published by IBM – we refer to these as medium-sized LLMs. Moreover, we include a State-of-the-Art (SotA) LLM that we prompt using Anthropic's API. (Models include gemma-3-27b-it (Google, Mar 2025); GLM-4-32B-0414 (Zhipu AI, Apr 2025); Granite (IBM); and others.)
