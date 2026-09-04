---
source_url: https://www.linkedin.com/in/martindilger/recent-activity/all/
title: "Last night, I spent 1 Million+ Tokens to train my Modeling Agent"
author: Martin Dilger
publication: LinkedIn
published: 2026-08-27
retrieved: 2026-08-30
type: note
---

Last night, I spent 1 Million+ Tokens to train my Modeling Agent.

Sounds impressive, but let me explain.

The Modeling Agent in the Eventmodelers Plattform is really good and knows Event Modeling as well as me ( I taught it, soon it will teach me )

But that´s not enough. So I started an experiment.

I have lots of Event Models I consider "well crafted", following the best practices that proved to be valuable in real world projects.

Now I took a realistic set of requirements and asked the Modeling Agent to model them.

Then I compare the resulting model with all my "good" models - mainly from a structural perspective. Are Chapters laid out the same way? Are Read Models structured in a similar way? How are given / when / thens structured? Are we using the same patterns?

In each iteration, it will record subtle differences and make adjustments to the skills used.

Then it will model the same requirements again, using the adjusted skills, now comparing to the previous version and all the "good" versions. Did the model improve?

It´s mindblowing.. here are some findings.

It realized that I´m using a lot of storylines instead of plain Given / When / Thens especially for Read Models connected to Automations. So it adjusted the skills to do the same - and it made a new rule for "Todo Lists" ( which is exactly what this is about )

It realized that I use linked elements to bridge events between chapters. This was hinted to in the skills, but not clearly stated as a rule. It added this as a modeling rule.

It realized that back arrows are not allowed, but it noticed that I´m using copies of Read Models to show how a later Event affects an earlier Read Model. Now it creates a copy of the slice, links the Read Model and shows how that affects the screen.

That is a self-learning loop and it just improves itself, gets better the longer I run it.

It´s running on local hardware using QWEN3.7:27b and I´ll just keep it running now.

This is absolutely fascinating, it catches all those tiny little subleties that are really hard to explain.

---

*Capture notes: collected 2026-08-30 from Martin Dilger's LinkedIn recent-activity feed in a live logged-in Chrome session. Post timestamp read as "3d" on 2026-08-30 → published 2026-08-27. This is the loop referred to in the 2026-08-28 follow-up captured as `dilger-modeling-agent-improved-by-learning-loop`. Whitespace normalized; the author's non-ASCII apostrophes preserved as posted. No per-post permalink was extractable without tripping the browser tool's query-string filter.*
