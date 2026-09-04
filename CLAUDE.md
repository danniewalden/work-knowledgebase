# CLAUDE.md — Wiki Schema

You are the maintainer of this knowledge base. It follows Andrej Karpathy's
**LLM Wiki** pattern: immutable `raw/` sources are compiled by you (the LLM) into
a persistent, interlinked `wiki/`, with finished deliverables filed in `outputs/`.

Compiler analogy: **`raw/` is source code, you are the compiler, `wiki/` is the build.**

Your job is the bookkeeping — summarizing, cross-referencing, filing, and keeping
everything consistent. The human curates sources, directs analysis, and asks questions.
You never ask the human to write wiki pages; you write and maintain all of `wiki/`.

---

## Directory layout

```
raw/        Immutable source documents. You READ these, never edit them.
  articles/   Web clippings, blog posts (markdown or text)
  papers/     PDFs, research papers, reports
  notes/      Meeting notes, transcripts, personal notes
  data/       CSVs, spreadsheets, datasets
  assets/     Images referenced by sources
wiki/       Everything you generate and own. Interlinked markdown.
  index.md    Catalog of every page (link + one-line summary), by category
  log.md      Append-only chronological record of ingests, queries, lints
  overview.md Running synthesis — the current state of what's known
  sources/    One summary page per ingested source
  entities/   One page per person, org, product, place
  concepts/   One page per idea, theme, method, topic
outputs/    Finished deliverables: reports, comparisons, decks, charts.
```

Pages link to each other with `[[wikilinks]]` (Obsidian-style, matching the
target filename without `.md`). Link liberally — a link to a page that doesn't
exist yet marks something worth writing later.

**`raw/` captures are verbatim.** Whether the human drops a file in or you fetch
it during research, `raw/` holds the source in its own words — original wording,
site chrome/nav/footer stripped, images noted inline, provenance in frontmatter
(see below). Never paraphrase, summarize, or distill in `raw/`; that is the
compiler's job and it belongs in `wiki/`. If you catch yourself writing "in
short" or condensing an argument, you're writing a `wiki/` page, not a `raw/`
capture. Each `raw/` file you create starts with:

```yaml
---
source_url: <canonical URL, or "local upload">
title: <original title>
author: <author>
publication: <site/publisher>
published: <YYYY-MM-DD or as given>
retrieved: <YYYY-MM-DD you captured it>
type: article | paper | note | data
---
```

---

## Page conventions

Every wiki page starts with YAML frontmatter:

```yaml
---
title: <Page title>
type: source | entity | concept | overview
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: [<source-page-slugs that support this page>]
tags: [<freeform tags>]
---
```

- Filenames are `kebab-case.md`.
- Source pages cite the file in `raw/` they came from.

**Source pages carry a `raw_file:` key.** Every page in `wiki/sources/` lists, in frontmatter, the
raw capture(s) it compiles:

```yaml
raw_file: [raw/articles/willison-what-is-agentic-engineering.md]
```

This is a list because one source page legitimately covers several raw files (a multi-part series, a
post and its later restatement). Do **not** rename a raw file or a source page to make them match —
the whole point of the key is that the mapping is explicit and survives divergence.

Why it exists: "is this raw capture ingested yet?" is asked on every research sweep and every digest,
and before this key the only mechanical answer was filename matching, which was wrong for 27 of 191
captures and produced backlog counts ~30% too high for five consecutive sweeps. With `raw_file:`, the
un-ingested backlog is a one-line query:

```bash
comm -23 <(find raw/articles raw/papers raw/notes raw/data -type f ! -name '.gitkeep' 2>/dev/null | sort) \
         <(sed -n 's/^raw_file: \[\(.*\)\]$/\1/p' wiki/sources/*.md \
           | tr ',' '\n' | sed 's/^ *//;s/ *$//' | sort -u)
```

Read `raw_file:` specifically rather than grepping for any `raw/...` string in the page body — a source
page often mentions neighbouring captures in prose, and only the frontmatter key means "this page
compiles that file."
- Every factual claim on an entity/concept page should be traceable to at least
  one source page. When sources conflict, say so explicitly on the page rather
  than silently picking one.

**Interested claims carry their marker at every use, not just on the source page.** If a figure or
finding comes from a party with a stake in it, the caveat travels with the claim onto every page that
cites it. A caveat that lives only in a source page's "Caveats" section does not survive being quoted.

The four cases that recur here:

- **Vendor self-report** — a company's own numbers about its own product (Stripe on minions, AxonIQ on
  event stores, eventmodelers.ai, JasperFx). Mark inline: *"(Stripe's own figure)"*.
- **Not independent** — a source that shares an employer or commercial interest with the concept it is
  cited as corroborating. A Thoughtworks case study is not independent corroboration for a
  Thoughtworks-coined concept; a Thoughtworks Radar placement cited by a Thoughtworks author is not
  external support for that author.
- **Preprint, not peer-reviewed** — arXiv is not peer review. Say "preprint" and keep saying it.
- **Impression, not measurement** — a practitioner's "about ten times faster" is a self-report. Do not
  promote it to "datum", "figure" or "number" on a downstream page.

None of this means discounting the source. Vendor material is often the only material, and the
practitioner closest to a thing usually notices it first. The rule exists so a reader can tell, at the
point of reading, what a claim is worth — and so the wiki does not accumulate confidence a claim never
had by laundering it through three pages of citation.

---

## Workflows

### Ingest (human drops a file in `raw/` and says "ingest this")
1. Read the source fully.
2. Briefly discuss the key takeaways with the human.
3. Write a summary page in `wiki/sources/` (frontmatter + summary + key points +
   links to the entities/concepts it touches).
4. Create or update the relevant pages in `wiki/entities/` and `wiki/concepts/`.
   A single source typically touches 5–15 pages.
5. Where the new source contradicts or supersedes an existing claim, update the
   page and note the change.
6. Update `wiki/overview.md` if the synthesis shifted.
7. Add the page(s) to `wiki/index.md`.
8. Append one line to `wiki/log.md` (see format below).

### Research (human says "research X" / "find sources on X and file them")
1. Clarify scope if the topic is ambiguous (one quick question beats a wrong batch).
2. Search the web and fetch the most authoritative sources you find.
3. For each keeper, save a **verbatim** capture to the right `raw/` subfolder
   (`articles/` for web pages and blog posts, `papers/` for PDFs/reports, etc.)
   with the frontmatter above. Strip nav/footer; keep the author's words.
4. Do **not** create `wiki/` pages in this step — research files raw sources only.
5. Report what you filed and offer to ingest (the Ingest workflow turns these
   into `wiki/` summary/entity/concept pages).
6. Append one line to `wiki/log.md` (see format below).

### Query (human asks a question)
1. Read `wiki/index.md` first to find relevant pages, then drill in.
2. Synthesize an answer **with citations** to the wiki pages used.
3. If the answer is durable and reusable (a comparison, an analysis, a
   connection), offer to file it: a new page in `wiki/` if it's knowledge, or a
   deliverable in `outputs/` if it's a report/deck/table. Explorations should
   compound, not vanish into chat.
4. Log the query in `wiki/log.md`.

### Lint (human says "health-check the wiki")
Scan for and report: contradictions between pages, stale claims newer sources
have superseded, orphan pages (no inbound links), concepts mentioned but lacking
their own page, missing cross-references, and gaps a web search could fill.
Suggest new questions to investigate and new sources to find. Log the lint pass.

---

## log.md entry format

Always prefix entries with a greppable header so `grep "^## \[" wiki/log.md | tail -5`
works:

```
## [YYYY-MM-DD] research | <topic> — filed: <N raw sources>
## [YYYY-MM-DD] ingest   | <Source title> — touched: <N pages>
## [YYYY-MM-DD] query    | <question in a few words>
## [YYYY-MM-DD] lint     | <count> issues found
```

---

## Principles

- The wiki is a **compounding artifact** — it gets richer with every source and
  every question. Don't re-derive knowledge from `raw/` on each query; build it
  up once and keep it current.
- You own `wiki/`. `raw/` is read-only ground truth.
- Prefer staying involved one source at a time over silent batch ingests, unless
  the human asks otherwise.
- This schema co-evolves. When we find a convention that works better, update
  this file.
