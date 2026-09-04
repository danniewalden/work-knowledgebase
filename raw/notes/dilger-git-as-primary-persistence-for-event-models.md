---
source_url: https://www.linkedin.com/feed/update/urn:li:activity:7500799427670884352/
title: "Full Git-Versioning for Event Models"
author: Martin Dilger
publication: LinkedIn
published: 2026-09-02
retrieved: 2026-09-04
type: note
capture_note: LinkedIn post captured verbatim via live logged-in Chrome (the headless
  scheduled watch cannot render this feed). Body is the author's own wording; the only
  edit is collapsing LinkedIn's rendered 'hashtag\n#x' markup back to '#x'. Post date
  derived from LinkedIn's relative age stamp at retrieval (2026-09-04 11:08 UTC), so it
  is accurate to the day, not the hour. source_url is the canonical per-post permalink,
  not the recent-activity feed.
---

Full Git-Versioning for Event Models

Earlier this year I started to build EM-Studio to solve Event Modeling for the Enterprise.

It all started with Supabase-Persistence, storing all data in relational tables in a Postgres.

I wasn't too concerned about it, technically it's only one table for the source data (of course it's all event sourced)

Next Sqlite was added as a lightweight alternative.

Both are live and used heavily.

Now I'm adding the one I was looking for all the time.
Git.

That Plattform already has built-in Git Supprt, but only as an extension. Like a backup. Every change you make gets tracked and versioned.

Now I'll add Git as a primary persistence as well.
No relational database.
All data lives in Git.

I love it.

Technically it'll be one repository per board you can configure.
( and yes, branching is supported )

And of course, it's very simple to add your own datastore. The system was designed from the start for "BYODS" - bring your own datastore.
- Redis, sure why not?
- S3 - good one. Certainly possible.
- yml - well.. not my first choice, but if you want?
- Sharepoint - just to mention something really crazy.

You can store your models in a Worm-Drive for auditability.

I think this really adds some really needed flexibility.

Solving Event Modeling for the Enterprise. Using BYODS - and especially the git-backend is a big step forward.

( I added a new LinkedIn Group "Solving the hard parts of Spec Driven Development" here https://lnkd.in/eb2vK7UM - ask questions, discussions, features of EM-Studio )

#eventmodeling #emstudio
