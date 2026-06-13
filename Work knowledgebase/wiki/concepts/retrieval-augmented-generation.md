---
title: Retrieval-Augmented Generation (RAG)
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [karpathy-llm-wiki, akka-event-sourcing-backbone-agentic-ai, akka-agentic-systems-are-distributed-systems]
tags: [llm, retrieval, contrast, agentic-ai]
---

# Retrieval-Augmented Generation (RAG)

The conventional way LLMs work over a document collection: files are indexed, and at
query time the LLM **retrieves relevant chunks** and generates an answer from them.
NotebookLM, ChatGPT file uploads, and most document-QA systems work this way.

It compensates for the LLM's training **cut-off** and for missing private data by supplying
the needed knowledge as context **within the prompt** — the "context augmentation" the name
refers to (per [[kevin-hoffman]], [[akka-event-sourcing-backbone-agentic-ai]]).

## Why the [[llm-wiki]] contrasts with it

Per [[karpathy-llm-wiki]], RAG rediscovers knowledge **from scratch on every question** —
nothing accumulates. A subtle question needing synthesis across five documents forces the
LLM to re-find and re-piece the fragments each time. The [[llm-wiki]] instead compiles
knowledge once into a persistent wiki and keeps it current, so cross-references and
synthesis already exist before the question is asked. At moderate scale (~100 sources)
a simple `index.md` catalog replaces embedding-based retrieval entirely.

_Source pages: [[karpathy-llm-wiki]]._
