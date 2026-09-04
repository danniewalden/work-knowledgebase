---
source_url: https://www.linkedin.com/in/ricofritzsche/recent-activity/all/
title: "Some architectural ideas become untouchable — the real concern is the domain capability, not horizontal layers"
author: Rico Fritzsche
publication: LinkedIn (post)
published: 2026-06-28
retrieved: 2026-06-29
type: note
---

(Verbatim capture of a Rico Fritzsche LinkedIn post, ~1d old when retrieved on
2026-06-29, pulled via logged-in Chrome. A fuller article is linked in his
first comment — NOT captured here. Restates/extends his capability-over-layers
and Functional Core/Imperative Shell theses; see also [[autonomous-domain-capabilities]],
[[rico-fritzsche-rpu-reactor-vocabulary]], [[fritzsche-functional-core-imperative-shell-agentic-coding]].)

It's fascinating how some architectural ideas become almost untouchable. The more diagrams are shared, the less often their assumptions are questioned. This was my reaction when I saw another Clean Architecture graphic circulating yesterday.

I believe the real problem is much deeper than repositories, ports, or dependency arrows. Dependency Inversion changes the direction of dependencies but does not remove the functional dependencies inside the behavior. Separation of Concerns is not achieved by horizontal technical layers; the real concern is the domain capability.

CRUD is not domain language. Domain experts think in processes, flows, decisions, and state transitions, and not in database operations such as Create, Read, Update, and Delete. Finally, the Functional Core / Imperative Shell approach keeps behavior independent from side effects and provides a much stronger foundation for coherent domain capabilities.

Some of my thoughts were inspired by Ralf Westphal's excellent work on functional dependencies, combined with my own experience building backend systems over the past three decades.

👉 Article link in first comment.

If you disagree, I would genuinely like to hear why.

Note about the post image: Dependency Inversion keeps concrete infrastructure outside the domain, but it only replaces a concrete dependency with an abstract one. The business logic still depends on I/O.
