---
source_url: https://www.linkedin.com/in/ricofritzsche/recent-activity/all/
title: "Microservices are not a maturity level — they are an architectural decision with a cost and a purpose"
author: Rico Fritzsche
publication: LinkedIn (post)
published: 2026-06-24
retrieved: 2026-06-29
type: note
---

(Verbatim capture of a Rico Fritzsche LinkedIn post, ~5d old when retrieved on
2026-06-29, pulled via logged-in Chrome. Points back to a critical article he
wrote in 2023, linked in his first comment — NOT captured here. Hashtags
#microservices #softwarearchitecture #modularmonolith.)

Microservices are one of those topics that still trigger very theoretical discussions.

The idea that teams must first learn to build a good modular monolith before they can build microservices keeps coming up. Anton Martyniuk, for instance, propagates this idea.

I think that frames the whole question in the wrong way.

Microservices are not the next maturity level in software development.
They are not a reward for experienced teams.
And they are certainly not something to adopt because other companies do it.

They are an architectural decision with a concrete cost and a concrete purpose.

That decision only makes sense when there is a valid reason behind it. Independent deployment can be such a reason. Different scaling characteristics can be such a reason. Strong business boundaries can be such a reason. Organizational autonomy can be such a reason.

And that last point is often underestimated.

Microservices are a good choice only when a team really owns a service end to end. That ownership includes responsibility for change, operation, failures, and the consequences of decisions. If that ownership does not exist, the result is often an organizational mess rather than technical autonomy.

The discussion is much bigger than technology, because it's about boundaries, domain knowledge, responsibility and how an organization actually works.

A modular monolith can absolutely be the right choice. It can be cheaper to change boundaries inside one deployable unit. That is a very practical argument.

But it is still only one possible choice.

There are also situations where starting with microservices is justified from the beginning, because the business, operational, or organizational constraints are already known. In such a case, building something else first just because a theory says teams have to "learn monoliths first" does not make much sense.

So for me, the real question is not monolith versus microservices.

The real question are:

☑️ What is the goal?
☑️ What are the boundaries?
☑️ Who owns what?
☑️ And what kind of structure can carry that responsibility in a realistic way?

I like microservices. But I am very critical of the way they are discussed and adopted.

Used for the right reasons, they can work very well. Used as a default pattern, they become expensive confusion.

I wrote a critical article about this back in 2023, and it still feels current today. Link in first comment.

#microservices #softwarearchitecture #modularmonolith
