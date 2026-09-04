---
source_url: https://www.linkedin.com/feed/update/urn:li:activity:7496661019960774656/
title: "Vertical Slice Architecture (VSA) does not fix entity-centered thinking."
author: Rico Fritzsche
publication: LinkedIn
published: 2026-08-28
retrieved: 2026-09-04
type: note
capture_note: LinkedIn post captured verbatim via live logged-in Chrome (the headless
  scheduled watch cannot render this feed). Author's own wording; only edit is collapsing
  LinkedIn's rendered 'hashtag\n#x' markup back to '#x'. Date derived from the relative age
  stamp at retrieval (2026-09-04 11:08 UTC), so accurate to the day, not the hour.
  source_url is the canonical per-post permalink, not the recent-activity feed.
  This is the LinkedIn statement of the VSA-ownership argument the 2026-09-04 sweep flagged
  as a Medium-only gap on the VSA x capability-ownership axis. It links a fuller article in
  the first comment (comment link not resolved at capture time). PRACTITIONER ARGUMENT, not
  measurement - the "test your design" list is a heuristic he proposes, not a study.
---

Vertical Slice Architecture (VSA) does not fix entity-centered thinking.

You can place the endpoint, handler, persistence code, and tests in one folder and still organize the business around database lifecycles.

When top-level folders are nouns and the requests beneath them are Create, Get, Update, and Delete, the code is organized vertically. Starting with the record that changes makes the entity lifecycle the use-case boundary.

That is an ownership problem.

VSA improves locality after a team chooses a request boundary. It does not discover that boundary. A CRUD-shaped request remains CRUD-shaped inside its own slice.

The boundary should follow what happens in the business and the language used to describe it. Each business operation becomes the unit of change. Domain experts talk about allocating an order, approving credit, admitting a patient, or settling a claim. Database operations belong to the implementation vocabulary.

Test your design:
- List the business changes a generic update accepts.
- Count how many slices depend on the shared entity model.
- Change one business rule and observe what else must move.

An entity-centered, CRUD-shaped Clean Architecture implementation has the same issue. Horizontal layers and vertical slices arrange code differently. Both preserve the same ownership problem when entity lifecycles determine the use cases.

I linked my full article in the first comment.

#softwarearchitecture #verticalslices #vsa
