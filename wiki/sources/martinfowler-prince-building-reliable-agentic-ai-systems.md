---
title: "Kulkarni/Thoughtworks — Building Reliable Agentic AI Systems (Bayer PRINCE)"
type: source
created: 2026-06-29
updated: 2026-06-29
sources: [martinfowler-prince-building-reliable-agentic-ai-systems]
raw_file: [raw/articles/martinfowler-prince-building-reliable-agentic-ai-systems.md]
tags: [harness-engineering, context-engineering, multi-agent-orchestration, agent-observability-and-evals, agent-explainability, agentic-ai, focus]
---

# Building Reliable Agentic AI Systems — the Bayer PRINCE case study

Article by **Sarang Kulkarni** ([[thoughtworks|Thoughtworks]]) on **martinfowler.com** (2026-06-16).
Source: `raw/articles/martinfowler-prince-building-reliable-agentic-ai-systems.md`. A rare
**independent, real-world production** case study — surfaced via the watch because martinfowler.com is
[[birgitta-bockeler|Böckeler]]'s venue, though this is a colleague's piece, not hers. Companion
peer-reviewed paper in *Frontiers in AI* (2025).

## What PRINCE is

**PRINCE** (Preclinical Information Center) is Bayer's agentic research assistant over decades of
preclinical study reports, built with Thoughtworks. It evolved **Search → Ask → Do**: keyword search →
RAG question-answering over unstructured PDFs → a multi-agent assistant that orchestrates workflows and
drafts regulatory documents. **Agentic RAG + Text-to-SQL**, orchestrated with **LangGraph**, served via
FastAPI; vector store in OpenSearch, structured data via Athena, agent state checkpointed in PostgreSQL,
app state in DynamoDB.

## The reliability architecture (read through two lenses)

The author explicitly frames the engineering as **[[context-engineering]]** (what each model sees) +
**[[harness-engineering]]** (the scaffolding around it) — terms not used at design time but fitting in
hindsight.

- **Multi-agent orchestration** ([[multi-agent-orchestration]]): a Clarify-Intent gate, a **Think & Plan**
  step (process reflection — *am I on the right trajectory?*, inspired by Anthropic's Think tool), a
  **Researcher** agent (hybrid RAG retrieval — keyword extraction, metadata filtering, query expansion,
  weighted hybrid search, cross-encoder rerank to k=7 — plus Text-to-SQL with schema-subset injection
  and 3-try error-correction), a **Reflection** agent (data reflection — *is the evidence sufficient?*),
  and a **Writer** agent (synthesis + a draft-reflection loop). **Three complementary reflection loops:
  process, data, draft.** Evolving toward **domain-specific Researcher sub-agents** (toxicology vs
  pharmacology) each owning their tools/schema.
- **Resilience** ([[harness-engineering]]): LLM fallbacks across providers, retries at both LLM-call and
  LangGraph-node level, errors fed back to the agent to replan, and **state persistence** so a failed run
  **resumes from the failed node** (user-initiated retries skip completed steps).
- **Trust / explainability** ([[agent-explainability]]): per-sentence **citations** to source chunks
  (page number + exact quote), visible intermediate steps, and human-in-the-loop on regulatory drafts
  ("final submissions authored and approved by qualified personnel").
- **Evaluation** ([[agent-observability-and-evals]]): **Langfuse** traces + **RAGAS** metrics
  (Faithfulness, Answer/Context Relevancy, Accuracy, Semantic Similarity); dataset evals on change +
  daily live-traffic evals.

## The core lesson — context discipline

"Larger context windows did not remove the need to be selective about what each agent sees." PRINCE
**routes the right context to the right capability**: planning context for Think&Plan, retrieval context
for the Researcher, evidence context for the Reflection agent, synthesis context for the Writer —
reducing **context pollution** and making each agent independently evaluable/debuggable. Headline:
"production-ready agentic AI is not only about better models or prompts. Reliability comes from
engineering both the **context** the model sees and the **harness** within which it acts."

## Why it matters here

The strongest **independent, regulated-enterprise** corroboration in the KB that the harness +
context-engineering vocabulary (Threads 3–4) describes how reliable agentic systems are actually built —
a system that arrived at the KB's framing on its own. Concrete worked instances of
[[multi-agent-orchestration]], reflection-as-[[feedforward-and-feedback-controls|sensor]],
[[agent-explainability]] via citation, and [[agent-observability-and-evals]] in production. Caveat:
Thoughtworks-authored (the firm that coined "harness engineering"), and a single deployment.

## Touches

[[thoughtworks]] · [[harness-engineering]] · [[context-engineering]] · [[multi-agent-orchestration]] ·
[[agent-observability-and-evals]] · [[agent-explainability]] · [[agentic-ai]] · [[context-rot]] ·
[[birgitta-bockeler]]

_Source: `raw/articles/martinfowler-prince-building-reliable-agentic-ai-systems.md`._
