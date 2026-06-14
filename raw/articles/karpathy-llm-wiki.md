# LLM Wiki — Andrej Karpathy

Source: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
Captured: 2026-06-11

A pattern for building personal knowledge bases using LLMs. This is an idea file,
designed to be copy-pasted to your own LLM agent (Claude Code, Codex, OpenCode, etc.).
Its goal is to communicate the high-level idea; the agent builds the specifics with you.

## The core idea

Most people's experience with LLMs and documents looks like RAG: you upload files,
the LLM retrieves relevant chunks at query time and generates an answer. This works,
but the LLM rediscovers knowledge from scratch on every question. There's no
accumulation. NotebookLM, ChatGPT file uploads, and most RAG systems work this way.

The idea here is different. Instead of just retrieving from raw documents at query
time, the LLM incrementally builds and maintains a persistent wiki — a structured,
interlinked collection of markdown files that sits between you and the raw sources.
When you add a source, the LLM reads it, extracts the key information, and integrates
it into the existing wiki — updating entity pages, revising topic summaries, noting
where new data contradicts old claims. The knowledge is compiled once and kept
current, not re-derived on every query.

The wiki is a persistent, compounding artifact. The cross-references are already
there. Contradictions have already been flagged. The synthesis already reflects
everything you've read. You never (or rarely) write the wiki yourself — the LLM
writes and maintains all of it. You're in charge of sourcing, exploration, and
asking the right questions. Obsidian is the IDE; the LLM is the programmer; the
wiki is the codebase.

Applies to many contexts: personal (goals, health, journaling), research (deep
dives over weeks), reading a book (companion wiki of characters/themes), business/
team (internal wiki fed by Slack, transcripts, docs), competitive analysis, due
diligence, trip planning, course notes, hobby deep-dives.

## Architecture — three layers

1. **Raw sources** — curated source documents (articles, papers, images, data).
   Immutable: the LLM reads but never modifies them. Source of truth.
2. **The wiki** — a directory of LLM-generated markdown (summaries, entity pages,
   concept pages, comparisons, an overview/synthesis). The LLM owns this entirely.
3. **The schema** — a document (CLAUDE.md for Claude Code, AGENTS.md for Codex)
   telling the LLM how the wiki is structured, the conventions, and the workflows.
   The key config that makes the LLM a disciplined maintainer, not a generic
   chatbot. You and the LLM co-evolve it.

## Operations

- **Ingest.** Drop a source into raw, tell the LLM to process it. It reads, discusses
  takeaways, writes a summary page, updates the index, updates entity/concept pages,
  appends to the log. One source might touch 10–15 pages. Prefer ingesting one at a
  time and staying involved; batch ingest is possible with less supervision.
- **Query.** Ask questions against the wiki. The LLM reads the index, drills into
  relevant pages, synthesizes an answer with citations. Output can be a page, a
  comparison table, a slide deck (Marp), a chart (matplotlib), a canvas. Good answers
  get filed back into the wiki as new pages so explorations compound.
- **Lint.** Periodically health-check: contradictions, stale claims, orphan pages,
  concepts lacking pages, missing cross-references, data gaps a web search could fill.
  The LLM suggests new questions and sources.

## Indexing and logging

- **index.md** is content-oriented: a catalog of every page (link + one-line summary,
  optional metadata), organized by category. Read first on every query. Works well at
  moderate scale (~100 sources, hundreds of pages) without embedding-based RAG.
- **log.md** is chronological: an append-only record of ingests, queries, lints. Keep
  entries greppable with a consistent prefix like `## [2026-04-02] ingest | Title` so
  `grep "^## \[" log.md | tail -5` works.

## Optional: CLI tools

As the wiki grows you may want a search engine over the pages. qmd is one option
(local hybrid BM25/vector search with LLM re-ranking, CLI + MCP server). Or vibe-code
a simple search script.

## Tips

Obsidian Web Clipper converts web articles to markdown. Download images locally so
the LLM can view them. Obsidian's graph view shows the shape of the wiki. Marp turns
markdown into slide decks. Dataview queries page frontmatter. The wiki is just a git
repo of markdown — version history and collaboration for free.

## Why this works

The tedious part of maintaining a knowledge base isn't the reading or thinking — it's
the bookkeeping: updating cross-references, keeping summaries current, flagging
contradictions, maintaining consistency across dozens of pages. Humans abandon wikis
because maintenance grows faster than value. LLMs don't get bored and can touch 15
files in one pass, so maintenance cost is near zero. Related in spirit to Vannevar
Bush's Memex (1945) — a personal, curated knowledge store with associative trails,
where the connections matter as much as the documents. The part Bush couldn't solve
was who does the maintenance. The LLM handles that.

## Note

The document is intentionally abstract — it describes the idea, not an implementation.
Directory structure, schema conventions, page formats, tooling all depend on your
domain and preferences. Everything is optional and modular.
