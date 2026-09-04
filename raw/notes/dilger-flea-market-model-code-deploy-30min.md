---
source_url: https://www.linkedin.com/in/martindilger/recent-activity/all/
title: "My Wife Asked Me to Build a Registration Form for a Flea Market"
author: Martin Dilger
publication: LinkedIn
published: 2026-07-01
retrieved: 2026-07-01
type: note
---

# My Wife Asked Me to Build a Registration Form for a Flea Market.

Just recently, my wife approached me: "Can you build me a flea-market registration?"

Hold my beer. Of course I can.

I immediately opened the Eventmodelers platform. She was a bit surprised.

But we started brainstorming anyway - I didn't bother explaining what it was called.

"So why do you need it?" I asked.

"We're organizing a flea market for kids, and we need people to register."

"Great. What happens after someone registers?"

"I just need a spreadsheet with the parents' names and emails."

She understood exactly what we were doing. Not because I taught her Event Modeling - she has no idea what that is. And she doens´t care.. Just by drawing the screens as we usually do she could easily follow along..

"Just the spreadsheet?" I asked.

"No, we also collect a 5 euro fee for the tables."

"Oh, so we need a payment integration. Stripe or Copecart?" She didn´t understand..and I was already halfway to modeling it.

She gave me the look. "We collect it by hand. Like always."

Alright, alright. "So how do you track who's paid?"

"Can we just do that in the spreadsheet too?"

I drew a simple button in a screen.. wouldn´t that be better? so she could filter for people who hadn't paid yet. She didn't care much either way, so that's what we shipped.

This story is real. But here's the point.

A few things I took away from it:

- My wife didn't care about Event Modeling, or what it could theoretically do for her. And she shouldn´t.. it´s just a tool. She wanted her problem solved. That's it.
- Modeling it, building it, and deploying it took less than 30 minutes. Could Claude have done this without any modeling at all? Sure - and here, it wouldn't have mattered I guess. But the more complex a system gets, the more that planning step starts to earn its keep.
- And "Event Sourcing is complicated"? Not really. I'd use it even for something this simple. Not because it's the fancy choice, but because it's actually simpler than the alternatives once you're used to. I'm not dogmatic about the method - I just like keeping things simple, and this happens to be the simplest way I know how.

Why did it take less than 30min - because we have the proper tooling. We don´t need to setup the project, make architecture decisions or talk for days about which event store to use.. that´s already been decided before we started.

You are literally one button click away from Building..

Model => Code => Deploy => rinse repeat.

\#eventmodeling
\#eventsourcing
