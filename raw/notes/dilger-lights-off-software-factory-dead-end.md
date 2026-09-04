---
source_url: https://www.linkedin.com/in/martindilger/recent-activity/all/
title: "The lights-off software factory is a dead end, if you ask me."
author: Martin Dilger
publication: LinkedIn (post)
published: 2026-08-16
retrieved: 2026-08-17
type: note
---

The lights-off software factory is a dead end, if you ask me.

lights-off is generally used to describe a software process where the code remains in the dark. No one reads it, no one reviews it - no one but agents.

Every single team I know who went down that route circled back.

I don´t practice it either, even though I´m all in on agentic engineering.

This works until it doesn´t. Typically it becomes apparent after some production incident. It´s fun trying to solve an issue, with production burning and no one there to navigate the code base ( as no one has ever seen it )

So you can´t do full code reviews - it´ll not be sustainable with the increased output - you just moved the bottleneck. But you can´t do no code-reviews either it seems. So what to do?

I work in several layers of trust.
It starts with the Event Model - the "Spec", describing exactly what needs to be done. Including the guard rails in the form of scenarios using Given / When / Then - Semantics.

Those Scenarios are translated to executable specifications. Call it Test-First Development if you will ( as we define the tests long before any code )

If all those tests are green, I´m pretty confident it does what it should.

After the implementation we have static checks
- were any tests adjusted ( requires review )
- are there any tests outside of the specification ( requires review )
- were files changed outside of the SUD ( Slice under development ) ( immediate fail )
- were dependencies changed? ( requires review )

Then typically we have the manual review:
This is not a functional review - at this point we already know it works. I look at the structure, does it match my mental map? This doesn´t take longer than 2-3 minutes.

Any of those guards can fail an implementation. Almost always, this means we throw away everything, record a learning "why" this was not good enough and start from scratch ( my moving the Slice back into "planned" )

This short human review has several benefits:
- I keep connected to the code base. It allows me to keep a map of it in my head. If something goes wrong, I roughly know where to look.
- you can capture structural problems with several quickly processed quality gates. The review bottle-neck doesn´t exists here.

I trust the process. I don´t care too much "how" a slice is implemented internally, as any bad implementation can be easily replaced. I do care a lot about the overall structure of the system and the shape of the persisted data ( our Events ). If that is broken, we got a serious issue - anything else can be easily fixed.

This allows to build flexible and evolvable architectures that can cope with any requirement.

So it´s not one step that makes this work, it´s the whole process I typically call the Triple-Architecture.
- Spec Driven Development using Event Modeling
- Structure using Slices
- Implementation using Event Sourcing

How do you work around the Review-Bottle-Neck?

#eventmodeling #eventsoucing #tripletarchitecture

---

*Capture note (not part of the source): post carried 13 reactions and 1 comment at time of capture. Hashtags reproduced as written (including the author's "#eventsoucing" typo). URLs in the post body, if any, were not present.*
