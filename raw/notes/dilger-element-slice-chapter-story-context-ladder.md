---
source_url: https://www.linkedin.com/in/martindilger/recent-activity/all/
title: "Slice-based architecture is not really about slices — the Element/Slice/Chapter/Story/Context ladder"
author: Martin Dilger
publication: LinkedIn
published: 2026-08-25
retrieved: 2026-08-26
type: note
---

Captured verbatim from Martin Dilger's LinkedIn feed via a logged-in Chrome session
(post age "1d" at retrieval on 2026-08-26). Links in the original are shortened
`lnkd.in` redirects and are elided as `[link]`.

---

Slice-based architecture is not really about slices.

Same as Event Sourcing is not really about Events.

People struggle with this one a lot. They hear slice, they learn to draw one, and they think that's the whole method.

A slice is just the smallest building block you can model. Nothing more.

Every slice either writes something (using a command), or reads something ( using a read model).

Group slices together and you get a chapter, a consistent part of a business process or a customer journey.

Connect chapters in the right order and you get a story, the whole flow from start to end.

And a full event modeling board typically contains many stories. They all together form a context. Describing a complete system typically.

Element. Slice. Chapter. Story. Context

That's the ladder, and a slice only sits on the bottom rung.

Most teams get stuck right there. They model slice after slice and never climb up to see the story, let alone the context around it.

Learn to zoom in and out - best done automatically using [link]

You need the tiny building blocks, but also the big picture to be effective.

👉 AI Adoption with a proven process. Book a call and we'll talk through the steps ([link])
