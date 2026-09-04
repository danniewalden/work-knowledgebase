---
source_url: https://www.linkedin.com/pulse/spec-driven-development-revenge-waterfall-bdd-taken-gojko-adzic-imquf
title: "Spec Driven Development - revenge of Waterfall or BDD taken to new level?"
author: Gojko Adzic
publication: LinkedIn Pulse
published: 2025-09-29
retrieved: 2026-08-31
type: article
---

# Spec Driven Development - revenge of Waterfall or BDD taken to new level?

Gojko Adzic — Author of Lizard Optimization, Impact Mapping, Specification by Example and a few more books… Partner at Neuri Consulting LLP, working on Narakeet and Votito

September 29, 2025

At Citcon last weekend, we had a quick look at the new Spec Kit tool from Microsoft/GitHub (https://github.com/github/spec-kit), promoting something called "Spec Driven Development", with the promise of executable specifications. The idea was to compare it to Spec by Example/BDD-style executable specifications and see if this is an evolution of the idea or something totally different. Here are some of my conclusions:

## What is it?

Spec-Driven Development seems to be an attempt to formalize a workflow around AI agent coding, extracting and codifying successful patterns for working with AI code generators into a process that can be standardized, and can be enforced by a tool across different people and teams. There are two current implementations of this, Spec Kit from Microsoft and Kiro from AWS. We primarily looked into Spec Kit, so the conclusions below might or might not apply to Kiro - I'd love your comments on this if you used Kiro.

The workflow enforces several steps, such as setting up the project "constitution", creating a "specification" that focused on what needs to be built and not how, then an implementation plan with tasks, and finally executing those tasks. AI coding agents do most of the work, keeping a human in the loop through documents generated for each phase.

For example, we asked Spec Kit to write a specification for a conference voting session, then went in and edited the resulting file, and let it then proceed to make a plan.

Using the AI tool to guess sensible defaults, while still being able to edit the conclusions before the next phase reminded me of Llewellyn Falco and his talk on process files and blueprints (https://craft-conf.com/2025/talk/hands-on-llewellyn-falco) for agentic AI.

## How it works?

Technically, Spec Kit creates custom commands for AI agents, supporting a range of tools that people already use (we tried it using Claude Code, but it seems to support almost any popular agent tool). Kiro, from what I understand, takes a different approach and works as a Visual Studio Code fork, forcing you to use their own custom IDE.

Spec Kit creates files in a project, that are supposed to be committed to version control, both to keep the project collective memory and to track it's own progress.

## What I like about it?

My first impressions is that the flow set by the tool mimics a lot of what I am currently doing when using Claude Code, and makes it more systematic. Exposing the tool conclusions into editable text files is a great way to keep a human in the loop and allow tweaking and adjusting the AI agent flow.

For example, when we asked it to spec out a conference voting system, the tool went into an interactive mode asking reasonable clarifying questions, and created a decent set of requirements for such a system.

In the technical research phase, it selected bad defaults (e.g. an outdated version of Node.js) but it was relatively easy to then tweak the generated file and tell it to use different tools. Making such choices explicit at least forces people to think harder about what they want to do, and directs AI agents with less effort than writing all of that from scratch.

## What I don't like about it

There's a lot of documentation generated throughout the process, walls of text that are difficult to parse. Most of it seems to be for the tool to track its own progress, and not necessarily for human consumption. We ended up just glancing or skipping through most of it, instead of reading the details.

The "spec" contains acceptance criteria in the given-when-then format, and functional requirements set out as must/should/could, but this is on such a high level that it fits more the scope of work than a specification. Here's the example that it generated for us:

```
## User Scenarios & Testing *(mandatory)*

### Primary User Story
Conference organizers want to collect real-time feedback on sessions during a conference. Attendees can join voting sessions for specific conference sessions, rate presentations, and provide feedback while dozens of people vote concurrently. Organizers can view aggregated results to understand session quality and attendee engagement.

### Acceptance Scenarios
1. **Given** a conference session is active, **When** an attendee enters the session voting code, **Then** they can access the voting interface for that specific session
2. **Given** an attendee is in a voting session, **When** they submit a rating and feedback, **Then** their vote is recorded and contributes to real-time results
3. **Given** multiple attendees are voting simultaneously, **When** votes are submitted, **Then** all votes are processed without data loss or system slowdown
4. **Given** a session organizer, **When** they view the session results dashboard, **Then** they see aggregated ratings, feedback comments, and participation statistics
5. **Given** a voting session is closed, **When** attendees try to access it, **Then** they receive a clear message that voting has ended

### Edge Cases
- What happens when dozens of people submit votes simultaneously?
- How does the system handle network interruptions during vote submission?
- What occurs when an attendee tries to vote multiple times for the same session?
- How are incomplete or invalid votes handled?
- What happens when session voting time limits are reached?

## Requirements *(mandatory)*

### Functional Requirements
- **FR-001**: System MUST allow conference organizers to create voting sessions for specific conference sessions
- **FR-002**: System MUST generate unique access codes for each voting session that attendees can use to join
- **FR-003**: System MUST support concurrent voting by up to 100 attendees without performance degradation
- **FR-004**: System MUST collect 1-5 star ratings from attendees for each session
- **FR-005**: System MUST display real-time aggregated results to session organizers
- **FR-006**: System MUST prevent duplicate voting by the same attendee for a single session
- **FR-007**: System MUST handle up to 100 concurrent users without performance degradation
- **FR-008**: System MUST store voting data and automatically delete it 30 days after conference end date
- **FR-009**: System MUST allow anonymous access to voting sessions using only the unique voting code
- **FR-010**: System MUST support 1-5 star rating input with simple rating interface
- **FR-011**: System MUST allow organizers to manually start and stop voting sessions with no automatic time limits
- **FR-012**: System MUST allow public access to view voting results for anyone with the session voting code
```

This is not a spec, it lacks a ton of detail. The real "spec" then ends up being in unit and integration tests that are generated based on these requirements. It just seems as a missed opportunity to create human-readable specs and drive the work from that.

Another thing that I did not like is that there's a scoping phase missing as a result. With such a spec, the tool tried to do too much and kind of went off the rails. We generated a ton of tests and code, but it was so overwhelming that the whole "human in the loop" idea was no longer feasible. With a more explicit scoping phase such a tool could enforce iterative delivery and progressive enhancement, identifying smaller chunks to built and keep humans in the loop.

## How this relates to Spec by Example/BDD?

It does not, really. The idea of "executable specifications" that Spec Kit tries to achieve is really materialising in unit and integration tests, that are readable only for developers. The artifacts it creates are perhaps useful as a high level overview for project management and progress tracking, not as detailed specifications.

## Conclusions

This so far looks interesting, and definitely something to keep an eye on, especially as it's still early days. Teams looking for more structure in their AI code generation workflows might find it useful now.

I'd love to see this approach evolve more and include a more explicit scoping phase, promoting iterative delivery, and to figure out how to use a source of truth that's detailed enough for people to approve/complain about, but not just in code. Until it does, it's not really going to live up to the promise of executable specs.

---

*Capture note (2026-08-31): the fourth and last of the "uncaptured primaries behind the SDD critique" open in `wiki/overview.md` since 2026-08-16. Blocked earlier today when the browser refused LinkedIn content access; retrieved on retry via live logged-in Chrome. **It is the earliest of the four by a wide margin** — 2025-09-29, three weeks after Spec Kit's September launch, versus Böckeler 2025-10-15, Zaninotto 2025-11-12, Eberhardt 2025-11-26 and Ng 2026-03. The KB has quoted him only through Ng's secondhand "the revenge of waterfall or BDD taken to a new level," which turns out to be **the title's question, not his conclusion** — the piece answers "it does not, really" to the BDD comparison and never actually calls SDD waterfall in the body. His verdict is markedly warmer than the other three: "definitely something to keep an eye on… Teams looking for more structure in their AI code generation workflows might find it useful now." The substantive objections are (1) generated specs are **scope-of-work, not specification** — the real spec ends up in developer-readable unit and integration tests, "a missed opportunity to create human-readable specs"; (2) a **missing scoping phase**, so the tool "tried to do too much and kind of went off the rails" and human-in-the-loop stopped being feasible; (3) walls of tool-progress documentation nobody reads. Note he is the author of* Specification by Example *and* Impact Mapping*, so the BDD comparison is first-party. Nav/footer/comments/reactions stripped; the generated spec sample is preserved verbatim in a code fence as it appeared inline.*
