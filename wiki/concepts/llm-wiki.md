---
title: LLM Wiki
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [karpathy-llm-wiki]
tags: [knowledge-management, pkm, method, llm]
---

# LLM Wiki

A pattern (from [[andrej-karpathy]]) for building a personal knowledge base where an
LLM **incrementally builds and maintains** a structured, interlinked markdown wiki on
top of your raw sources. The knowledge is **compiled once and kept current** — a
compounding artifact — rather than re-derived on every query as in
[[retrieval-augmented-generation]]. This very knowledge base is an instance of it.

## Three layers

- **Raw sources** — curated, immutable source documents. The LLM reads, never edits.
  Source of truth. (Here: `raw/`.)
- **The wiki** — LLM-generated, LLM-owned interlinked markdown: source summaries,
  entity pages, concept pages, an overview/synthesis. (Here: `wiki/`.)
- **The schema** — a config document (`CLAUDE.md`) defining structure, conventions,
  and workflows; makes the LLM a disciplined maintainer rather than a generic chatbot.
  Co-evolves with use.

Compiler analogy: raw is source code, the LLM is the compiler, the wiki is the build.

## Three operations

- **Ingest** — process a new raw source: read it, write a summary page, update entity/
  concept pages (often 10–15 pages touched), append to the log.
- **Query** — ask questions; the LLM reads `index.md`, drills into pages, answers with
  citations. Durable answers get filed back into the wiki or `outputs/` so explorations
  compound.
- **Lint** — periodic health-check: contradictions, stale claims, orphan pages, missing
  concept pages, missing cross-references, gaps a web search could fill.

## Why it works

The hard part of a knowledge base isn't reading or thinking — it's the bookkeeping
(cross-references, current summaries, flagging contradictions, consistency). Humans
abandon wikis when maintenance outpaces value; LLMs don't get bored and can touch many
files in one pass, so maintenance cost is near zero. Spiritually close to the [[memex]].

## Navigation files

- `index.md` — content catalog (link + one-line summary per page), read first on queries.
- `log.md` — chronological, append-only, greppable history.

_Source pages: [[karpathy-llm-wiki]]._
