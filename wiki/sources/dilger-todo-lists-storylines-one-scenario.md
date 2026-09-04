---
title: "Dilger — Mastering TODO Lists in Event Modeling (Storylines)"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [dilger-todo-lists-storylines-one-scenario]
raw_file: [raw/notes/dilger-todo-lists-storylines-one-scenario.md]
tags: [event-modeling, given-when-then, specifications, method, focus]
---

# Dilger — Mastering TODO Lists in Event Modeling (Storylines)

LinkedIn post by **[[martin-dilger]]**, 2026-08-15. Raw capture:
`raw/notes/dilger-todo-lists-storylines-one-scenario.md` (204 words). A carousel/document attachment
accompanied the post and was not transcribed.

## What it says

A **TODO list** in [[event-modeling]] is structurally trivial — "just a queue of things to do
essentially" — and Dilger admits he no longer remembers why he found it hard. The difficulty was never
the structure; it was **describing the behavior in a way that is easy for human and AI alike to
understand**.

The method move: instead of writing several [[given-when-then]] scenarios for a TODO list, **use one
scenario to describe it all** — "much more compact." He originally called these **Vertical Specs**
(they're laid out vertically below a slice), found the name confused people, and renamed them
**Storylines**: "examples that tell a story."

The feature shipped on [[eventmodelers-ai]] the day of the post — "available since today" dates the
Storylines release to **2026-08-15**.

## Why it's in this batch

It belongs with the self-training-agent pair because **the learning loop independently rediscovered it**.
Grading its own output against Dilger's hand-crafted models, the agent noticed — in his words — that
"I´m using a lot of storylines instead of plain Given / When / Thens especially for Read Models
connected to Automations," adjusted its skills to match, and "made a new rule for 'Todo Lists'"
([[dilger-one-million-tokens-self-training-modeling-agent]]). The follow-up confirms the agent now
"handles TODO Lists well, and knows how to specify their behavior using storylines"
([[dilger-modeling-agent-improved-by-learning-loop]]).

That convergence is the reason to read the three together: a convention the author had written up
*separately and in prose* was recovered *from the artifacts* by a structural diff. It is a small but
clean demonstration that the good-model corpus carries method knowledge the skill files did not.

## On the method itself

Storylines are a **compaction** of GWT, not a replacement: one narrative scenario standing in for several
discrete ones where the discrete ones would repeat most of their setup. The tradeoff is the usual one for
narrative specs — compactness against per-case addressability — and Dilger does not discuss it. Worth
noting that the naming history ("Vertical Specs" → "Storylines") is itself an
[[ubiquitous-language]]-in-practice episode: the term changed because the audience misread it, not
because the concept did.

## Caveats

- Very short, vendor-authored, and announcing a feature on the author's own platform.
- The attachment carrying the worked examples was not captured, so the *shape* of a Storyline is
  described here only in prose.

## Related

[[martin-dilger]] · [[eventmodelers-ai]] · [[given-when-then]] · [[event-modeling]] ·
[[dilger-one-million-tokens-self-training-modeling-agent]] ·
[[dilger-modeling-agent-improved-by-learning-loop]] · [[slice]]
