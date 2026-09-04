---
title: "Dilger — Slice-based architecture is not really about slices (the Element/Slice/Chapter/Story/Context ladder)"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [dilger-element-slice-chapter-story-context-ladder]
raw_file: [raw/notes/dilger-element-slice-chapter-story-context-ladder.md]
tags: [event-modeling, slice, method, vocabulary, focus]
---

# Dilger — Slice-based architecture is not really about slices

LinkedIn post by **[[martin-dilger]]**, 2026-08-25. Raw capture:
`raw/notes/dilger-element-slice-chapter-story-context-ladder.md`. Ends with a promotion for his AI
adoption consulting.

**A real method extension, and the keystone of the [[slice]] page.** It names the zoom levels above the
slice, which the KB had been using informally for months without definition.

## The ladder

> "Slice-based architecture is not really about slices. Same as Event Sourcing is not really about
> Events. People struggle with this one a lot. They hear slice, they learn to draw one, and they think
> that's the whole method."

- **Element** — a card on the board. *(Named but not defined in the post.)*
- **Slice** — "just the smallest building block you can model. Nothing more." Every slice either writes
  (via a command) or reads (via a read model).
- **Chapter** — grouped slices: "a consistent part of a business process or a customer journey."
- **Story** — chapters connected in the right order: "the whole flow from start to end."
- **Context** — many stories on a board, "describing a complete system."

> "Element. Slice. Chapter. Story. Context. That's the ladder, and a slice only sits on the bottom rung."

## The diagnosis

> "Most teams get stuck right there. They model slice after slice and never climb up to see the story,
> let alone the context around it… You need the tiny building blocks, but also the big picture to be
> effective."

He pitches zooming as a **tooling** problem — "best done automatically" — which is consistent with his
Excel-grid design bet ([[dilger-planning-like-excel-legible-to-human-and-ai]]): a coordinate system is
what makes zoom levels navigable rather than notional.

## Why it matters here

- It supplies the vocabulary for [[slice]], written the same day, and retro-fits definitions to
  "chapter" and "story" — terms already used across a dozen pages, including in the self-training
  agent's own learned rules ("Are Chapters laid out the same way?",
  [[dilger-one-million-tokens-self-training-modeling-agent]]).
- **Context** is the rung that connects the method to [[domain-driven-design]]'s bounded context. He
  does not make that link explicit, and the wiki should not assume the two are identical — but the
  correspondence is close enough to be worth testing.
- The "not really about slices" framing is a corrective to the KB's own emphasis: nearly every
  agent-facing claim here is slice-level, which is exactly the bottom rung he says teams get stuck on.

## Caveats

- Short, assertive, marketing-adjacent; no worked example of a chapter or story boundary.
- **No rule for where a chapter ends.** "A consistent part of a business process" is a judgement call,
  and the post offers no test for distinguishing a chapter from an arbitrary grouping.

## Related

[[slice]] · [[event-modeling]] · [[martin-dilger]] · [[triplet-architecture]] ·
[[vertical-slice-architecture]] · [[domain-driven-design]] · [[eventmodelers-ai]]
