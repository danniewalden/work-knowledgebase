---
source_url: https://www.linkedin.com/in/ricofritzsche/recent-activity/all/
title: "AI coding agents expose the missing home for domain capabilities — Autonomous Domain Capabilities & Command Context Consistency"
author: Rico Fritzsche
publication: LinkedIn (post)
published: 2026-06-08
retrieved: 2026-06-15
type: note
---

(LinkedIn post, ~1 week old as of retrieval. Captured via live logged-in Chrome. A "Full article on Medium" is linked in the first comment — not captured here.)

Today, AI coding agents make it easy to generate and change code at a speed that felt unrealistic only a few years ago. That speed exposes an old structural weakness, because many approaches still do not give a domain capability a clear home.

In horizontal layered approaches such as Clean Architecture and Hexagonal Architecture, a single domain capability is still split across technical ownership boundaries. Request handling, application layer, repositories, mappings, and shared domain structures all participate in one capability. Repositories are especially problematic because they tend to become shared access points for many unrelated capabilities. The behavior is not local. It has to be reconstructed from the architecture.

Vertical Slice Architecture improves this by making interactions visible. Commands and Queries become explicit, and the code moves closer to the request being processed. But the deeper ownership problem remains when the handler still depends on shared domain models, shared repositories, or aggregate structures underneath. The slice becomes a local entry point into a larger shared structure instead of becoming the place where the capability fully owns its processing.

That raised the question for me:
If software is used through Commands and Queries, why attach those interactions to a centralized object model?

A Command does not need to be routed into a shared object model before it can mean something. It can define the facts it needs, build a local context from those facts, make a decision, and produce consequences. A Query can do the same for reading: define the facts it needs, derive a projection, and return a result.

That is the idea behind Autonomous Domain Capabilities and Command Context Consistency (CCC).

Recorded facts provide the Application State, but they are not the domain by themselves. The domain becomes visible through the capabilities that interpret those facts and produce new ones. Each capability is realized by a Request Processing Unit (RPU), which builds its own context, makes its own decision, and keeps behavior local.

The domain is not a centralized object structure. The domain is the combination of recorded state and the capabilities that know how to work with it.

The result is a structure where behavior, ownership, and change stay local to the capability.

→ Full article on Medium (link in first comment)

[Accompanying diagram: "Domain Capabilities" — an outer ring of "RPU" (Request Processing Unit) units surrounding a central "Application State (Recorded Events)" core, labelled "Domain".]
