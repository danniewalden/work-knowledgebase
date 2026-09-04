---
title: Spec-Driven Development
type: concept
created: 2026-06-13
updated: 2026-08-31
sources: [dilger-spec-driven-development-needs-four-phases, miller-jasperfx-critterstack-ai-event-modeling-strategy, dilger-markdown-is-a-suggestion-dressed-as-a-spec, ng-spec-driven-development-is-waterfall-in-markdown, dilger-describing-without-solving-burns-you-out, dilger-spec-driven-development-applied, dilger-faros-ai-report-amplifies-unclear-requirements, dilger-keep-command-handlers-pure, jwilger-agent-skills-event-modeling, dilger-model-is-a-living-spec-always-on-agent, fraktalio-event-modeler-connect-ai-agents-mcp, dilger-is-code-still-the-source-of-truth, dilger-harness-is-20-percent-requirements-are-80, dilger-user-stories-need-event-modeling-framework, dilger-drawio-model-in-code, dilger-flea-market-model-to-deploy, dilger-spec-driven-tools-need-event-modeling-front-half]
tags: [event-modeling, agentic-coding, spec-driven-development, harness, focus]
---

# Spec-Driven Development

The practice of producing a **clear, validated specification of intended behavior before any code is
written** — and, in the agent era, using that spec as the *environment* that constrains an AI coding
agent rather than trying to steer it with better prompts. Named and evangelized by
**[[martin-dilger]]** ([[dilger-spec-driven-development-applied]], with a `#specdrivenbook` tag for his
book *Spec Driven*), but the underlying move is shared across the KB's harness thread.

## The core argument

- **Prompt engineering is the wrong lever.** Dilger calls it "a desperate attempt to force a language
  model to behave through better wording" that "didn't work." You can't *force* an agent ("AI is like
  a teenager"); you **design an environment where good behavior is the path of least resistance** and
  add feedback loops that keep answering "am I holding this right?"
- **The spec is the environment.** [[event-modeling]] supplies "clarity of intent before a single line
  of code gets written"; that artifact becomes the agent's source of truth. Dilger's rule of thumb:
  *every process that worked well without AI works even better with AI*, because such processes make
  the right thing easier than the wrong thing.
- **Unclear requirements get amplified, not fixed.** The Faros AI Report's quality regressions
  (incidents/PR +242.7%, review time +441.5%) are read as evidence that throughput without an upstream
  spec just ships defects faster ([[dilger-faros-ai-report-amplifies-unclear-requirements]]).
- **The spec is the work — and it's *live*.** Dilger's sharpest statement: "The spec isn't a stepping
  stone to the code anymore. The spec is the work. Everything else follows." He describes an agent
  building continuously from a model as he edits it, with a slice→tests-as-harness→implement→PR loop
  ([[dilger-model-is-a-living-spec-always-on-agent]]). On the tooling side, [[fraktalio]]'s Event
  Modeler has an agent author the model and its Given-When-Then specs over MCP
  ([[fraktalio-event-modeler-connect-ai-agents-mcp]]) — spec-first realized as a feature.
- **The spec is the source of truth; code is a lagging indicator (2026-06-16).** Dilger separates
  *intent* (what the system must do — which in most teams "lives nowhere") from *the actual thing* (what
  the code does), and argues code only ever *chases* intent. When AI generates code from a spec, the
  spec becomes the source of intent and code is "almost disposable," regeneratable on demand, with the
  agent detecting model↔code drift ([[dilger-is-code-still-the-source-of-truth]]). This is the *why*
  beneath "the spec is the work."
- **The 80/20 split (2026-06-29).** Dilger's most quantified statement of the thesis: the
  [[harness-engineering|harness]] and the code are only ~20% of the solution; the other **80% is
  clarifying requirements and understanding business processes**, "a human, communications problem" with
  no technical fix — "nobody tells you how to write that damn markdown." Spec-driven development *is* the
  80%; the harness is the (over-attended) 20% ([[dilger-harness-is-20-percent-requirements-are-80]]).

- **User stories are a format without a framework (2026-07-12).** The mainstream-facing version: teams
  told to write user stories get "a sentence structure" and no way to know what's missing — so they stall.
  The fix isn't discipline but a **visual model with a timeline**; the story then generates *from* the
  model, and eventually the modeled timeline replaces the story as the hand-off artifact
  ([[dilger-user-stories-need-event-modeling-framework]]). The same "produce the spec first, derive the
  downstream artifact from it" move, aimed one level below the usual audience.

- **The spec must be un-corruptable by the agent — a framework + MCP, not raw XML (2026-06-30).** If "the
  spec is the work," an agent that can silently mangle the spec is a hole in the thesis. Dilger's draw.io
  post makes the corollary concrete: keeping the model in git is right, but raw draw.io XML gives the agent
  "no framework to follow, no rules — so it's easy to make mistakes." The fix is a **standardized model
  format + an [[model-context-protocol|MCP]] that validates the agent's edits before commit**, so it
  self-corrects ([[dilger-drawio-model-in-code]]). This is the spec-layer twin of
  [[dilger-keep-command-handlers-pure]] (a written spec is necessary but not sufficient — enforce it) and
  of [[tornhill-cannot-trust-agent-codescene-mcp|"use a deterministic external sensor"]].
- **Pre-made decisions are what make spec-first *fast* (2026-07-01).** The flea-market vignette shows the
  payoff: modelling → code → deploy in under 30 minutes because the platform had already fixed setup,
  architecture, and event-store choices, so the spec was "one button click away from Building." Dilger's
  own honest caveat scopes the thesis — for a trivial app, ceremony-free vibe coding would have been fine;
  "the more complex a system gets, the more that planning step earns its keep"
  ([[dilger-flea-market-model-to-deploy]]; [[vibe-modeling]]).

## Relationship to the rest of the KB

Spec-driven development is the *requirements/intent* face of [[event-modeled-agent-design]]: where
that page maps Event Modeling constructs onto agents, this names the discipline of putting the model
*first*. It converges with [[harness-engineering]]'s guides-and-sensors model and
[[feedforward-and-feedback-controls]] (the "am I holding this right?" loops are inferential sensors),
and with [[context-engineering]] (the spec is high-value context loaded before work). The strongest
worked instance is [[jwilger-agent-skills-event-modeling]], where the spec — vertical slices + Given-
When-Then scenarios — literally becomes the machine-checkable contract (TDD acceptance gates) for an
autonomous build. [[dilger-keep-command-handlers-pure]] is the cautionary corollary: a written spec/
skill is necessary but **not sufficient** — the harness must *enforce* it, because agents drift.

## SDD tools skip the digging — EM is their missing front half (Dilger, 2026-08)

[[dilger-spec-driven-tools-need-event-modeling-front-half]] sharpens Dilger's critique into a concrete
seam. Testing **Spec Kitty** with vague requirements, he found it jumped to the **tech stack by its third
question** and produced a "domain model" before grasping the problem — **46 markdown files in 20 minutes**
that no business stakeholder could follow and no one will maintain. "Skipping the visual model doesn't
remove the complexity — it removes the thing that was managing it." His resolution is **not** to reject
SDD tools but to put **[[event-modeling|Event Modeling]] in front of them**: the event model does the
problem-decomposition and stakeholder alignment, then a skill exports it into the toolkit's task list
(worked with **AWS Kiro**; a planned `eventmodelers export --spec-kitty` CLI bridge for Spec-Kit /
Spec-Kitty / Kiro). This is the [[dilger-harness-is-20-percent-requirements-are-80|"requirements are the
hard 80%"]] thesis made into an interop story, and a fresh direction on the
[[event-modeled-agent-design]] seam (EM → SDD task lists).

## The failure mode, named by its own evangelist (Dilger, 2026-08-14)

Every argument above is *for* spec-first. [[dilger-describing-without-solving-burns-you-out]] is the
first captured source giving SDD's **failure mode**, and it comes from Dilger himself:

> "This is also where spec-driven development goes wrong for a lot of teams. They stop solving problems
> and just describe them, and then hand it to AI and hope it figures out the solution. That's not being
> in charge, that's checking out before it gets interesting… Describing a problem without solving it
> leaves a hole that keeps growing."

The distinction that saves the thesis is **describing ≠ designing**. A spec is the *record of thinking
already done*, not a way to outsource the thinking; "done right, spec-driven development still means
you're in charge of solving the problem. You hand over the boring part." He reports the cost of getting
this wrong as burnout — days spent supervising 5 parallel agent sessions "like a kindergartner," with
the wry observation that "a few years ago, we were obsessed with protecting people from context
switching. Now we call the same thing productivity."

This is the requirements-side twin of [[comprehension-debt]]: you can accrue debt by over-delegating the
*problem*, not only by not reading the generated code. It also gives the KB an internal counterweight
where it previously had only external ones —
[[tornhill-merge-conflicts-agentic-bottleneck|Tornhill's "SDD and the Illusion of Known Scope"]] and the
"stay the engineer" caveats in [[loop-engineering]]. Pair it with
[[bockeler-tdd-inside-the-agent-loop|Böckeler's]] same-week question — *where do we insert ourselves as
arbiters?* — and the two answer identically from opposite ends: **own the problem and the acceptance
criteria; delegate the process.**

## The outside-in critique — and the numbers pointing the other way (Ng, 2026-03)

> **⚠ Chronology correction, 2026-08-31 — this section's framing is wrong and awaits a rewrite.** Ng was
> written up here as the KB's *first* outside-in critique of SDD and as the assembler of an empirical
> record "the KB did not hold at all." Both claims were an artifact of capture order, not of history.
> The 2026-08-31 primaries hunt captured **three earlier originals**, each of which Ng is downstream of:
> Böckeler 2025-10-15 (`raw/articles/bockeler-understanding-sdd-kiro-speckit-tessl.md`), Zaninotto
> 2025-11-12 (`raw/articles/zaninotto-spec-driven-development-waterfall-strikes-back.md`) and Eberhardt
> 2025-11-26 (`raw/articles/eberhardt-putting-spec-kit-through-its-paces.md`) — an **Oct–Nov 2025
> critique wave** that Ng restated four to five months later. Zaninotto cites Böckeler; Eberhardt cites
> Böckeler. Ng's real contribution is *synthesis and the provenance argument*, not primacy or evidence.
> The figures below have been corrected against the primaries; the section's framing has deliberately
> **not** been rewritten, because that is the ingest's job, not a lint's. See
> `outputs/lint-2026-08-31.md`.

[[ng-spec-driven-development-is-waterfall-in-markdown]] is the KB's **first captured** critique of SDD
from outside the thread, and it changed what this page could claim. Two contributions:

**1. It assembles the external empirical record**, which the KB had not held until then — though, as the
correction above notes, the originals it summarises predate it:

- **Scott Logic** — *now corrected against the primary, captured 2026-08-31
  ([[eberhardt-putting-spec-kit-through-its-paces|raw]]): the author is Colin Eberhardt, Scott Logic's
  CTO, and the codebase is his own hobby app, not a production one.* Rebuilding one feature with Spec Kit
  cost **33m30 of agent time, 689 loc and 2,577 lines of markdown against 3.5 hours of review**; his
  ordinary iterative approach produced 1,000 loc in 8m of agent time with 24 minutes of review and no
  bugs, while the Spec Kit run shipped a broken dev server. He puts it at "around ten times faster"
  without SDD — *his own impression, not a measurement.* The 406-line research document restating his own
  stack is real, as is "I don't consider it a viable process, at least not in its purest form."
  **Correction to a figure this page carried since 2026-08-16:** "the spec phase alone produced 2,500
  lines of Markdown" was wrong — 2,577 is the *cumulative* total for the whole feature; the specify step
  alone was 230 lines, and the plan step was the bloated one at 2,067.
- **Böckeler's Kiro analysis** (*not* "Fowler/Böckeler" — she is the sole author, published on Fowler's
  site; also captured 2026-08-31): four user stories and sixteen acceptance criteria *for a minor bug
  fix* — "a sledgehammer to crack a nut" — with agents ignoring parts of the spec anyway. Verified
  verbatim against the primary.
- **Augment Engineer**: 1,300 lines of Markdown to display a date. "We've reinvented Big Design Up Front.
  We just replaced Word documents with Markdown and project managers with LLMs."
- **Marmelab**, independently: "The Waterfall Strikes Back" — SDD repeats waterfall's mistake because
  "the most important information surfaces during building, not before."
- **[[gojko-adzic]]**, from inside the BDD tradition — *but see the correction below*: Ng relays him as
  saying SDD is "the revenge of waterfall or BDD taken to a new level."

> **⚠ Misattribution, corrected 2026-08-31.** "The revenge of waterfall or BDD taken to a new level" is the **title of Adzic's post, posed as a question** — not his verdict. The primary is now captured (`raw/articles/adzic-spec-driven-development-revenge-of-waterfall-or-bdd`, 2025-09-29) and he answers the BDD half **"it does not, really"**, never calls SDD waterfall in the body, and lands warmer than any other critic: *"definitely something to keep an eye on… Teams looking for more structure in their AI code generation workflows might find it useful now."* Ng relayed the headline as a judgment and the KB repeated it. His actual objections are narrower and more useful: generated specs are
> **scope-of-work, not specification** ("this is not a spec, it lacks a ton of detail" — the real spec
> ends up in developer-readable unit and integration tests, "a missed opportunity"), and Spec Kit lacks a
> **scoping phase**, so it "tried to do too much and kind of went off the rails" until human-in-the-loop
> was no longer feasible. Awaiting ingest.

**2. It names the mechanism as an *interface* problem, not a quality problem.** The community answer to
these failures — write better specs — misses it. An agent "takes the document at face value and produces
code that matches the words, not the intent"; it cannot ask whether the designer agreed to the flow, and
cannot see the scope change in a Slack thread forty minutes after commit. Worse, a spec **flattens a
cross-functional set of mental models into one voice** — the author's — and no designer, DevOps engineer
or PM is ever going to open a `.specify` folder to check it. Hence the line: *"The spec is a contract
between you and the LLM that nobody else signed."* And **spec rot changes character** under agents: a
stale spec used to be annoying, now it is dangerous, because the agent executes it confidently, fast, and
without flagging drift.

His counter-proposal is not "no structure" but structure harvested from recorded cross-functional
conversations and carried into tickets, prompts, and an in-flight decision log — see [[decision-trace]].

### How much of this actually lands on the KB's thesis

Less than the title suggests, but not nothing:

- **Ng's target is document-first SDD *toolkits*** (SpecKit, Kiro, Tessl), and on those he and
  [[martin-dilger]] partly agree: [[dilger-spec-driven-tools-need-event-modeling-front-half]] found Spec
  Kitty reaching for the tech stack by its third question and emitting 46 markdown files in 20 minutes
  that "no business stakeholder could follow." Eberhardt's and Zaninotto's numbers, which Ng relays, are
  the external measurement of exactly that complaint — and Zaninotto's independently-arrived list of
  seven failure modes (context blindness, markdown madness, systematic bureaucracy, faux agile, **double
  code review**, false sense of security, diminishing returns on brownfield) is the fullest statement of
  it anywhere in the material.
- **The genuine collision is over authorship.** This page's thesis is that the spec is the work; Ng's
  objection is that *one person's* spec is the work of one person. The KB's answer has to be that
  [[event-modeling]] is built collaboratively with stakeholders in the room and stays live — which is a
  claim about practice, not about the artifact, and the KB has no independent evidence that modelling
  sessions resist the flattening Ng describes. See [[event-modeled-agent-design]].
- **What does not survive unqualified** is the assumption that a written spec handed to an agent is
  *cheap*. Eberhardt's ratio is the KB's only figure on the cost side of "the spec is the work," and it
  points the opposite way from [[dilger-faros-ai-report-amplifies-unclear-requirements]]. Treat it as an
  impression rather than a datum: it is one person's self-report on one hobby project, and he says so.

**Weight it accordingly:** every figure above is secondhand in Ng's telling, none of the primaries is in
`raw/`, his own SDD trial was a solo personal project, and his replacement workflow is itself unevaluated.

## "Requires suitable language" — and the counter-position (2026-08)

The two poles of [[model-as-code-vs-model-as-language]] are both, at root, positions on *this* page's
central question: if prose specs fail, what replaces them?

**[[martin-dilger]]** answers with a formal modeling language
([[dilger-markdown-is-a-suggestion-dressed-as-a-spec]], 2026-08-25). His test is a ratio: *"Pages of prose to
produce a handful of lines. If the explanation outweighs the thing it's explaining, the tool doing the
explaining is wrong - always was."* Hence: *"Spec-Driven Development requires suitable language. Event
Modeling is the one that works for me. A precise specification of behavior."* Note he explicitly grants
that code **is** a formal language; his objection is that code specifies implementation while the thing
needing specification is behavior over time — and that the business cannot review it.

**[[jeremy-miller]]** answers with executable specifications and no intermediate model at all
([[miller-jasperfx-critterstack-ai-event-modeling-strategy]], 2026-08-21). His Bobcat tool takes the Gherkin path, and the
design rule is explicit: *"Rather than have people waste time writing intermediate models for policies,
constraints, or validation rules in a diagram, go straight to Behavior Driven Development specifications
that become actionable specs."* This is **not** a rejection of [[given-when-then]] — it is the claim that
GWT is the *only* part worth authoring by hand, with the structural rest inferred from code.

What they share is narrower than it looks, and worth stating precisely: **hand-authoring a separate
description of the rules is waste.** Ng and Dilger both aim that at *Markdown-as-specification* — Ng on
provenance grounds (nobody agreed it), Dilger on language grounds. **Miller does not.** He never
discusses prose or Markdown specs; his target is diagrams and intermediate DSLs, and he lists "a markdown
input?" among options he would consider for expressing tests. Treating all three as one anti-Markdown
front is the tidy-symmetry error [[model-as-code-vs-model-as-language]] was written to avoid — see the
framing caution on that page.

## The scoping counter-argument — SDD needs four phases (Dilger, 2026-08-29)

[[dilger-spec-driven-development-needs-four-phases]] answers the whole critique cluster above by saying
it is aimed at the wrong phase:

> 1) Idea → Intent · 2) Intent → Spec · 3) Spec → Code · 4) Code → Operations & Maintenance
>
> "Most frameworks and handbooks like Kiro, SpecKit and also Anthrophics latest Handbook on Software SDLC
> - focus almost exclusively on 3) … Leaving out 75% of the work."

His ranking: 1 and 4 are hard, 2 "is mechanical if 1) is done right", 3 "the easiest of them all." The
test he offers: *"You are not doing SDD if you don't have an answer to 1) or 4)."*

Two observations the KB should attach to this:

- **It is close to unfalsifiable as stated** — any SDD failure can be attributed to a missing phase 1 —
  and phases 1 and 2 are what his platform and consulting sell. Treat it as a reframing to test, not a
  rebuttal that lands.
- **But it converges with [[gojko-adzic]] independently.** Adzic's central complaint about Spec Kit is a
  missing **scoping phase**, which is Dilger's phase 1 in different words, from the BDD tradition rather
  than the Event Modeling one, with neither citing the other. Two people arriving at "the tools implement
  the easy middle" is worth more than either alone.
- **Phase 4 is a genuine hole in this KB.** Operations and maintenance of agent-built systems is
  addressed by no captured source — and it is one of the two he calls hardest.

## Open questions

The standing ask — *a production case study quantifying spec-first vs. prompt-first agent output* — is now
**partially answered, and against the thesis**: Eberhardt's ~10x is the first such figure, though it is
one person, one hobby project, one toolkit, and is a self-reported impression rather than a measurement.
*(Update 2026-08-31: the primary is now captured, so this no longer reaches the KB secondhand — but the
page has not yet been rewritten from it. See the ingest note below.)* Still open: nothing comparable exists for
*model-first* SDD as Dilger practises it, so the KB cannot yet tell whether the 10x indicts spec-first
thinking or just the document-generating toolchains.

Also open: **if not a hand-authored spec, then what?** The two loudest voices diverge completely on the
replacement — a formal modeling language (Dilger) or the code itself with visualization on top (Miller). That disagreement is tracked separately
at [[model-as-code-vs-model-as-language]] (added 2026-08-30).

Also open: **how do you tell a spec that records solved thinking from one that defers it?** Dilger names
the failure but offers no test for it beyond a felt sense ("when did you last feel the kick of actually
solving something"). Ng supplies an oblique candidate — *was the author in the room when the decisions
were made?* — which is a provenance test rather than a content test.

_Sources: [[dilger-spec-driven-development-applied]] ·
[[dilger-faros-ai-report-amplifies-unclear-requirements]] · [[dilger-keep-command-handlers-pure]] ·
[[jwilger-agent-skills-event-modeling]] · [[dilger-model-is-a-living-spec-always-on-agent]] ·
[[fraktalio-event-modeler-connect-ai-agents-mcp]] · [[dilger-is-code-still-the-source-of-truth]] ·
[[dilger-harness-is-20-percent-requirements-are-80]] · [[dilger-user-stories-need-event-modeling-framework]] ·
[[dilger-drawio-model-in-code]] · [[dilger-flea-market-model-to-deploy]] · [[dilger-spec-driven-tools-need-event-modeling-front-half]] ·
[[dilger-describing-without-solving-burns-you-out]] · [[ng-spec-driven-development-is-waterfall-in-markdown]]._
