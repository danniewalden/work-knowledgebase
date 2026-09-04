---
source_url: https://www.linkedin.com/feed/update/urn:li:activity:7498994893915357184/
title: "Every time I discuss archiving old events, first there's nodding, but there's always someone who says..."
author: Oskar Dudycz
publication: LinkedIn
published: 2026-08-28
retrieved: 2026-09-04
type: note
capture_note: LinkedIn post captured verbatim via live logged-in Chrome (the headless
  scheduled watch cannot render this feed). Author's own wording; only edit is collapsing
  LinkedIn's rendered 'hashtag\n#x' markup back to '#x'. Date derived from the relative age
  stamp at retrieval (2026-09-04 11:08 UTC), so accurate to the day, not the hour.
  source_url is the canonical per-post permalink, not the recent-activity feed.
  Part of his #EventDrivenDiary LinkedIn series; appeared in the feed as a self-repost, so
  the original may predate 2026-08-28 - treat the date as the repost date, not necessarily
  first publication. PRACTITIONER GUIDANCE from client work, not measurement.
---

Every time I discuss archiving old events, first there's nodding, but there's always someone who says:

"Hey, but I have the legal obligations to allow certain modifications within 5 years of removal"

Or

"Normally, it's impossible to do anything in this process, but there are rare cases where someone can perform some action even after several years"

And of course, such cases can happen, for example:
- we may want to verify the cashier shift report and add corrections if, for example, cash was wrongly calculated.
- generate the invoice correction if the initial one had wrong data.
- retrofit data that we got with a delay. Also some, entities just have a longer lifetime.

Event stores usually scale well with the number of streams. If they're not actively accessed and are not long, then it's okay to keep them. Of course, as long as we have enough storage on disk.

We can consider keeping the streams with a longer lifetime or delaying their archiving using a multi-stream approach. It's worth noting that you don't need to have a uniform archiving strategy for all. We can select different ones case by case.

And again, for such cases keeping streams short and summary events (so stuff we discussed in previous chapters of #EventDrivenDiary).

We can slice our streams per lifetime (e.g. bank account to accounting period, point of sales to cashier shifts etc.). We could even keep just the last summary event, archive the rest.

Thanks to that we can keep only single event instead of multiple ones, and if we need to reopen or perform additional action, then we start from the summary event instead of the full history.

So our event storage stops growing infinitely, which is a common concern for people starting with Event Sourcing.
