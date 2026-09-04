---
source_url: https://adamtornhill.substack.com/p/an-opinionated-and-mainly-correct
title: "An opinionated (and mainly correct) guide to naming"
author: Adam Tornhill
publication: "Code for Humans and Machines (adamtornhill.substack.com)"
published: 2026-06-23
retrieved: 2026-06-28
type: note
capture_note: >
  SUMMARY NOTE, NOT VERBATIM. adamtornhill.substack.com is Tornhill's personal
  monetized publication; per the established watch convention (see log 2026-06-17,
  2026-06-23) his Substack pieces are captured as copyright-conscious summary
  notes with short representative quotes only, to be turned into a wiki source
  page on request. Part of his "AI-Readable Code" series. Full text was readable
  via WebFetch this run (modified_time meta = 2026-06-23T15:11:52Z), confirming
  the date and in-window status (lookback 14d).
---

# An opinionated (and mainly correct) guide to naming — summary

Tornhill's thesis: naming is not aesthetics — **good naming minimizes
"reconstruction work" for both humans and machines.** Names are "cognitive
compression mechanisms"; when reading unfamiliar code we infer purpose by
building mental representations driven largely by class/function names, so
stronger names make that process cheaper. He cites evidence that clearer
identifier names cut debugging time ~19% (Springer EMSE study) and that a recent
study on structural elements aiding LLM code understanding found **improving
identifier names "consistently yielded the largest returns"** (arXiv 2505.10443).
This is the same through-line as the rest of his series: optimize code so an
agent has to reconstruct less of the missing context.

Core habits he advocates:

- **Optimize function names for the calling context, not the declaration site** —
  we read call sites far more than declarations. Let names combine into sentences
  at the call site, e.g. `notify_all(registered_clients, about=the_new_version)`.
  A readable call becomes a single "chunk" that frees working memory and improves
  reasoning.
- **Derive names via "Wishful Thinking"** (from SICP): write the code as if the
  ideal abstraction already existed, get the sentence right, *then* implement.
  Naming comes first.
- **Let domain types liberate parameter names** — fight *primitive obsession*
  (`int languageId`, `int newsItemId`). Introduce real domain types
  (`Language preferredRssFeedLanguage`, `NewsItem clickedArticle`): the type says
  *what* the argument is, freeing the name to say *why* it's there.
- **Scope determines length** — names expand on surrounding context; smaller scope
  → shorter name. `i` is fine in a tight loop/lambda but detrimental as an
  instance variable or public API.

Conventions he argues *against* (the "what not to do"):

- **Drop the `I`-prefix on interfaces** (`ChatConnection`, not `IChatConnection`)
  — that something is an interface is the least interesting, leaky detail; callers
  shouldn't care about the implementation kind.
- **Get rid of getters/setters** — `get`/`set` are procedural and lead down the
  "asking rather than telling" path (cf. Tell-Don't-Ask). Model
  `set_customer_status(customer, SUSPENDED)` as `suspend(a_customer)`; even
  query-like functions read better renamed (`buyer = customer_for(customer_id)`).
  Invokes the *mere-exposure principle* — we prefer the familiar — and urges
  questioning whether practices are based on familiarity or reason.
- **Avoid the dumpster names** — `Utils`, `Misc`, `Helper` are vague labels that
  "attract code of those same qualities"; a utility class is "an admission that
  we're prepared to give up on our design." There's a hidden domain concept
  wanting a proper name.

Closing: good names guide future readers "whether they are fellow humans or,
increasingly common, coding agents" — both benefit from explicit intent and rich
context.

## Why it's a keeper (on-thread)

Directly extends the wiki's [[ai-readable-code]] thread and Tornhill's CLEAR
principles — naming as the most leverage-per-effort move for both human and
agent legibility, now with a cited LLM-code-understanding result. Updates:
[[ai-readable-code]], [[adam-tornhill]], [[tornhill-ai-readable-code-series]]
(new entry in the series), [[agent-legibility]].

## Caveat

Single-author opinion piece (explicitly "opinionated"); the supporting studies
are cited second-hand. Summary-only capture — not the author's full verbatim text.
