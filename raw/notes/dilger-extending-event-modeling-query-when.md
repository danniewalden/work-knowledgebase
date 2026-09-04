---
source_url: https://www.linkedin.com/in/martindilger/recent-activity/all/
title: "Extending Event Modeling: an optional 'Query' (WHEN) on the read side"
author: Martin Dilger
publication: LinkedIn
published: 2026-06-29
retrieved: 2026-06-30
type: note
---

(LinkedIn post, ~20h before retrieval. Apostrophes reconstructed from a live-Chrome
text scrape; a promotional course link at the end was elided as [link].)

The first time I'm extending Event Modeling..

While writing my book "Understanding Eventsourcing" - I made sure to completely
stick to Event Modeling "Standard" - not reinventing anything, not adding new
elements... just using what was defined.

Same for the Event Modelers Plattform - probably the platform that is the closest
to the Event Modeling "Standard" - if you read the book or the original article by
Adam Dymitruk, you should feel at home immediately - colors, elements, everything..

I'm all for simplicity - what is not strictly required can be left out. Now I'm
deviating for the first time from this, I'm adding something, but not
lightheartedly..

After discussions at the Event Modeling Conference in munich, it was clear that
something was missing. It came up in several discussions by independent people.

The possibility to express complex queries in Scenarios..

And by accident, I had discussed the same with Adam Dymitruk before as well. I
wouldn't add this myself - I'm seeking feedback from everybody.

Let me explain what changes:

We typically work with Given / When / Thens to express behavior / business rules..

GIVEN - a user was registered
WHEN - the user tried to register again
THEN - error - users can only register once.

same for the read side - I taught people for years to just leave out the WHEN part..

GIVEN - a user was registered
THEN - we expect this data to be available..

But now we are adding optional WHEN named "Query"

GIVEN - a user was registered
WHEN - we query with the users email-address
THEN - we expect the user to be returned...

It's available on [the platform] - feedback is already positive, seems many people
have been waiting for this.

( and btw. I noted down every single feedback I got from the participants of the
Event Modeling Conference, and every single one has been addressed.. I take this
serious )

This will also be used in the new Section of the Online Course "Implementing [link]
