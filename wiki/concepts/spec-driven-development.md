---
title: Spec-Driven Development
type: concept
created: 2026-06-13
updated: 2026-09-04
sources: [dilger-spec-driven-development-needs-four-phases, miller-jasperfx-critterstack-ai-event-modeling-strategy, dilger-markdown-is-a-suggestion-dressed-as-a-spec, ng-spec-driven-development-is-waterfall-in-markdown, dilger-describing-without-solving-burns-you-out, dilger-spec-driven-development-applied, dilger-faros-ai-report-amplifies-unclear-requirements, dilger-keep-command-handlers-pure, jwilger-agent-skills-event-modeling, dilger-model-is-a-living-spec-always-on-agent, fraktalio-event-modeler-connect-ai-agents-mcp, dilger-is-code-still-the-source-of-truth, dilger-harness-is-20-percent-requirements-are-80, dilger-user-stories-need-event-modeling-framework, dilger-drawio-model-in-code, dilger-flea-market-model-to-deploy, dilger-spec-driven-tools-need-event-modeling-front-half, adzic-spec-driven-development-revenge-of-waterfall-or-bdd, bockeler-understanding-sdd-kiro-speckit-tessl, zaninotto-spec-driven-development-waterfall-strikes-back, eberhardt-putting-spec-kit-through-its-paces, tornhill-blast-from-the-past-sdd-illusion-of-known-scope, dilger-communicating-intent-to-an-agent-needs-a-dsl, dilger-ux-as-first-class-in-spec-driven-development, dilger-only-engineers-care-about-consistent-systems, dilger-agentic-engineer-program-stack-agnostic-spec, dilger-goto-cph-2026-event-modeling-ai-native-software-design, tune-no-rapport-with-a-model-you-didnt-code]
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

## Weak, strong, and which one is under attack (Böckeler's ladder)

Almost every disagreement on this page is really a disagreement about *which* SDD.
[[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler]] (2025-10-15) supplied the distinction the KB
now uses as working vocabulary, and it is worth stating before anything else:

- **Spec-first** — a well-thought-out spec is written first and used for the task at hand.
- **Spec-anchored** — the spec is *kept* after the task and used for evolution and maintenance.
- **Spec-as-source** — the spec is the main source file over time; only the spec is edited and *"the
  human never touches the code."*

Her finding: *"All SDD approaches and definitions I've found are spec-first, but not all strive to be
spec-anchored or spec-as-source. And often it's left vague or totally open what the spec maintenance
strategy over time is meant to be."* She classifies Kiro and spec-kit as spec-first in practice
(spec-kit branches per spec, i.e. per change request, not per feature) and Tessl as the only one
reaching for spec-as-source. *(**NOT INDEPENDENT** — martinfowler.com is [[thoughtworks]]' own channel
and Böckeler is a Thoughtworks Distinguished Engineer; she is a primary here, but not external
corroboration for any Thoughtworks framing.)*

**Why this changes how the critique cluster reads:**

- **[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill]] scopes himself to the strong
  form explicitly** — *"It can be anything from a relatively lightweight way to drive agents to a
  strong form where the spec itself is the ground truth. It's the latter I'm concerned with."*
- **[[eberhardt-putting-spec-kit-through-its-paces|Eberhardt]]** classifies Spec Kit as spec-as-source,
  *"SDD in the purest form"*, and closes by rejecting SDD *"at least not in its purest form."*
- **Böckeler herself practises spec-first and recommends it** — *"the general principle of spec-first is
  definitely valuable in many situations."*
- **[[gojko-adzic|Adzic]] never argues against specification at all** — his complaint is that the
  generated artifact isn't one.

So the honest summary is: **spec-first is close to consensus; spec-as-source is what the sceptics
reject; and the KB's own thesis — "the spec is the work", a live model regenerating code — sits at the
spec-as-source end.** That is where the argument actually is.

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
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill's "SDD and the Illusion of Known Scope"]] and the
"stay the engineer" caveats in [[loop-engineering]]. Pair it with
[[bockeler-tdd-inside-the-agent-loop|Böckeler's]] same-week question — *where do we insert ourselves as
arbiters?* — and the two answer identically from opposite ends: **own the problem and the acceptance
criteria; delegate the process.**

## The outside-in critique — and the numbers pointing the other way (Ng, 2026-03)

[[ng-spec-driven-development-is-waterfall-in-markdown]] is the KB's **synthesis** of the SDD critique,
not its origin. The provenance runs **Adzic (2025-09-29) → Böckeler (2025-10-15) → Zaninotto
(2025-11-12) → Eberhardt (2025-11-26) → Ng (2026-03)**; Zaninotto and Eberhardt both cite Böckeler, and
so does Tornhill. All four primaries are now captured, and every figure the KB used to reach through Ng
is re-cited to its primary below. Two contributions remain his: the assembled record, and the
interface/authorship argument.

**1. The empirical record, from the primaries:**

- **[[eberhardt-putting-spec-kit-through-its-paces|Eberhardt]]** (Colin Eberhardt, CTO of
  [[scott-logic]], 2025-11-26 — the primary, nine months before Ng). He deleted a ~1,000-line feature
  from his own hobby PWA and rebuilt it with Spec Kit, committing every step. Totals:
  **33m30 agent time, 689 loc, 2,577 lines of markdown, 3.5 hrs review**, and the run shipped a broken
  dev server (a trivial unpopulated-variable bug). His ordinary iterative approach on the same class of
  work: **8m agent time, 1,000 loc, no markdown, 15 min review, 9 min functional test, no bugs.** He
  puts it at *"around ten times faster"* without SDD — **his own impression, not a measurement** (n=1,
  one hobby app, one toolkit, and he had already built the feature once). **Correction the primary
  confirms:** the KB's old "2,500 lines of Markdown in the spec phase" was wrong — 2,577 is the
  *cumulative* total, Specify alone was **230** lines, and **Plan** was the bloated step at **2,067**
  (including a 444-line module contract *"4x the length of the actual module itself"* and a 406-line
  research document). Verdict: *"I don't consider it a viable process, at least not in its purest
  form."*
- **[[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler]]** (2025-10-15, the earliest of the
  hands-on trials and the origin of the weak/strong ladder above — *not* "Fowler/Böckeler"; she is sole
  author, published on Fowler's site). Kiro turned a **minor bug fix into 4 user stories with 16
  acceptance criteria** — *"like using a sledgehammer to crack a nut"* — with agents ignoring parts of
  the spec anyway, and in one case reading spec-kit's *descriptions of existing classes* as new
  requirements and **regenerating them as duplicates**. *"To be honest, I'd rather review code than all
  these markdown files."* **NOT INDEPENDENT** (Thoughtworks' own channel).
- **[[zaninotto-spec-driven-development-waterfall-strikes-back|Zaninotto]]** (François Zaninotto,
  founder/CEO of [[marmelab]], 2025-11-12 — *"The Waterfall Strikes Back"*, 225 points on Hacker News,
  and the likely lineage of Ng's own title). The **1,300 lines of Markdown across 8 files to display a
  date** figure the KB has been attributing to "Augment Engineer" via Ng **originates here**, linked to
  a public PR. His seven failure modes are the fullest such list anywhere in the material:
  **context blindness, markdown madness, systematic bureaucracy, faux agile, double code review, false
  sense of security, diminishing returns on brownfield** (*"For large existing codebases, SDD is mostly
  unusable"*). His distinctive argument is about **who SDD is for**: *"You must be a business analyst to
  catch errors during the requirements phase, and a developer to catch errors during design… it can
  only be used by the rare individuals who master both trades. SDD repeats the same mistake as No Code
  tools."* His replacement is smaller units, not fewer documents — a Lean-Startup loop he calls
  **Natural Language Development**. He is also **the only one of the four who calls SDD a step in the
  wrong direction outright**.
- **[[gojko-adzic]]**, from inside the BDD tradition and the **earliest** of the primaries
  ([[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]], 2025-09-29 — three weeks after Spec
  Kit launched). Ng relayed his title as a verdict; it is a **question**, and the KB repeated the error
  for two weeks. Adzic answers the BDD half **"It does not, really"**, **never calls SDD waterfall
  anywhere in the body**, and lands warmer than any other critic: *"definitely something to keep an eye
  on… Teams looking for more structure in their AI code generation workflows might find it useful
  now."* He likes that the tool's conclusions land in editable, version-controlled text files, and says
  the flow *"mimics a lot of what I am currently doing when using Claude Code, and makes it more
  systematic."*

  His two real objections are narrower and more useful than the headline. **(1) Scope-of-work, not
  specification.** The generated spec carries [[given-when-then|GWT]] scenarios and MUST/SHOULD
  requirements, but *"this is on such a high level that it fits more the scope of work than a
  specification… This is not a spec, it lacks a ton of detail."* The real spec then migrates into unit
  and integration tests *"readable only for developers"* — *"a missed opportunity to create
  human-readable specs and drive the work from that."* Coming from the author of *Specification by
  Example*, that is a **first-party** verdict on whether SDD is BDD taken further: it isn't, because
  the executable specification stops being human-reviewable. **(2) A missing scoping phase**, so
  *"the tool tried to do too much and kind of went off the rails. We generated a ton of tests and code,
  but it was so overwhelming that the whole 'human in the loop' idea was no longer feasible."*
  What he wants is *"a source of truth that's detailed enough for people to approve/complain about, but
  not just in code."*

**Do not flatten these four into one anti-SDD front.** Adzic is the warmest and never argues against
specification; Böckeler is a **tool** critic who practises and recommends spec-first herself; Eberhardt
rejects the *purest* form and defends the debate; Tornhill (below) scopes himself to the strong form and
**explicitly declines the waterfall argument**; only Zaninotto calls SDD a step in the wrong direction.

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

## The deepest objection: implementation *is* the discovery process (Tornhill, 2026-05-28)

[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]] is not another complaint about markdown
volume, and it is not the waterfall argument — he declines that explicitly: *"Not due to waterfall
thinking — many SDD practitioners evolve their systems iteratively — but rather due to the nature of
problem solving."* His argument is one claim with a mechanism.

**The claim.** *"Implementation is an essential part of the discovery process itself. And the further we
remove ourselves from it, the harder it becomes."* So a method that treats the spec as ground truth
mislocates where the learning happens.

**The mechanism — requirements explosion.** He invokes **Robert Glass**: *"for every 10-percent
increase in problem complexity, there is a 100-percent increase in the software solution's
complexity."* Therefore *"each requirement in the spec will lead to tens of implicit design
requirements that need to be resolved. We cannot leave that as guesswork for an agent to figure out."*
*(**Glass's assertion as relayed by Tornhill** — he names no specific work and measures nothing
himself. Never write "research shows".)*

**Why you cannot answer it with a fuller spec** — his three obstacles: (1) *"Free text lacks
precision… Even structured prose and checklists leave room for ambiguity. That's why we have
programming languages."* (2) You cannot know the solution requirements up front, and if agents decide
them for you, recovering them is *"like reverse engineering a legacy codebase. That's the position we'd
be in. Constantly."* (3) Enriching a requirements spec with implementation detail and contracts blurs
it: *"the model starts to become the implementation and loses its value as an overview."* Hence the
line the whole piece turns on:

> "The moment a model becomes the implementation, it ceases to be a good model."

**He is not anti-document.** *"We should write stuff down to make it more concrete and invite a
conversation. That helps thinking, too. But we need to treat that document as an imperfect starting
point rather than the finished product."* His position on SDD is *"something I'll continue to observe
but sit out on for now."*

**What this costs this page's thesis.** [[dilger-is-code-still-the-source-of-truth|"Code is a lagging
indicator, almost disposable"]] and *"the spec is the work"* both assume the spec can hold the intent.
Tornhill's answer is that most of what must be decided **is not intent at all** — it is implicit
design, discoverable only by building. The Event Modeling reply would have to be that a timeline plus
[[given-when-then|GWT]] scenarios per slice *does* pin those decisions down; **the KB has no evidence
for that**, and obstacle (3) attacks it directly: specify enough to resolve implicit requirements and
you have turned the model into the implementation.

**And it is the second MDA warning in the batch.** Tornhill lived through Model-Driven Architecture,
Executable UML and RUP at two employers: the design review with hand-drawn UML worked and paid off for
onboarding; then the vendors closed the loop with an action language and *"the first victim was the
documented design. The executable diagrams turned so bloated and verbose that they became literally
incomprehensible. After all, the new audience was a compiler, not humans."* Tooling regressed too — no
pipelines, CLIs, IDEs or linters: *"Imagine coding in a Microsoft Word document."*
[[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler]] reaches for the same precedent
independently and adds the half Tornhill omits: MDD's **parseable structure at least bought tool
support** for writing valid, complete, consistent specs, which natural-language SDD gives up — so
spec-as-source risks *"the downsides of both MDD and LLMs: Inflexibility and non-determinism."*

*(**NOT INDEPENDENT** for the alternative he prescribes — *"intention-revealing software design,
automated safeguards for our code and its behavior"* is the category his own product, CodeScene,
sells. And note the piece contains **no figures at all**.)*

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

He then names what is missing, which the August post did not
([[dilger-communicating-intent-to-an-agent-needs-a-dsl]], 2026-09-03):

> "Somehow the software industry has chosen raw markdown as the medium of choice to do that. I'm not a
> fan of this. Raw markdown is suboptimal for anything beyond a project kickoff… What used to be a
> Jira Ticket became Markdown Files. Same old stuff, some new paint. **What's missing is a DSL to
> unambiguously describe flow, behavior + business rules.**"

Three things about this are load-bearing and easy to get wrong:

- **He is not objecting to markdown as a file format.** *"The medium itself - nobody cares in the end
  ( you can export Json, Markdown, Toon.. from my tools )."* The objection is to markdown as a
  *language*. Anyone reading him as anti-markdown-file is reading him wrong.
- **His four requirements on the medium** — *specific, unambiguous, information complete, structured* —
  are the closest thing the KB has to a testable statement of what an agent-facing spec must be. They
  are asserted, not defended.
- **"For me, Eventmodeling is that DSL. Battle-tested over hundreds of projects by many companies. I
  documented the standard Json-Format in 2024."** *(**VENDOR SELF-REPORT** — "hundreds of projects" is
  **his own figure** with no project, company or method named, and he sells the platform and the
  training the claim underwrites; **no independent corroboration for it exists anywhere in this KB**.
  The 2024 JSON format is referenced by a shortlink and is **not captured in `raw/`**.)*

Two more September notes complete the position, and one of them relocates the objection entirely.
[[dilger-only-engineers-care-about-consistent-systems]] (2026-09-01) argues the problem is not the
notation but the **chain of handovers**: *"requirements engineers talking to product owners, product
owners talking to business, nobody talking to real clients - everything reshaped a little at each hop…
Now with AI - we are just adding one more hop to the chain. Engineers talking to AI, writing tons of
markdown.. one more handover."* His fix is a conversation and then a modelling session with screens,
*"and you do not have to write a single line of code for that."* **This is the same diagnosis
[[ng-spec-driven-development-is-waterfall-in-markdown|Ng]] makes** — the spec is a contract nobody else
signed — reached from the opposite camp, and the two split only on what the room should produce (Ng: a
[[decision-trace]]; Dilger: a model). The same note also concedes something his enforcement-minded
material does not: real users *"are perfectly fine correcting things manually. Only engineers care
about absolutely consistent systems."*

And [[dilger-ux-as-first-class-in-spec-driven-development]] (2026-08-31) states the replacement
concretely: *"Instead of deriving the UX from markdown files ( which become unreadable and impossible
to maintain from a certain size on ), we focus on the functionality, the UX and the business rules
described as Given / When / Then ( BDD Style ). Spec-Driven Development does not need Markdown Files."*
So the division of labour is **screens carry the interaction, GWT carries the rules** — narrower and
more checkable than "use a DSL". Worked instance: [[dilger-ui-only-interactions-filtering]]. See
[[screens-as-specification]]. *(**VENDOR SELF-REPORT**; the demonstration is deferred to an
**uncaptured 60-minute webinar**, which is the fuller primary for this claim.)*

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

**A claim from the same author that *is* falsifiable (2026-09-03).** Selling his 3-week programme
([[dilger-agentic-engineer-program-stack-agnostic-spec]]), Dilger asserts stack independence:
*"The Implementation-Stack itself almost doesn't matter. Participants can pick one of the many Build
Kits available - #axon, #marten, #cratis, #emmet (node), #python… Fully taking advantage of the 'Spec'
in Spec-Driven-Development - they can even switch stacks mid-course or build in parallel in all
Stacks."* If one event model really drives builds in five runtimes at once, the model is a
specification of **behaviour** and not a description of an implementation — which is the whole
argument. **Nothing demonstrates it**; it is a course affordance, hedged by its own author
(*"almost doesn't matter"*), on a **VENDOR SELF-REPORT** marketing post.

Note what it collides with. This is precisely the aspiration
[[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler]] names and doubts — *"we could have AI fill
in all the solutioning and details, and switch to different tech stacks with the same spec"* — against
which her finding is that separating functional from technical spec is something *"we don't have a good
track record as a profession"* at. And Build Kits (stack-specific generators fed by a stack-agnostic
model) are **structurally the MDA architecture** that Tornhill and Böckeler both say failed. **This is
the most direct live test of the MDA-repeats objection the KB holds**, and it is the experiment nobody
has run: same requirements, one model, five stacks, measured output.

**Phase 4 update.** The hole is still a hole, but it now has one datapoint of framing rather than
none: Dilger's GOTO Copenhagen masterclass sells itself as *"From Requirements to Maintainable
Systems"* — *"AI can generate code in seconds. Maintaining and evolving that code is becoming the real
challenge"* ([[dilger-goto-cph-2026-event-modeling-ai-native-software-design]]). That is the frame
asserted in marketing copy for an event that had not yet run at ingest time. It fills nothing.

## The modelling version of the same objection (Tune, 2026-08-28)

Dilger's "describing without solving" and Ng's "reviewer, not builder" both say the artifact can exist
without the understanding behind it. [[nick-tune]] states the DDD form
([[tune-no-rapport-with-a-model-you-didnt-code]]): *"discussing and refining a domain model is not the
same as writing the lines of code yourself… **And that means the domain model is going to be worse**
because I'm clearly missing some nuances that could lead to big modelling breakthroughs."* And the
part that bites hardest on spec-first workflows: *"I'm struggling to see how to get the same level of
rapport with the model without actually writing the code. **Maybe it's not even possible.**"*

The premise this challenges is the one SDD needs to be true — that implementation is downstream of
understanding, so it can be delegated once the spec is right. Tune's claim is that implementation was
*generating* understanding, which is the same objection
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill's "SDD and the Illusion of Known
Scope"]] makes from the code side ("implementation is an essential part of the discovery process
itself"), now aimed at the model rather than the scope. It is **thin** (a short LinkedIn post; a
quality claim inferred from a stated feeling, unobservable by construction — a missed breakthrough
leaves no trace), and the KB's candidate reply is the one this page's Event-Modeling material already
implies: a spec the human *models* rather than merely *writes* keeps the thinking on the human's side —
[[event-modeling]], [[model-as-code-vs-model-as-language]]. See [[verification-burden]] and
[[comprehension-debt]].

## Open questions

The standing ask — *a production case study quantifying spec-first vs. prompt-first agent output* — is
**partially answered, against the thesis, and now grounded in the primary**:
[[eberhardt-putting-spec-kit-through-its-paces|Eberhardt's]] ~10x is the only such figure the KB holds,
and it remains one person, one hobby project, one toolkit, and a **self-reported impression rather than
a measurement**. Still open, and now more sharply: **nothing comparable exists for *model-first* SDD as
[[martin-dilger]] practises it**, so the 10x indicts document-generating toolchains and cannot be
transferred to [[event-modeled-agent-design]] — which is also the reason it is not a refutation of this
page.

**The new sharpest question: does the model-first route repeat MDA, or escape it?**
Two independent sources who worked with Model-Driven Architecture
([[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]],
[[bockeler-understanding-sdd-kiro-speckit-tessl]]) say the failure mode is that an executable model
bloats into the implementation and stops being readable, while gaining non-determinism and losing MDD's
one advantage (tool-checkable validity). Dilger's stack-agnostic Build Kit claim is the escape route he
asserts. **The experiment that would settle it exists and nobody has run it:** one model, several
stacks, measured output quality and model readability.

**And a question the sceptics raise that this page had not:** *what is the spec's maintenance strategy?*
Böckeler found it *"left vague or totally open"* in all three toolkits, and spec-kit branching per
change request rather than per feature suggests spec-*first* dressed as spec-anchored. That is
[[dilger-spec-driven-development-needs-four-phases|Dilger's phase 4]], still addressed by no captured
source.

Also open: **how do you tell a spec that records solved thinking from one that defers it?** Dilger names
the failure but offers no test beyond a felt sense. Ng supplies a provenance test — *was the author in
the room when the decisions were made?* — and Dilger independently endorses the same test in
[[dilger-only-engineers-care-about-consistent-systems]] ("one more handover"). **Adzic supplies a
third, and it is the most checkable of them:** *can a non-developer approve or complain about it?* His
objection to Spec Kit is that the real spec migrates into developer-only tests, which fails that test by
construction.

Also open: **if not a hand-authored prose spec, then what?** The replacements now number four, not two:
a formal modelling language ([[martin-dilger]]), the code with visualization on top
([[jeremy-miller]]), enforced structural constraints
([[nick-tune-enforced-application-architecture-agents-humans|Tune]]), or **nothing at all beyond a
small next increment** ([[zaninotto-spec-driven-development-waterfall-strikes-back|Zaninotto]],
[[eberhardt-putting-spec-kit-through-its-paces|Eberhardt]]). Tracked at
[[model-as-code-vs-model-as-language]].

_Sources: [[dilger-spec-driven-development-applied]] ·
[[dilger-faros-ai-report-amplifies-unclear-requirements]] · [[dilger-keep-command-handlers-pure]] ·
[[jwilger-agent-skills-event-modeling]] · [[dilger-model-is-a-living-spec-always-on-agent]] ·
[[fraktalio-event-modeler-connect-ai-agents-mcp]] · [[dilger-is-code-still-the-source-of-truth]] ·
[[dilger-harness-is-20-percent-requirements-are-80]] · [[dilger-user-stories-need-event-modeling-framework]] ·
[[dilger-drawio-model-in-code]] · [[dilger-flea-market-model-to-deploy]] · [[dilger-spec-driven-tools-need-event-modeling-front-half]] ·
[[dilger-describing-without-solving-burns-you-out]] · [[ng-spec-driven-development-is-waterfall-in-markdown]] ·
[[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]] · [[bockeler-understanding-sdd-kiro-speckit-tessl]] ·
[[zaninotto-spec-driven-development-waterfall-strikes-back]] · [[eberhardt-putting-spec-kit-through-its-paces]] ·
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]] · [[dilger-communicating-intent-to-an-agent-needs-a-dsl]] ·
[[dilger-ux-as-first-class-in-spec-driven-development]] · [[dilger-only-engineers-care-about-consistent-systems]] ·
[[dilger-agentic-engineer-program-stack-agnostic-spec]] · [[dilger-goto-cph-2026-event-modeling-ai-native-software-design]] ·
[[tune-no-rapport-with-a-model-you-didnt-code]]._
