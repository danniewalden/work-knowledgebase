---
title: "Source: Fowler — Paracelsus Maxim"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [fowler-paracelsus-maxim]
raw_file: [raw/articles/fowler-paracelsus-maxim.md]
tags: [vocabulary, off-thread, short]
---

# Source: Fowler — Paracelsus Maxim

A short bliki dictionary entry by **[[martin-fowler]]**, 2026-09-02. Raw capture:
`raw/articles/fowler-paracelsus-maxim.md`. **Deliberately short page: this is a ~240-word vocabulary
entry with no connection to the KB's threads. It is recorded so the capture is not left un-ingested.**

## Summary

Fowler names a maxim he uses: **"The difference between a medicine and a poison is dosage."** After
Paracelsus — *"All things are poison, and nothing is without poison; the dosage alone makes it so a thing
is not a poison"* — the point being that arguments about practices being "good" or "bad" usually miss two
variables. His example: *"A little global data, especially when immutable, can be a handy way of
propagating information that may [be] needed anywhere in a program, but it quickly becomes dangerous if
there is a lot of it about."* The whole entry reduces to one instruction:

> "So when thinking about when things are good or bad, we should always ask **'in what contexts' and 'in
> what doses'?**"

## Key points

- The only durable content is that **question pair**, and it is a thinking habit rather than a claim. It
  has no dependencies, no evidence, and nothing to verify.
- Where it could earn its keep in this KB is as a phrasing for something several pages already do
  informally — the *dose* variable in practices this wiki treats as binary. Candidates: how much AGENTS.md
  guidance before it becomes noise ([[context-engineering]]); how many automated checks before "number of
  checks ≠ quality" bites ([[feedforward-and-feedback-controls]]); how much autonomy per rung
  ([[autonomy-ladder]]); how many parallel agents ([[multi-agent-orchestration]]). None of those pages
  needs this vocabulary to make its point.

## Limits

- **A dictionary entry, not an argument.** No evidence, no case, no application to AI or agents anywhere
  in it. Fowler is naming a rhetorical move.
- **Nothing in it is about this KB's subject matter.** The dosage idea is generic to any practice
  discussion.

## Connections / contrast

Off-thread. My recommendation to the curator: **drop, or keep only as a phrase**. If it is kept, its
entire value is one sentence to reuse ("in what contexts, and in what doses") — which is a *style* note,
not knowledge, and the wiki does not currently have a home for style notes. It should not become a concept
page.

## Related

[[martin-fowler]] · [[feedforward-and-feedback-controls]] · [[autonomy-ladder]] ·
[[context-engineering]]
