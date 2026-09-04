---
source_url: https://medium.com/@iamalvisng/spec-driven-development-is-waterfall-in-markdown-e2921554a600
title: "Spec-Driven Development Is Waterfall in Markdown"
author: Alvis Ng
publication: Medium (self-published; author is a Technical Lead)
published: 2026-03-16
retrieved: 2026-08-16
type: article
capture_note: >-
  Member-only Medium story. Headless fetch returned only the free preview (cut off at
  "Solo…"); captured in full via live Chrome using the author's own paywall-free FRIEND
  LINK, which he publishes in the article's opening line (?sk=1743ebf048396bb0040ab98abf2410e7).
  Medium site chrome (nav, clap/bookmark/sign-in controls, footer) stripped; the author byline block
  is kept at the foot of the capture as provenance for his self-description.
  One inline image noted in brackets. Dannie-directed ingest (2026-08-16), not a watch capture;
  out of the normal 14-day window by ~5 months.
---

# Spec-Driven Development Is Waterfall in Markdown

## SpecKit has 77K GitHub stars. Scott Logic tested it and found it 10x slower. The industry learned nothing from Confluence.

Alvis Ng — 10 min read — Mar 16, 2026

*⭐️ (Not a Medium member yet? Read the rest of this story paywall-free [here](https://medium.com/@iamalvisng/spec-driven-development-is-waterfall-in-markdown-e2921554a600?sk=1743ebf048396bb0040ab98abf2410e7).)*

[SpecKit](https://github.com/github/spec-kit) has 77,000 GitHub stars. AWS built [an entire IDE](https://kiro.dev/) around spec-driven development. [Tessl raised $125 million](https://fortune.com/2024/11/14/tessl-funding-ai-software-development-platform/) on the promise that specs, not code, should be the source of truth.

The pitch was clean: stop vibe coding, write a proper specification, let the agent execute against it. Engineers loved it. It felt like rigor. It felt like the adults had finally entered the room.

Then [someone actually tested it](https://blog.scottlogic.com/2025/11/26/putting-spec-kit-through-its-paces-radical-idea-or-reinvented-waterfall.html) on a real project. Ten times slower. More ceremony. Same bugs.

The industry built an entire ecosystem around one idea: if we give AI agents a detailed enough spec, they'll produce working software. It's the same bet the industry made with outsourcing, with offshoring, with every model that tries to replace understanding with documentation. Write it down clearly enough and someone (or something) on the other side will execute it perfectly.

If nobody read the Confluence page, nobody is reading your `.specify` folder. And the agent that does read it is missing everything the document left out.

I know this because I tried it myself. On a personal project, spec-driven development felt promising. Solo environment. No competing stakeholders. No shifting requirements. I wrote the spec, pointed the agent at it, and the output was reasonable. In isolation, the approach makes sense.

Then I thought about what would happen if I tried this at work. Where the API you're building against ships a breaking change mid-sprint. Where a security audit invalidates your authentication flow after the spec is committed. Where the client reprioritizes the roadmap based on a board meeting you weren't invited to. Where things are dynamic not just between iterations, but within a single ticket.

And I realized spec-driven development works in the one environment where you don't need it. When you're solo and the requirements are stable, a spec is just a conversation with yourself. The moment you add a team, competing priorities, and real-world volatility, the spec is stale before the first standup.

[Image: "Image by Kind and Curious on Unsplash"]

## The $750 Million Bet on a Solved Problem

Let's be specific about what happened in 2025.

GitHub released SpecKit in September. It scaffolds a `.specify` directory with gated phases: specify, plan, tasks, implement. It supports 23 AI agent platforms. It includes a "constitution" file that defines principles the agent must follow. The engineering community treated it like a gift.

Within weeks, SpecKit had a Wikipedia page. Thoughtworks put spec-driven development on the Technology Radar. LinkedIn Learning produced a course. Conference talks appeared. "Spec-Driven Development: The End of Vibe Coding" became a real presentation title at DevLand 2026.

AWS followed with Kiro, a VS Code fork where spec-driven development is the core paradigm. Specifications drive everything: requirements with acceptance criteria, design documents, and implementation tasks. More than 250,000 developers used it during preview.

Then came Tessl, founded by the former Snyk CEO. They took the most extreme position: code is the generated artifact, the spec is the maintained source. Code files get marked `// GENERATED FROM SPEC - DO NOT EDIT`. They raised $125 million at a $750 million valuation. They have 21 employees. They are still in beta.

And the open-source ecosystem exploded. BMAD-METHOD simulates 19 named agent personas: Mary the BA, Preston the PM, Winston the Architect, Devon the Dev. OpenSpec takes a minimalist Markdown approach. GSD claims three developers can produce the output of eight. By March 2026, over 30 frameworks had been mapped in the space.

The narrative was unified: vibe coding is the disease, specs are the cure.

Except the cure doesn't work.

## What Happens When You Actually Test It

Scott Logic's engineers ran SpecKit on a real codebase. Not a todo app. Not a weekend project. A production system with real constraints. The spec phase alone generated 2,500 lines of Markdown, including a 406-line "research document" that told them things they already knew about their own technology stack. The implementation still had bugs. The whole process took roughly 10x what iterative prompting would have taken. Their conclusion: "I don't consider it a viable process, at least not in its purest form."

The Fowler/Bockeler analysis found similar results with Kiro. For a minor bug fix, Kiro generated four user stories with sixteen acceptance criteria. They described it as "using a sledgehammer to crack a nut." Worse, the agents ignored portions of the spec entirely and generated duplicate code despite explicit instructions not to.

Augment Engineer documented a team that produced 1,300 lines of Markdown just to display a date on a page. Their verdict: "We've reinvented Big Design Up Front. We just replaced Word documents with Markdown and project managers with LLMs."

Marmelab's engineering team reached the same conclusion independently. Their blog post title said it all: "The Waterfall Strikes Back." SDD tries to remove developers from software development. That's the same mistake waterfall made, and it failed for the same reason. The most important information surfaces during building, not before.

Even Gojko Adzic, the pioneer of Behavior-Driven Development, weighed in. He called SDD "the revenge of waterfall or BDD taken to a new level."

And SpecKit itself? Developers have started asking whether the project is still actively maintained. Features are quietly being absorbed into GitHub Copilot's native plan mode. The tool that launched the movement may be turning into a feature of the product it was supposed to complement.

## Why Specs Fail as Agent Inputs

The SDD community's response to these failures is predictable: the specs weren't good enough. Write better specs. Be more detailed. Add more acceptance criteria. Give the agent more context.

This misses the point. Specs are fine for communicating between humans who share context, who can ask follow-up questions, who can read between the lines. The problem is using specs as the interface between humans and AI agents. That's where the model breaks.

An AI agent executes exactly what the spec says. It cannot ask "did the designer agree to this flow?" It cannot flag "this conflicts with what DevOps said about the deployment pipeline." It cannot sense that the scope changed in a Slack thread forty minutes after the spec was committed. It takes the document at face value and produces code that matches the words, not the intent.

You do not work on a spec. You work on a requirement that needs to pass through discussions with designers, DevOps engineers, product managers, and stakeholders. Each of these people holds a different mental model of what "done" looks like. The designer thinks in user flows. DevOps thinks in deployment constraints. Product thinks in business outcomes. Your spec flattens all of these perspectives into a single voice: yours. And then you hand that flattened document to an agent and expect it to produce something the whole team can ship.

Even if you write the most comprehensive spec imaginable and commit it to the repo, you would not expect your designers, DevOps engineers, and product managers to open a `.specify` folder and review what you're about to feed the agent. They have their own tools, their own workflows, their own context. The spec becomes a contract between you and the LLM that nobody else signed.

And then there's spec rot. In traditional development, a stale spec is annoying. In spec-driven agentic development, a stale spec is dangerous. The agent will confidently execute against outdated requirements. It won't flag the drift. It won't ask if things have changed. It will generate code that matches a document that no longer matches reality. And it will do it fast.

This is the same failure that killed comprehensive documentation in the Agile era. We learned this lesson. We wrote it down. Apparently, nobody read that document either.

## What Works in the Real World

The question is not whether AI agents need structure. They do. Vibe coding is chaos. The question is where that structure comes from.

Spec-driven development says: write the structure down first, then hand it to the agent. But real projects are dynamic. Requirements change within a ticket. Scope shifts within an iteration. A customer call on Tuesday reshapes the feature you specced on Monday. A deployment constraint surfaces on Thursday that invalidates the architecture you fed the agent on Wednesday. SDD assumes stability. Real teams operate in constant motion.

The workflow that handles this reality gives the agent structure from conversations, not from documents.

Have the syncs. Design, DevOps, product, whoever has context on the requirement. Tell them you're recording the meeting. Gather as much information as possible during that call. The designer says "that flow breaks for screen readers." The DevOps lead says "we can't deploy that behind the canary setup." Product changes the scope based on something the sales team reported yesterday. All of this matters. None of it would have been in a spec, because the person writing it wouldn't have known to include it.

After the call, take the meeting notes and use an LLM to structure everything into a readable format. Decisions made. Constraints identified. Acceptance criteria the group agreed on. Open questions flagged. Commit this alongside the codebase. Not as a spec. As a structured record of what the team actually aligned on.

Then distribute the work. Whatever board the team uses. Each ticket gets filled with clear specifications, acceptance criteria, and a definition of done, pulled directly from the structured meeting notes.

Nobody opens a 40-page specification document. Everyone reads their assigned ticket.

This is where the "spec" actually lives: in the natural unit of work that engineers already read. You're not removing documentation. You're moving it to where people actually look.

For each ticket, write the prompt yourself. Describe what needs to be done alongside the description in the ticket. Use the tools: Superpowers for implementation planning, Serena for codebase-aware editing, whatever MCP servers the stack requires. The prompt is the spec, scoped to one task, written by someone who was in the room when the decisions were made.

And specifically prompt the model to document whenever a decision is made or whenever implementation of a part is done. Every trade-off chosen. Every approach selected over an alternative. Not as a spec. As a trace.

Then you start to notice: things work according to what was actually discussed. Not according to what one person imagined the requirement was. And when things change mid-iteration, as they always do, the trace captures the pivot. The spec would have just been wrong.

## The Trace Changes Everything

When incidents happen, you don't just have code to debug. You have a complete trace of what happened and why the issue might exist.

The meeting where the team decided on the approach. The ticket that specified the acceptance criteria. The prompt that implemented the feature. The decision log that explains why one approach was chosen over another. Every step is traceable to a human conversation, not a generated document that was stale before the first line of code was written.

Think about how you debug today. Something breaks. You open the spec. You compare it to the implementation. You try to figure out where they diverged. But the spec was written two weeks ago, before the scope changed, before three different conversations reshaped the requirements. You're comparing a fantasy document to reality and wondering which one lied.

With a decision trace, you follow the trail. The structured meeting notes tell you what the team agreed on. The ticket tells you the acceptance criteria. The decision log tells you what trade-offs were made during implementation and why. You can trace the bug back to the exact assumption that broke, and you can see the conversation where that assumption was made.

A spec would have just been silently wrong. The trace tells you the story of how the code evolved and why.

This is what it means to embrace AI while keeping yourself in the flow. When you write a spec and hand it to an agent, you've removed yourself from the process. When the code comes back, you're auditing someone else's work. You're a reviewer, not a builder.

When you're in the meetings, writing the prompts, capturing the decisions, you're embedded in the work. You're collaborating with the AI in context, with the full history of why this code exists and what it's supposed to do. You're in the flow, not watching from the outside.

## The Confluence Callback

SpecKit has 77K stars. Kiro got 250K developers. Tessl got $750 million. Thirty frameworks mapped in under a year. Conference talks. A Wikipedia page. The whole ceremony.

And they're solving the same problem Confluence solved in 2005. Giving engineers a well-structured place to write things that nobody reads.

Here's what SDD tools will never fix: the gap between what one person writes down and what a cross-functional team actually needs to ship. No amount of structured Markdown will bridge that gap. The spec is always one person's understanding. The work requires everyone's.

The irony is that AI is genuinely useful in this process. Not as the reader of your spec. As the structurer of your conversations, the scribe of your decisions, the tracer of your reasoning. The best role for AI in your workflow is not replacing the human alignment step. It's making the output of that step retrievable, structured, and permanent.

The spec-driven development movement asked the right question: how do we give AI agents the structure they need to produce useful code? They just answered it wrong. The structure doesn't come from a document one person writes before the work begins. It comes from the conversations that document was supposed to replace.

Your agent doesn't need a spec. It needs the context you only get by being in the room.

> The spec is a contract between you and the LLM that nobody else signed.

---

**Written by Alvis Ng** — 1.8K followers · 1.3K following

> Technical Lead. I write about what I learned/am learning, from software to product insights, faith, psychology, AI, and what's not mentioned in meetings.

*(Author byline block from the source page, kept as provenance for the author's self-description; the
surrounding follow/clap/bookmark controls were stripped.)*
