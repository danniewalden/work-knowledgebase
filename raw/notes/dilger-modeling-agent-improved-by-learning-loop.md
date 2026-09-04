---
source_url: https://www.linkedin.com/in/martindilger/recent-activity/all/
title: "The Event Modeling Agent improved significantly — what the learning loop taught it"
author: Martin Dilger
publication: LinkedIn
published: 2026-08-28
retrieved: 2026-08-30
type: note
---

The Event Modeling Agent in the Eventmodelers Plattform improved significantly over the last few days. this is due to a learning loop described here: [lnkd.in link]

Some insights:

It properly models translations ( and knows when to use them)

it handles TODO Lists well, and knows how to specify their behavior using storylines.

It learned to break down screens into functional blocks, copies the screens and marks different areas, using dedicated read models. (this allows to generate the UI much more easily)

It actively prevents back arrows by using Read Model and Screen copies showing the updated state along the timeline.

One thing that interesting, ever 5th iteration or so is really bad, making stupid modeling mistakes, skipping steps.. digging into the reasoning, it's always the model taking shortcuts when it reaches certain budget thresholds. Most models are obviously trained to make the best with the budget they have, actively taking shortcuts when budgets get depleted, to deliver at least something.

I'll incorporate this in the learning loop, let's see how it'll improve itself on that.

all in all that's been some truly astonishing learnings. fascinating to watch a model improve itself.

test it yourself by simply following the steps outlined here: [lnkd.in link]

just give it your business requirements - pdfs, excel sheets, confluence pages and let it model

---

*Capture notes: collected 2026-08-30 from Martin Dilger's LinkedIn recent-activity feed in a live logged-in Chrome session. Post timestamp read as "2d" on 2026-08-30 → published 2026-08-28. Direct follow-up to the 2026-08-27 post captured as `dilger-one-million-tokens-self-training-modeling-agent`, which describes the learning loop itself. Whitespace normalized; emitted URLs replaced with placeholders (two `lnkd.in` shortlinks, unresolved this run). No per-post permalink was extractable without tripping the browser tool's query-string filter.*
