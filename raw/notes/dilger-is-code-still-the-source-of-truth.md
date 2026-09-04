---
source_url: https://www.linkedin.com/in/martindilger/recent-activity/all/
title: "Is Code still the source of truth?"
author: Martin Dilger
publication: LinkedIn (post)
published: 2026-06-16
retrieved: 2026-06-17
type: note
---

> Captured verbatim from Martin Dilger's LinkedIn post (1d old at retrieval).

Is Code still the source of truth?

Yesterday Sam Hatoum asked this question, and by chance I have been discussing this for months - also at Craft Conf in Budapest a few weeks ago.

Let me start with a definition, because this debate goes nowhere without one.

Source of truth - to me - means: if someone wants to understand how a piece of functionality works, where shall they go?

There's a bug in production. You open the codebase and find a coupled mixture of Italian meals. Spaghetti. Lasagna. Some Gnocchi sprinkled through the system.

Logs are missing.
Monitoring isn't there.
The code technically exists, but it reveals nothing.

If Code is the source of truth, and your system starts to rot. What does that mean?

So what does the team do? They find the one person who just knows. In that moment, that person becomes the source of truth. Not the code.

What happens when that person leaves? The knowledge disappears. Code over time buries its original intention until it's gone.

There are actually two separate things here:
The intent - what we need the system to do
The actual thing - what the code does

In most teams I've worked with, intent lives nowhere. It's in a closed Jira ticket. A Confluence page nobody has opened in two years. In the head of a product manager who left before anyone thought to ask them.

When intent is lost, you can't even verify the system is still doing what it was supposed to do. You're just hoping.

Here is my opinionated take - code is a lagging indicator.

It's the result of intent, never the origin. Requirements change and code adapts - but it's always chasing the intent, never leading it.
AI made this impossible to ignore.

If AI generates code from a specification:

- The specification becomes the source of intent
- Code is just the output - one implementation of it
- Where code and model diverge, AI can detect the drift and adapt

Code becomes almost disposable. One expression of the model, regeneratable on demand.

The source of truth is the intent. The model. The specification that captures what the system is supposed to do and why. Code follows the model. It always did.

It depends on your definition - but mine hasn't changed. Code never really was.

#eventmodeling
