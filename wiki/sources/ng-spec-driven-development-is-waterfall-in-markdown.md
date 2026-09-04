---
title: "Ng — Spec-Driven Development Is Waterfall in Markdown"
type: source
created: 2026-08-16
updated: 2026-08-16
sources: [ng-spec-driven-development-is-waterfall-in-markdown]
raw_file: [raw/articles/ng-spec-driven-development-is-waterfall-in-markdown.md]
tags: [spec-driven-development, agentic-coding, critique, decision-trace, focus]
---

# Ng — "Spec-Driven Development Is Waterfall in Markdown"

**[[alvis-ng|Alvis Ng]]**, Medium, **2026-03-16** (member-only; captured via the author's own friend link).
Raw: `raw/articles/ng-spec-driven-development-is-waterfall-in-markdown.md`.

The KB's **first sustained outside-in critique of [[spec-driven-development]]**, and the first source to
assemble the *external empirical record* against it in one place. Everything above it in the SDD thread is
either advocacy ([[martin-dilger]]) or an insider's caveat
([[dilger-describing-without-solving-burns-you-out]]); this is a working technical lead arguing the model
itself is wrong for team environments, and proposing a replacement.

## The argument in one line

> "The spec is a contract between you and the LLM that nobody else signed."

SDD, Ng argues, **works only in the environment where you don't need it** — solo, stable requirements,
no competing stakeholders. He tried it on a personal project and it went fine; the failure is structural
and only appears with a team: "the moment you add a team, competing priorities, and real-world
volatility, the spec is stale before the first standup."

## The evidence he assembles (all secondhand — see caveats)

| Source | Finding |
| --- | --- |
| **Scott Logic** (blog, 2025-11-26) | Ran SpecKit on a real production codebase. Spec phase alone = **2,500 lines of Markdown**, including a 406-line "research document" telling them things they already knew about their own stack. Bugs remained. **~10x slower** than iterative prompting. Verdict: "I don't consider it a viable process, at least not in its purest form." |
| **Fowler / Böckeler analysis of Kiro** | For a *minor bug fix*, Kiro generated 4 user stories with 16 acceptance criteria — "using a sledgehammer to crack a nut." Agents also **ignored portions of the spec** and generated duplicate code despite explicit instructions. |
| **Augment Engineer** | A team produced **1,300 lines of Markdown to display a date on a page**. "We've reinvented Big Design Up Front. We just replaced Word documents with Markdown and project managers with LLMs." |
| **Marmelab** | Independent same conclusion, titled "The Waterfall Strikes Back": SDD tries to remove developers from development — waterfall's mistake, failing for waterfall's reason, because **the most important information surfaces during building, not before**. |
| **Gojko Adzic** ([[gojko-adzic]]) | The BDD pioneer calls SDD "the revenge of waterfall or BDD taken to a new level." **⚠ Ng misreads him** — that is the *title* of Adzic's 2025-09-29 post, posed as a question, and Adzic answers the BDD half "it does not, really." Primary captured 2026-08-31; see [[gojko-adzic]]. |

Market context he gives: SpecKit ~77K GitHub stars (Sept 2025, `.specify` dir, gated specify→plan→tasks→
implement phases, a "constitution" file, 23 agent platforms); AWS **Kiro** (VS Code fork, >250K devs in
preview); **Tessl** ($125M raise at a $750M valuation, 21 employees, still in beta, `// GENERATED FROM SPEC
- DO NOT EDIT`); 30+ frameworks mapped by March 2026 (BMAD-METHOD's 19 agent personas, OpenSpec, GSD).
He notes SpecKit's own maintenance is being questioned as features get absorbed into Copilot's plan mode.

## Why specs fail *as agent inputs* (the mechanism)

The community's answer to failure is "write better specs." Ng says that misses the point — the problem is
the **interface**, not the quality:

- Specs work **between humans who share context** and can ask follow-ups. An agent "takes the document at
  face value and produces code that matches the words, not the intent." It cannot ask *did the designer
  agree to this flow?*, cannot flag a conflict with DevOps, cannot sense a scope change in a Slack thread
  forty minutes after commit.
- **The spec flattens perspectives.** "You do not work on a spec. You work on a requirement that needs to
  pass through discussions with designers, DevOps engineers, product managers, and stakeholders." The
  designer thinks in user flows, DevOps in deployment constraints, product in business outcomes; the spec
  compresses all of them "into a single voice: yours." And nobody else will ever open the `.specify`
  folder to check it.
- **Spec rot is worse under agents.** "In traditional development, a stale spec is annoying. In
  spec-driven agentic development, a stale spec is dangerous." The agent executes outdated requirements
  confidently, won't flag drift, "and it will do it fast."

## His replacement: structure from conversations, and a [[decision-trace|trace]]

He agrees agents need structure ("vibe coding is chaos") and disputes only *where it comes from*:

1. **Hold the syncs and record them** — design, DevOps, product. The constraints that matter ("that flow
   breaks for screen readers", "we can't deploy that behind the canary setup") are things of which he
   says: "None of it would have been in a spec, because the person writing it wouldn't have known to
   include it."
2. **LLM-structure the meeting notes** into decisions / constraints / agreed acceptance criteria / open
   questions, committed alongside the codebase — "not as a spec. As a structured record of what the team
   actually aligned on."
3. **Push it into tickets**, pulled from those notes. "Nobody opens a 40-page specification document.
   Everyone reads their assigned ticket." Documentation isn't removed, it's *moved to where people look*.
4. **Write the prompt per ticket yourself** — "the prompt is the spec, scoped to one task, written by
   someone who was in the room when the decisions were made" (he name-checks Superpowers, Serena, MCP
   servers).
5. **Have the model log every decision and trade-off as it goes** — "Not as a spec. As a trace."

The payoff is debugging: instead of "comparing a fantasy document to reality and wondering which one
lied," you follow meeting notes → ticket → prompt → decision log back to the exact assumption that broke.
"A spec would have just been silently wrong. The trace tells you the story of how the code evolved and why."

His closing frame is a role argument: "When you write a spec and hand it to an agent, you've removed
yourself from the process… You're a reviewer, not a builder." AI's best role is "not as the reader of your
spec" but "as the structurer of your conversations, the scribe of your decisions, the tracer of your
reasoning."

## Where this lands in the KB

- It **answers a standing open question** on [[spec-driven-development]] — which asked for "a production
  case study quantifying spec-first vs. prompt-first agent output." The Scott Logic 10x figure is the
  first such number in the KB, and it points the *opposite* way from
  [[dilger-faros-ai-report-amplifies-unclear-requirements]].
- It is **not** a refutation of the KB's actual through-line, and shouldn't be filed as one. Ng's target
  is **document-first SDD toolkits** (SpecKit/Kiro/Tessl). Dilger's own position is that those tools
  *skip the digging* and need [[event-modeling]] as their front half
  ([[dilger-spec-driven-tools-need-event-modeling-front-half]]) — a critique that rhymes with Ng's.
  See [[event-modeled-agent-design]] for where the two genuinely collide: Ng says a spec flattens many
  stakeholders into one voice, which is precisely the failure a *shared visual model built in the room*
  claims to solve.
- The "in the room / reviewer not builder" framing converges with [[comprehension-debt]] and with
  [[morris-humans-and-agents-in-software-engineering-loops|Morris's]] in-the-loop bottleneck (if that
  backfill is accepted), from a different direction: not unread code, but **unowned decisions**.

## Caveats

- **Every empirical claim is secondhand.** Ng cites Scott Logic, "the Fowler/Bockeler analysis", Augment
  Engineer, Marmelab and Adzic; none of these primaries is in `raw/` yet, and the Scott Logic post is the
  only one he links directly. The 10x figure is a practitioner's summary of a single team's single trial,
  not a study.
- **His own test was a personal project.** He explicitly did *not* run SDD at work — the team-environment
  failure is reasoned ("then I thought about what would happen if I tried this at work"), not observed.
- **The replacement workflow is unevaluated.** No numbers, no case study; the decision-trace proposal is
  asserted on the same practitioner authority he criticizes SDD advocates for.
- Self-published Medium opinion piece by a non-tracked author; the headline numbers double as engagement
  hooks. Filed for the argument and the pointers, not as measurement.

_Touches: [[spec-driven-development]] · [[decision-trace]] · [[alvis-ng]] · [[gojko-adzic]] ·
[[event-modeled-agent-design]] · [[comprehension-debt]] · [[given-when-then]] · [[context-engineering]] ·
[[agentic-coding]] · [[vibe-modeling]]._
