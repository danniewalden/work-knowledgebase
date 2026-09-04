---
source_url: https://www.linkedin.com/in/adam-tornhill-71759b48/recent-activity/all/
title: "You just cannot trust your coding agent to produce maintainable or even machine-legible code"
author: Adam Tornhill
publication: LinkedIn (post)
published: 2026-06-22
retrieved: 2026-06-23
type: note
---

# Adam Tornhill — LinkedIn post, 2026-06-22 (~21h before retrieval)

Captured verbatim from Adam Tornhill's LinkedIn recent-activity feed via a live
logged-in Chrome session (post text only; an attached before/after refactoring
screenshot is referenced but not captured).

---

I feel like a repetitive canary in the coal mine, but this needs to be said again: you just cannot trust your coding agent to produce maintainable or even machine-legible code.

I ran into this again today when preparing an agentic refactoring workshop. The existing code was in poor shape, and I told my agent to fix a specific code health issue. You see the result in the attached screenshot.

A software design disaster where one problem was traded for an even worse one.

No, it's not enough to ask an agent to "follow the SOLID principles", "write clean code", or even have another LLM review the code. You'd spend a ton of tokens and still get the same subpar code:

* LLMs are non-deterministic. Code quality is too important to leave to chance.
* An LLM has no reliable way of assessing code health.
* Your existing code is a large part of the context. This means agents perform particularly poorly where they are needed the most: in complex and unstructured code.

The good news is that this problem is already solved. I use deterministic Code Health feedback through the CodeScene MCP in my coding workflow, giving the agent an external source of truth rather than asking it to judge its own output.

I keep pressing this issue because I see plenty of companies on the highway to legacy code. Some code health issues won't hurt you now. The code might even work. But those sins accumulate quickly, leading to a downward spiral where neither you — nor your agent — can easily evolve the code.

As someone who codes 100% agentic — and has been doing that for nine months — I'm surprised that so many developers ignore this aspect. It's strikingly obvious the moment you do anything beyond a toy project.
