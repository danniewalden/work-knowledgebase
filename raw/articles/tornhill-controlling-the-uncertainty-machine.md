---
source_url: https://adamtornhill.substack.com/p/controlling-the-uncertainty-machine
title: "Controlling the Uncertainty Machine: Do You Still Need to Read AI Code?"
author: Adam Tornhill
publication: "Code for Humans and Machines (Substack)"
published: 2026-08-20
retrieved: 2026-08-26
type: article
---

# Controlling the Uncertainty Machine: Do You Still Need to Read AI Code?

*Section: AI-READABLE CODE*

**Human attention should follow uncertainty. We don't need to read all AI-generated code. But we need to make the code we do read count.**

ADAM TORNHILL — AUG 20, 2026

---

With AI coding, human attention and focus become bottlenecks. AI-first codebases have a different context and audience. As a reaction to that, we need to reconsider traditional "best practices" to reap the full benefits of coding agents.

As developers, we're used to being accountable for all code we write. Coding agents do not change that. But we need to use our time effectively, and I simply found that trying to grasp all code in detail is no longer efficient; if we approach agentic coding the way we tackle manual coding, we'll spend the majority of our time deconstructing meaning from code. It's wasteful and cognitively effortful.

That obviously doesn't mean that I no longer care about readability, code structure, or architecture. Quite the contrary. This whole blog is about maintainable code. Rather, I leverage automation and strict processes to relieve me of the code-reading burden without incurring unacceptable risks.

## Human inspection is driven by uncertainty

A question like "do we still need to read all AI generated code" is pointless in isolation. The answer depends on the task, and more specifically on the uncertainty inherent in each type of task. That is, how much of the intended solution's behavior and structure is already understood and represented in the existing system.

That task uncertainty drives both the relative autonomy I grant a coding agent, and the effort I spend reviewing the resulting code.

*[Image: Uncertainty determines how much code I inspect. The more exploratory the task, the deeper I go.]*

Consider a bug fix. Here it's usually enough to inspect the evidence for the fix. Reproduce the problem, fix it, and have the new tests pass. Since the majority of bugs are local and contextual, bug fixes rarely require novel designs or architectural changes. They are naturally constrained.

Contrast those bug-fixing tasks with the first iteration on a new feature or capability. The existing structure and patterns in a codebase are important context that guides coding agents. When doing novel work, establishing those structures is key. This requires more detailed involvement. However, it doesn't require that I read all code. Let's explore the process.

## Tests as human/agent abstraction boundaries

Understanding code we didn't write ourselves is one of the hardest parts of software engineering. If we approach agentic coding the way we tackle manual coding, we'll spend the majority of our time trying to deconstruct meaning from code. We'd effectively turn ourselves into legacy code maintainers. That's a mentally draining place to be and is unlikely to speed up anything.

So instead I've come to accept that I'll no longer know every line of code. I never read all AI-generated code. But, and this is important, make the code you do read count.

The pattern that worked for me is to focus my manual review efforts on tests. I typically instruct my agent — after the planning stage — to generate the end-to-end (e2e) tests first. I then review, and iterate on those tests together with the agent.

A strong test suite serves as a boundary between the code I do inspect and the code I give the AI autonomy to develop.

Starting with e2e tests solves the validation problem: how do I ensure that the AI generates the right code?

With the e2e tests nailed down, I typically let the agent proceed and write the code that makes them pass. I rarely spend much time looking at the actual implementation.

The possible exception is novel features that don't yet have an architectural home. Software development never was, and still isn't, a streamlined, simplistic transformation. In such cases, I do perform spot inspections of the code. But again, I don't focus on details, but rather on the overall structure and patterns to lay a strong foundation for the next iterations that can be more autonomous.

## Turn review findings into future guards

Now, before we proceed to discuss code quality, let me emphasize that I do spend a lot of time iterating on those tests. AI-generated application code is rarely optimal out of the box. But it's usually decent. The test code? Not so much. So it pays off to run those extra test refactorings.

My focus for the e2e test design is to optimize for ease of inspection.

The iterations and refactorings I do are typically:

- Bringing the tests and code closer to the domain.
- Looking for gaps and omissions, including negative tests and error reporting.
- Introducing additional abstractions to document the intent.

That is, context that helps future iterations.

I do resist the temptation to change the code myself. Instead, I instruct my agent to change it and, once I'm satisfied, I instruct the agent to capture the transformation as a forward-looking SKILL. That way, my review findings turn into future guards and guidance.

## Enforce what you don't inspect

So, how can I guarantee that the uninspected application code remains maintainable and easy to change?

You occasionally hear that code is all about outcomes: what business value does a piece of code enable? That's partly true, but also a massive bit of an over-simplification.

Code isn't just produced and then lying dormant as an immutable artifact. Successful features attract change: improvements, extensions, and additional capabilities. Typically the most business-critical code experiences the largest volume of changes. Making those changes easy is what good software design is all about.

In sharp contrast to early hype, AI didn't make software maintenance go away. Rather, AI amplified the need for maintainable code. As our research discovered, a coding agent is even more picky about code quality than we humans. The bar is higher. So how do I ensure that my code is maintainable if I don't review it? The solution is a multi-layered safety net.

Over the past six months, I've built up a collection of SKILLs that capture my preferred coding style, design principles, and application-specific rules for architecture, etc. Those SKILLs grew gradually as feedback to flaws in AI-produced code.

Still, code quality cannot be left to chance, hoping that Claude or Codex are having a good day. Consequently, I use deterministic tools as part of my workflow. Some of these tools are commercial (e.g. vulnerability scanners, and the CodeHealth MCP), others like linters are free. I then complement those tools with custom-built domain-specific checks to enforce architectural rules and even to catch some of the most common e2e sins.

*[Image: The general human/agent abstraction boundary. In practice, the boundary moves with the uncertainty of the specific task.]*

The point is that these rules and constraints need to be enforced. Deterministically.

## The hardest thing to refactor is our habits

Given that I had typed out code by hand for almost 40 years, becoming comfortable with not reading code was a large mental shift when going agentic.

Almost a year into my agentic journey, I'm now quite confident that I don't need to know every line of code. I get that confidence by knowing that the system behaves as intended, remains maintainable, and lives within the established boundaries.

I also made peace with the fact that agentic code might not look exactly the way I would have written it myself. Familiarity is a poor argument for resisting change.
