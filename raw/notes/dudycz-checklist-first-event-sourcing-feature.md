---
source_url: https://www.linkedin.com/feed/update/urn:li:activity:7500256800592588800/
title: "How to start with #EventSourcing? How to pick a first feature for it?"
author: Oskar Dudycz
publication: LinkedIn
published: 2026-09-01
retrieved: 2026-09-04
type: note
capture_note: LinkedIn post captured verbatim via live logged-in Chrome (the headless
  scheduled watch cannot render this feed). Author's own wording; only edit is collapsing
  LinkedIn's rendered 'hashtag\n#x' markup back to '#x'. Date derived from the relative age
  stamp at retrieval (2026-09-04 11:08 UTC), so accurate to the day, not the hour.
  source_url is the canonical per-post permalink, not the recent-activity feed.
  Part of his #EventDrivenDiary LinkedIn series. PRACTITIONER HEURISTIC - a 14-question
  checklist he proposes, and he explicitly disclaims it ("this checklist lacks the depth
  and nuance... that's why I don't like checklists"). Not a validated instrument. Links a
  fuller article.
---

How to start with #EventSourcing? How to pick a first feature for it? I've been answering that so many times, that I'm surprised I haven't yet written about it explicitly.

I heard that you all love checklist, so here it is for asking yourselves if the feature is the right choice.

1. Who owns the process lifecycle?
2. Do we produce our own events, or only consume other people's?
3. Can a command be rejected for a business reason?
4. Is the decision a business rule or a retry policy?
5. Could we run an EventStorming session on it with a non-technical colleague?
6. Does the stream end?
7. Is it off the critical path?
8. What happens if it's wrong for a day?
9. Could we walk it back in a week?
10. Is it small enough to do slightly rogue?
11. Can the event store we choose run on storage we already operate?
12. Does it fit inside a single module?
13. Is any part of it asynchronous?
14. Is it real?

And if this checklist lacks the depth and nuance for you, then I agree; that's why I don't like checklists! And hey, are you looking for nuance and in-depth analysis on LinkedIn? Sweet summer child!

Jokes aside, guess what? I've got nuances for you in my new article!

What would you add to this (check)list? Or maybe you disagree with it?

Read it here https://lnkd.in/dAurDQ4B

#EventDrivenDiary
