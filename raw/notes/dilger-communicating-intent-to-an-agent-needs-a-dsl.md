---
source_url: https://www.linkedin.com/feed/update/urn:li:activity:7501375085392379904/
title: "how to communicate your intent to an agent.."
author: Martin Dilger
publication: LinkedIn
published: 2026-09-03
retrieved: 2026-09-04
type: note
capture_note: LinkedIn post captured verbatim via live logged-in Chrome (the headless
  scheduled watch cannot render this feed). Body is the author's own wording; the only
  edit is collapsing LinkedIn's rendered 'hashtag\n#x' markup back to '#x'. Post date
  derived from LinkedIn's relative age stamp at retrieval (2026-09-04 11:08 UTC), so it
  is accurate to the day, not the hour. source_url is the canonical per-post permalink,
  not the recent-activity feed.
---

how to communicate your intent to an agent..

somehow the software industry has chosen raw markdown as the medium of choice to do that.

I'm not a fan of this. Raw markdown is suboptimal for anything beyond a project kickoff.

Requirements need to be:
- specific
- unamiguous
- information complete
- structured

Just writing some markdown files doesn't solve any of the problems we faced in the past.

What used to be a Jira Ticket became Markdown Files.
Same old stuff, some new paint.

What's missing is a DSL to unambiguously describe flow, behavior + business rules.

The medium ifself - nobody cares in the end ( you can export Json, Markdown, Toon.. from my tools )

There are several attempts to stanardize how to describe behavior.

For me, Eventmodeling is that DSL. Battle-tested over hundreds of projects by many companies.

I documented the standard Json-Format in 2024 ( https://lnkd.in/e4FEdAz3 ) and all my workflows use it internally.

How do you structure your Agent Instructions?
