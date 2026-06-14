# Work Knowledgebase

A personal knowledge base built on Andrej Karpathy's
[**LLM Wiki** pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f):
you curate sources, an LLM compiles them into a persistent, interlinked wiki, and
the knowledge **compounds** over time instead of being re-derived on every question.

This is different from RAG. RAG retrieves chunks at query time and rediscovers
everything from scratch each time. Here, the LLM reads each source once, integrates
it into the wiki, updates cross-references, and flags contradictions — so the
synthesis already reflects everything you've read.

## The three layers

```
raw/        Immutable sources you curate.        ← source code
wiki/       LLM-generated interlinked markdown.   ← compiled output
outputs/    Finished reports, decks, charts.      ← deliverables
CLAUDE.md   The schema that runs it all.          ← the config
```

The compiler analogy: **`raw/` is source code, the LLM is the compiler, `wiki/`
is the build.** `CLAUDE.md` is the load-bearing file — it's what makes the LLM a
disciplined wiki maintainer rather than a generic chatbot.

## How to use it

1. **Add a source.** Drop a file into the right `raw/` subfolder (`articles/`,
   `papers/`, `notes/`, `data/`).
2. **Ingest it.** Open this folder in Cowork (or Claude Code) and say
   *"ingest raw/papers/<filename>"*. The LLM summarizes it, updates entity and
   concept pages, refreshes the overview, and logs the ingest.
3. **Ask questions.** *"What do my sources say about X?"* The LLM reads
   `wiki/index.md`, drills into the relevant pages, and answers with citations.
   Good answers get filed back into the wiki or `outputs/`.
4. **Lint periodically.** *"Health-check the wiki"* — the LLM finds
   contradictions, stale claims, orphan pages, and gaps to fill.

## Navigation

- [wiki/index.md](wiki/index.md) — catalog of every page
- [wiki/overview.md](wiki/overview.md) — running synthesis
- [wiki/log.md](wiki/log.md) — chronological history
- [CLAUDE.md](CLAUDE.md) — the schema (read this to understand the conventions)

You write almost nothing here yourself. You curate, direct, and ask; the LLM does
the summarizing, cross-referencing, and bookkeeping.

---

### Optional companion: the append-and-review note

Karpathy's other note-taking idea is the
[append-and-review note](https://karpathy.bearblog.dev/the-append-and-review-note/):
one single plain-text note where you append every raw thought to the top, let old
ones sink "under gravity," and periodically rescue what still matters. It pairs
well with this wiki — use it as a fast capture inbox, then ingest the keepers as
sources. If you want one, ask and I'll add a `inbox.md` for it.
