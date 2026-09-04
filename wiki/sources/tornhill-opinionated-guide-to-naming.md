---
title: "Adam Tornhill — An Opinionated (and Mainly Correct) Guide to Naming"
type: source
created: 2026-06-29
updated: 2026-06-29
sources: [tornhill-opinionated-guide-to-naming]
raw_file: [raw/notes/tornhill-opinionated-guide-to-naming.md]
tags: [ai-readable-code, agent-legibility, agentic-coding, refactoring, focus]
---

# Adam Tornhill — An Opinionated (and Mainly Correct) Guide to Naming

Substack post by **[[adam-tornhill]]** ("Code for Humans and Machines", 2026-06-23), part of the
[[tornhill-ai-readable-code-series|AI-Readable Code series]]. Source: summary note
`raw/notes/tornhill-opinionated-guide-to-naming.md` (copyright-conscious summary, not verbatim).

## Thesis — naming is cognitive compression

Naming is not aesthetics: **good names minimize "reconstruction work" for both humans and machines.**
Names are "cognitive compression mechanisms" — reading unfamiliar code, we infer purpose from
class/function names, so stronger names make that inference cheaper. Cited evidence: clearer identifier
names cut debugging time ~19% (Springer EMSE), and a study on what helps **LLM** code understanding
found improving **identifier names "consistently yielded the largest returns"** (arXiv 2505.10443).
Same through-line as the rest of the series: shrink what an agent must reconstruct.

## Habits he advocates

- **Optimize names for the *call site*, not the declaration** — we read calls far more than
  declarations; let names form a sentence at the call site (`notify_all(registered_clients, about=…)`),
  a single readable "chunk."
- **Wishful Thinking** (from SICP) — write the code as if the ideal abstraction existed, get the
  sentence right, *then* implement. Naming comes first.
- **Let domain types liberate parameter names** — fight *primitive obsession* (`int languageId`);
  introduce real types (`Language preferredRssFeedLanguage`) so the type says *what* and the name is
  freed to say *why*.
- **Scope determines length** — `i` is fine in a tight loop, harmful as a public API name.

## Anti-patterns

- **Drop the `I`-prefix on interfaces** (`ChatConnection`, not `IChatConnection`) — implementation kind
  is the least interesting, leaky detail.
- **Get rid of get/set** — procedural accessors lead to "ask, don't tell"; model
  `set_status(customer, SUSPENDED)` as `suspend(a_customer)` (cf. Tell-Don't-Ask). Invokes the
  *mere-exposure principle*: question whether a practice is based on familiarity or reason.
- **Avoid dumpster names** (`Utils`, `Misc`, `Helper`) — vague labels that "attract code of those same
  qualities"; a utility class is "an admission that we're prepared to give up on our design." There's a
  hidden domain concept wanting a name.

## Why it matters here

The highest-leverage-per-effort entry in [[ai-readable-code]]: naming is the single best move for
[[agent-legibility]], now with a cited LLM-code-understanding result. Extends
[[tornhill-clear-design-principles-agentic-age|CLEAR]]'s *Explicit intent* and *Local reasoning*.
Caveat: explicitly an opinion piece; supporting studies cited second-hand; summary-only capture.

## Touches

[[adam-tornhill]] · [[ai-readable-code]] · [[agent-legibility]] · [[agentic-coding]] ·
[[tornhill-ai-readable-code-series]] · [[locality-of-reference]]

_Source: `raw/notes/tornhill-opinionated-guide-to-naming.md`._
