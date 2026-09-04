---
source_url: https://www.linkedin.com/feed/update/urn:li:activity:7500918538543517696/
title: "Here's my agentic code-review skill for Claude Code, Codex & friends"
author: Addy Osmani
publication: LinkedIn
published: 2026-08-28
retrieved: 2026-09-04
type: note
capture_note: LinkedIn post captured verbatim via live logged-in Chrome (the headless
  scheduled watch cannot render this feed). Author's own wording; only edit is collapsing
  LinkedIn's rendered 'hashtag\n#x' markup back to '#x'. Date derived from the relative age
  stamp at retrieval (2026-09-04 11:08 UTC), so accurate to the day, not the hour.
  source_url is the canonical per-post permalink, not the recent-activity feed.
  Surfaced in the feed as a SELF-REPOST: LinkedIn's age stamp ("1w") is the ORIGINAL post's
  age, so 2026-08-28 is the original date; the repost that put it in the window is ~09-02.
  AUTHOR'S OWN TOOL - he is describing a skill pack he publishes (addyosmani/agent-skills),
  so the claims about what it does are self-report about his own artefact, with no
  evaluation, benchmark or comparison against other review skills.
---

Here's my agentic code-review skill for Claude Code, Codex & friends

I've been iterating on the code review skill in my Agent Skills pack and it transforms the /review process by doing four specific things: 1. reviews on five quality axes, 2. labels findings by severity, 3. orders finding by what changes outcomes and 4. proposes the moves to address the review.

Try it out in about 30 seconds: https://lnkd.in/gmf3uZ7t

npx skills add addyosmani/agent-skills --skill code-review-and-quality
(Want the whole lifecycle pack instead? Spec through ship, just drop the --skill flag).

Reviews on five axes: Correctness, readability, architecture, security, and performance. Most automated reviews collapse to "do the tests pass?" Tests are necessary, but they don't catch a leaking module boundary.

Labels every finding by severity: "Critical" blocks the merge. No prefix means required. "Nit" and "FYI" are optional. This stops authors from treating every comment as mandatory and burning an afternoon on formatting preferences.

Leads with leverage: If there is one structural problem and ten nits, the structural problem is the review. Findings are ordered by what actually changes the outcome.

Proposes the move: Saying "This is complex" leaves the author guessing. Saying "Replace this conditional chain with a dispatcher" is a review they can act on.

The review is your quality gate. It is worth telling your agent what a good one looks like. Run /review before you merge.

If you don't end up using it or there's another code-review skill out there you like better, that's totally cool. I hope this proves useful to someone out there.

#ai #programming #softwareengineering
