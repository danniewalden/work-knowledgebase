---
title: "Source: Karpathy — LLM Wiki"
type: source
created: 2026-06-11
updated: 2026-06-11
sources: [karpathy-llm-wiki]
tags: [knowledge-management, llm, pkm, method]
---

# Source: Karpathy — LLM Wiki

**Raw file:** `raw/articles/karpathy-llm-wiki.md`
**Origin:** [gist.github.com/karpathy/442a6bf555914893e9891c11519de94f](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
**Author:** [[andrej-karpathy]]

## Summary

An "idea file" describing a pattern for building personal knowledge bases with LLMs.
Rather than RAG (retrieve chunks fresh on every query), the LLM **incrementally builds
and maintains a persistent, interlinked markdown wiki** that sits between you and your
raw sources. Knowledge is compiled once and kept current, so it **compounds** over time.
This wiki itself is an instance of the pattern.

## Key points

- Contrasts with [[retrieval-augmented-generation]]: RAG re-derives knowledge each query;
  the [[llm-wiki]] accumulates it.
- Three layers: immutable **raw sources** → an **LLM-owned wiki** → a **schema** file
  (`CLAUDE.md`). See [[llm-wiki]].
- Three operations: **ingest**, **query**, **lint**. See [[llm-wiki]].
- Two navigation files: `index.md` (content catalog) and `log.md` (chronological,
  greppable history).
- The human curates and asks; the LLM does all summarizing, cross-referencing, and
  bookkeeping — the maintenance burden that makes humans abandon wikis.
- Spiritually related to Vannevar Bush's [[memex]] (1945); the LLM solves the
  "who maintains it" problem Bush couldn't.
- Optional tooling: Obsidian (graph view, Web Clipper, Marp, Dataview), a search engine
  like `qmd` at larger scale. The wiki is just a git repo of markdown.

## Touches

[[andrej-karpathy]] · [[llm-wiki]] · [[retrieval-augmented-generation]] · [[memex]] ·
[[append-and-review-note]]
