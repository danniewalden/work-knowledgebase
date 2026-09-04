---
source_url: https://adamtornhill.substack.com/p/a-blast-from-the-past-sdd-and-the
title: "A Blast from the Past: SDD and the Illusion of Known Scope"
author: Adam Tornhill
publication: "Code for Humans and Machines (Substack)"
published: 2026-05-28
retrieved: 2026-09-04
type: article
capture_note: >-
  NOT INDEPENDENT for the alternative the piece prescribes: the author is the founder and
  CTO of CodeScene, and the closing recommendation ("intention-revealing software design,
  automated safeguards for our code and its behavior") is the problem space his own
  commercial product addresses. The critique of SDD itself is argument from personal
  career experience (MDA / Executable UML / RUP at two named-but-unnamed employers early
  in his career), not measurement — there are no figures in this piece at all. The one
  external citation is Robert Glass's requirements-explosion claim, quoted verbatim
  ("for every 10-percent increase in problem complexity, there is a 100-percent increase
  in the software solution's complexity"), which the author attributes to Glass without
  giving a specific work; treat that ratio as Glass's assertion as relayed here, not a
  measurement made or verified by Tornhill. Full text captured; one image is noted inline
  as [image: ...]. The trailing subscribe line is retained because it is part of the
  author's own sign-off copy.
---

# A Blast from the Past: SDD and the Illusion of Known Scope

One of the most fascinating aspects of the hyper-modern agentic era is the return of older attempts at taming software development. The latest trend to resurrect goes by the name of Spec-Driven Development (SDD). SDD does stand out as a revival of the belief that code is a mere artifact.

This article explores SDD through the lens of someone who lived through modelling days past. I acknowledge that "this time it might be different", so I'll focus my concerns on the flawed idea that implementation is the mere execution of a known scope. Rather, implementation is an essential part of the discovery process itself. And the further we remove ourselves from it, the harder it becomes.

## Quick recap: what is SDD?

The idea with SDD is to capture the intended behavior in a structured specification. We then let a coding agent execute the resulting tasks and generate design docs, etc., in the process.

Yet, as Birgitta Böckeler points out, SDD seems to come in several forms. It can be anything from a relatively lightweight way to drive agents to a strong form where the spec itself is the ground truth. It's the latter I'm concerned with.

The risk is that SDD becomes the latest iteration of an age-old manager dream: have your skilled seniors specify what to build, then pass it on to the seemingly simpler "implementation" while pretending that step is predictable and somehow less important. In the 1990s, "implementation" meant a team of coders kept in the dark. Today, it's obviously agents.

The process didn't work well back then. As both the pace and expectations on a software delivery are orders of magnitude higher now, I'm sceptical about how well SDD will work this time around. Not due to waterfall thinking — many SDD practitioners evolve their systems iteratively — but rather due to the nature of problem solving.

## The pull: a need for predictability

Software development is at a crossroads. The best possible outcome of the agentic revolution is that we raise the bar for software engineering. We know what's good for us: strong automated test suites, continuous delivery, small increments, modular architectures, and top-notch code quality.

We also know that GenAI is stochastic. But so too is a group of humans collaborating on software. And if history taught us anything, the solution isn't just better input but also faster feedback loops. Let me elaborate by travelling back in time to the model wars.

## The Emperor's new executable clothes

SDD is strongly reminiscent of the Model-Driven Architecture, Executable UML, and the glorious Rational Unified Process (RUP) of decades (fortunately) long gone.

Early in my career, I used these technologies at two different companies. In the first one, we had an effective design review process. As a developer, I'd basically sketch out the software design as a UML class diagram, complement it with some sequence diagrams for the dynamics, and did a walkthrough for my peers.

Yes, the process was slow. But what we designed usually worked as a direction on what to implement. The real advantage, though, was that the resulting UML diagrams served well for onboarding and extensions. It was easy enough to get the high-level view of the solution, which helped when later drilling into the code.

So far so good. Then came the tool vendors. I mean, if you've already sketched out your design, why not take it full circle and generate all code from that sketch? After all, code is just an implementation detail, right? All that was needed was to extend UML with an "action language" to capture those "details".

How well did it work in practice? Oh, the first victim was the documented design. The executable diagrams turned so bloated and verbose that they became literally incomprehensible. After all, the new audience was a compiler, not humans.

Changes and extensions got painful. You see, all those power tools we've gotten used to — build pipelines, command line utilities, IDEs, linters, etc. — didn't exist in the vendors' design tools. Imagine coding in a Microsoft Word document. That's how it felt.

[image: Model-Driven Architecture flashback showing complex diagrams]

*A Model-Driven Architecture flashback. Some scars never heal.*

## The cognitive perils of a strong spec

Tooling was only part of the model-driven fiasco. A stronger problem was the process mindset at that time. Agile was brand new, and few people were familiar with the movement outside narrow programmer circles. Virtually every company I worked with operated in waterfall mode.

However, back then, the expectations on a software delivery were quite different. Today, with daily deployments being the standard, we just cannot afford to be slow in acting on feedback.

Human problem solving is inherently iterative and driven by reflection in action. We learn by doing. Express an idea in code, test it out, observe, and learn. The cycle expands our understanding of the problem we're trying to solve. That improved understanding is then translated into modifications to the program, which we in turn observe and learn from. Rinse and repeat. We just cannot short-circuit that.

No, I don't mean that we shouldn't think things through early on. We should. And we should write stuff down to make it more concrete and invite a conversation. That helps thinking, too. But we need to treat that document as an imperfect starting point rather than the finished product.

## The most underestimated aspect of code: requirements explosion

The main challenge starts if we work from a spec as if the problem was already understood. The reason is the concept of *requirements explosion*. The term was first coined by Robert Glass. Glass argues that "for every 10-percent increase in problem complexity, there is a 100-percent increase in the software solution's complexity."

In other words, each requirement in the spec will lead to tens of implicit design requirements that need to be resolved. We cannot leave that as guesswork for an agent to figure out.

To make SDD work, we would have to provide directives that let agents resolve a large share of all those implicit requirements.

So, couldn't we complement our spec with a detailed solution model? We could. But it would lead us on a march with three major obstacles:

1. **Free text lacks precision**. Yes, we can explain constraints, etc., in text, but that becomes verbose and hard to check. Even structured prose and checklists leave room for ambiguity. That's why we have programming languages. Those are excellent at capturing precise rules intended for machines.

2. **We cannot know the solution requirements up-front**. Remember: we learn by doing. And if we don't and rather have agents make those decisions for us, it becomes orders of magnitude harder to derive and capture the solution requirements. Think reverse engineering a legacy codebase. That's the position we'd be in. Constantly.

3. **Extending requirements specs with implementation details and contracts blurs the model**: This is what hit hardest back in the MDA/UML days: the model starts to become the implementation and loses its value as an overview, a different level of abstraction. Code just needs another level of precision.

> The moment a model becomes the implementation, it ceases to be a good model.

## The other road ahead

SDD is something I'll continue to observe but sit out on for now. However, that doesn't mean I don't value structure and a certain predictability. It just means we should look for those qualities elsewhere.

Predictable progress rests on domain expertise, intention-revealing software design, automated safeguards for our code and its behavior, and rapid visual feedback, all amplified by a highly skilled team. Those capabilities are harder to grow than a spec. But they are also far more valuable. With or without SDD.

Subscribe for practical patterns, research, and reflections on coding in the agentic era.
