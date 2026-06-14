---
source_url: https://www.linkedin.com/feed/update/urn:li:activity:7470400125186691074/
title: "Keep your Command Handlers pure (not even Claude understands this)"
author: Martin Dilger
publication: LinkedIn
published: 2026-06-10
retrieved: 2026-06-13
type: article
---

# Keep your Command Handlers pure (not even Claude understands this)

**Martin Dilger** — *LinkedIn feed post, 3d ago (edited)*

---

Keep your Command Handlers pure. (Not even Claude understands this, though.)

What does this even mean?
It means that business decisions happen in one place, with explicit inputs and deterministic outcomes.

Understandable. Readable. Testable.

Just a few days ago, I had a small dispute with Claude Code.

After being assigned a slice, it moaned:
"The existing tests are unit tests on the Command Handler - the new check lives in routes.ts, so I need a route/integration test. Let me see how other route tests are structured in this project."

Wait a second.

There is so much to unpack in that one sentence.

Claude saw a business rule and immediately looked for the nearest place to implement it. That happened to be the routing layer.

LLMs don't understand architecture. They recognize patterns.
If your architecture allows logic in five different places, they will happily put it in any of those five places. Sometimes they'll even invent a sixth.

That's why guardrails matter.
In this case, Claude completely ignored the Event Model and the Scenarios and tried to put logic into the routing layer to enforce that users can only own a single organization.

The details don't really matter.

Once the rule lives in the routing layer, you suddenly need route tests.
And Claude would happily have generated some.

But that is treating the symptom, not the cause.

The business decision never belonged there in the first place.

So, with all the patience I could bring up, I reminded it again that we keep our Command Handlers pure. (It's literally stated in the Skill. You did read it, did you?)

The routing layer has exactly one job: collect data.

It should contain no business logic whatsoever.

Instead, pass all information required for the decision through the command.

The command is your DTO. Use it.
Make Command Handlers pure.
Push every business decision into them.
Pass all required information through the command.
Keep controllers, routes, and transports dumb.
Then humans and AI have exactly one place where business logic can live.
And make sure that place is visible in your Event Model.

( and yes, in this case there is a potential concurrency issue you need to be aware of )

#eventmodeling #eventsourcing
