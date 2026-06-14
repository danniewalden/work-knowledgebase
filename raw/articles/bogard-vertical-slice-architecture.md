---
source_url: https://www.jimmybogard.com/vertical-slice-architecture/
title: "Vertical Slice Architecture"
author: Jimmy Bogard
publication: jimmybogard.com
published: 2018-04-19
retrieved: 2026-06-14
type: article
---

# Vertical Slice Architecture

*Foundational/seed capture (origin of the term) — filed 2026-06-14 to ground the new
`vertical-slice-architecture` wiki concept after Dannie broadened the focus. Not a "new this week"
watch item.*

Many years back, we started on a new, long term project, and to start off with, we built the
architecture around an onion architecture. Within a couple of months, the cracks started to show
around this style and we moved away from that architecture and towards CQRS (before it had that name).
Along with moving to CQRS, we started building our architectures around vertical slices instead of
layers (whether flat or concentric, it's still layers). Since then, for the last 7-8 years or so,
building around vertical slice architectures for all manners of applications and systems has been our
exclusive approach and I can't imagine going back to the constraints of layered architecture
approaches.

A traditional layered/onion/clean architecture is monolithic in its approach.

The problem is this approach/architecture is really only appropriate in a minority of the typical
requests in a system. Additionally, I tend to see these architectures mock-heavy, with rigid rules
around dependency management. In practice, I've found these rules rarely useful, and you start to get
many abstractions around concepts that really shouldn't be abstracted (Controller MUST talk to a
Service that MUST use a Repository).

Instead, I want to take a tailored approach to my system, where I treat each request as a distinct use
case in how to approach its code. Because my system breaks down neatly into "command" requests and
"query" requests (GET vs POST/PUT/DELETE in HTTP-land), moving towards a vertical slice architecture
gives me CQRS out of the gate.

So what is a "Vertical Slice Architecture"? In this style, my architecture is built around distinct
requests, encapsulating and grouping all concerns from front-end to back. You take a normal "n-tier"
or hexagonal/whatever architecture and remove the gates and barriers across those layers, and couple
along the axis of change:

When adding or changing a feature in an application, I'm typically touching many different "layers" in
an application. I'm changing the user interface, adding fields to models, modifying validation, and so
on. Instead of coupling across a layer, we couple vertically along a slice. **Minimize coupling
between slices, and maximize coupling in a slice.**

With this approach, most abstractions melt away, and we don't need any kind of "shared" layer
abstractions like repositories, services, controllers. Sometimes these are still required by our tools
(like controllers or ORM units-of-work) but we keep our cross-slice logic sharing to a minimum.

With this approach, each of our vertical slices can decide for itself how to best fulfill the request.

The old Domain Logic patterns from the Patterns of Enterprise Architecture book no longer need to be
an application-wide choice. Instead, we can start simple (Transaction Script) and simply refactor to
the patterns that emerges from code smells we see in the business logic. New features only add code,
you're not changing shared code and worrying about side effects. Very liberating!

There are some downsides to this approach, however, as it does assume that your team understands code
smells and refactoring. If your team does not understand when a "service" is doing too much to push
logic to the domain, this pattern is likely not for you.

If your team does understand refactoring, and can recognize when to push complex logic into the
domain, into what DDD services *should* have been, and is familiar other Fowler/Kerievsky refactoring
techniques, you'll find this style of architecture able to scale far past the traditional
layered/concentric architectures.
