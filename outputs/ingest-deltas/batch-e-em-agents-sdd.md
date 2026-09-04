# Ingest deltas — Batch E: Event Modeling × agents, and the spec-driven-development controversy

**Written 2026-09-04. 15 raw captures compiled into 15 source pages in `wiki/sources/`.**
This file is the work order for the orchestrator, who applies all entity/concept edits serially.
Nothing in `wiki/entities/`, `wiki/concepts/`, `wiki/index.md`, `wiki/overview.md` or `wiki/log.md`
was touched by this batch. **One `wiki/sources/` page belonging to an earlier batch needs a one-line
repair and was deliberately left alone — see §16.**

**Source pages written** (all with `raw_file:` set, all verified against the backlog query):

| Slug | Raw | Date |
| --- | --- | --- |
| `adzic-spec-driven-development-revenge-of-waterfall-or-bdd` | `raw/articles/…` | 2025-09-29 |
| `bockeler-understanding-sdd-kiro-speckit-tessl` | `raw/articles/…` | 2025-10-15 |
| `zaninotto-spec-driven-development-waterfall-strikes-back` | `raw/articles/…` | 2025-11-12 |
| `eberhardt-putting-spec-kit-through-its-paces` | `raw/articles/…` | 2025-11-26 |
| `nick-tune-event-sourced-claude-code-workflows` | `raw/articles/…` | 2026-03-04 |
| `tornhill-blast-from-the-past-sdd-illusion-of-known-scope` | `raw/articles/…` | 2026-05-28 |
| `dilger-loop-engineering-never-argue-with-agent` | `raw/articles/…` | 2026-06-10 |
| `dilger-ui-only-interactions-filtering` | `raw/articles/…` | 2026-07-31 |
| `dilger-goto-cph-2026-event-modeling-ai-native-software-design` | `raw/articles/…` | date unresolved (runs 2026-09-28/29) |
| `dilger-podcast-episode-47-agentic-modeling-audit-trails` | `raw/articles/…` | **DATE UNRESOLVED** |
| `dilger-ux-as-first-class-in-spec-driven-development` | `raw/notes/…` | 2026-08-31 |
| `dilger-only-engineers-care-about-consistent-systems` | `raw/notes/…` | 2026-09-01 |
| `dilger-git-as-primary-persistence-for-event-models` | `raw/notes/…` | 2026-09-02 |
| `dilger-communicating-intent-to-an-agent-needs-a-dsl` | `raw/notes/…` | 2026-09-03 |
| `dilger-agentic-engineer-program-stack-agnostic-spec` | `raw/notes/…` | 2026-09-03 |

**Delta items: 50** — **38 concept UPDATE items across 13 pages** (§1–§6, §8–§14, including three
frontmatter items), **1 concept CREATE** (§7), **6 entity UPDATEs + 4 entity CREATEs** (§15), and
**1 `sources/` citation repair** (§16). §17 (index/log) is listed for convenience but this batch does
not own those files.

**If you are triaging, do these seven first:** §1.1 (the weak/strong ladder — the vocabulary everything
else needs), §1.2 (the Adzic misattribution, the only place the KB currently misrepresents someone),
§1.3 + §14 + §16 (the same mis-piped Tornhill wikilink in three files), §1.5 (requirements explosion —
the strongest objection the page lacks), §2.1 (the MDA precedent), §4.1 (the 2026-06-10 date
correction), §15.1 (the Adzic entity repair).

**Standing instruction for every paste below.** The interested-claim markers are *inside* the pasted
text on purpose. Do not strip them when placing the text, and do not let a figure travel to a third
page without its marker. §0 lists every number and framing in this batch that must not be promoted.

---

## 0. Claims this batch refused to promote — apply on any page that cites them

Not a page edit. A checklist for the fidelity pass and for any future page that reaches for these.

| Claim | Source page | Why it is not a datum |
| --- | --- | --- |
| "around ten times faster" without SDD | `eberhardt-putting-spec-kit-through-its-paces` | **IMPRESSION NOT MEASUREMENT.** His own words, n=1, one hobby app, one toolkit, no control for ordering or for the fact that he had already built the feature once. Never render as a rate or a benchmark. |
| 33m30 agent / 3.5 hrs review / 2,577 lines md / 689 loc | same | Real instrument readings from **one run**, self-instrumented, no repetition. The **Tasks step's statistics block duplicates the Plan step's verbatim** in the original, so the per-step totals are approximate and Tasks is effectively unreported. |
| "2,500 lines of Markdown in the spec phase" | (the KB's old figure) | **WRONG and already corrected.** 2,577 is the *cumulative* total for the whole feature; Specify alone was **230** lines; Plan was the bloated step at **2,067**. |
| "1,300 lines of Markdown to display a date", 8 files | `zaninotto-spec-driven-development-waterfall-strikes-back` | Real and linked to a public PR — but **someone else's PR**, relayed. Re-cite to Zaninotto, not to "Augment Engineer" via Ng. |
| "spending 80% of your time reading instead of thinking" | same | **IMPRESSION.** He labels it *"in my opinion"*. A percentage in rhetoric, not a measurement. |
| "about 10 hours" to build the 3D sculpting tool with no spec | same | **NOT INDEPENDENT · self-report.** His own weekend project, on his own company's blog, as the counter-example to the thing he is arguing against. |
| 4 user stories / 16 acceptance criteria for one small bug | `bockeler-understanding-sdd-kiro-speckit-tessl` | An **artifact count**, not an outcome. Verified verbatim against the primary. |
| "in the same time it took me to run and review spec-kit I could have implemented the feature" | same | **IMPRESSION NOT MEASUREMENT**, and **NOT INDEPENDENT** (martinfowler.com is Thoughtworks' own channel; Böckeler is a Thoughtworks Distinguished Engineer). |
| "for every 10-percent increase in problem complexity, there is a 100-percent increase in the software solution's complexity" | `tornhill-blast-from-the-past-sdd-illusion-of-known-scope` | **Robert Glass's assertion as relayed by Tornhill**, attributed to no specific work, measured by nobody in the citation chain. Never write "research shows". |
| "intention-revealing design + automated safeguards for our code and its behavior" as the alternative | same | **NOT INDEPENDENT** — Tornhill is founder/CTO of CodeScene and that is his product's category. The piece contains **no figures at all**. |
| "15 minutes in RESPAWN vs 2 minutes DEVELOPING"; "I've seen great results on real projects" | `nick-tune-event-sourced-claude-code-workflows` | **IMPRESSION NOT MEASUREMENT · NOT INDEPENDENT.** Instrument readings from one session of his own harness on a personal project; he states the scoping himself. The "great results" claim carries no number. |
| "battle-tested over hundreds of projects by many companies" (Event Modeling as a DSL) | `dilger-communicating-intent-to-an-agent-needs-a-dsl` | **VENDOR SELF-REPORT · his own figure.** No project, company or method named. **No independent corroboration exists anywhere in this KB.** |
| "as I did for hundreds of engineers already" | `dilger-loop-engineering-never-argue-with-agent` | **VENDOR SELF-REPORT** for a paid training service. |
| "Clean iterations … will outperform long, polluted conversations every single time. Not sometimes. Every time." | same | Stated absolutely with **zero evidence**. Carry as a position, never as a finding. Its mechanism claim (polluted context ⇒ hallucination) is asserted, not demonstrated. |
| "it was indistinguishable from modeling with humans" (two agents modelling) | `dilger-podcast-episode-47-agentic-modeling-audit-trails` | **IMPRESSION NOT MEASUREMENT · VENDOR SELF-REPORT.** A felt comparison on his own platform; also **show-notes level, not verified against audio**. |
| "100 comments" → "genuinely useful" after tuning `/wdyt` | same | Impressions, not counts to compare. |
| Episode 47's date | same | **UNRESOLVED. Do not assign one.** No date in HTML, metadata or body. Absent from the RSS feed and from podcast.eventmodeling.org (both still end at **Ep 46, 2026-04-26/27**), so it post-dates 2026-04-27 and nothing more can be said. **And it may be a channel prior sweeps never polled rather than a new item** — `eventmodelers.ai/docs/podcast` is a separate, more current index than the `.org` one. Any page citing it must say so. |
| "Fully taking advantage of the 'Spec'… they can even switch stacks mid-course or build in parallel in all Stacks" | `dilger-agentic-engineer-program-stack-agnostic-spec` | **VENDOR SELF-REPORT · marketing.** A course affordance, hedged by its own author (*"almost doesn't matter"*), demonstrated nowhere. High-value *claim*, zero evidence. |
| GOTO Copenhagen masterclass (11,000 DKK, two days) | `dilger-goto-cph-2026-event-modeling-ai-native-software-design` | **Distribution, not efficacy.** Marketing copy for a paid engagement that, at ingest time, **has not happened yet**. Publication date unresolved. |
| "We are doing this for years - because it works" (UX first-class) | `dilger-ux-as-first-class-in-spec-driven-development` | **VENDOR SELF-REPORT**, and the demonstration is deferred to an **uncaptured 60-minute webinar**. |
| Screen Preview, Multi-Screen Views, HTML Views, git backend, BYODS, WORM auditability | Dilger notes/articles | **VENDOR SELF-REPORT** — all EM-Studio features. The git backend is announced as *being added*, not reported in use. |

**Provenance rule for the four SDD primaries.** Adzic (2025-09-29) → Böckeler (2025-10-15) → Zaninotto
(2025-11-12) → Eberhardt (2025-11-26) → **Ng (2026-03)**. Zaninotto cites Böckeler; Eberhardt cites
Böckeler; Tornhill (2026-05-28) cites Böckeler. **Ng is the downstream synthesis, not the origin**, and
every figure the KB has been citing through Ng should now be re-cited to its primary.

**LinkedIn short-form rule for this batch.** Five of the fifteen are LinkedIn notes and three of them
restate something longer: `dilger-ux-as-first-class-in-spec-driven-development` is a trailer for an
**uncaptured 60-minute webinar** (that is the fuller primary);
`dilger-communicating-intent-to-an-agent-needs-a-dsl` sharpens
`dilger-markdown-is-a-suggestion-dressed-as-a-spec` (2026-08-25) and rests on an **uncaptured 2024 JSON
format document**; `dilger-agentic-engineer-program-stack-agnostic-spec` sells the same curriculum as the
GOTO masterclass listing. `dilger-git-as-primary-persistence-for-event-models` and
`dilger-only-engineers-care-about-consistent-systems` have no fuller primary and are the only sources
the KB has for their content.

---

## 1. `wiki/concepts/spec-driven-development.md` — UPDATE (9 items)

**This is the batch's largest and most important target.** The page's own 2026-08-31 correction block
says its Ng section *"awaits a rewrite, because that is the ingest's job, not a lint's."* **This is that
ingest.** Do items 1.1 → 1.3 in order; they replace and repair, and the rest are additive.

### 1.1 — CREATE a new section defining the weak/strong ladder, and put it early

**Why:** the page argues about "SDD" as one thing across four critics who are each aiming at a different
rung. Böckeler's taxonomy is the vocabulary the whole dispute needs, it is now a captured primary, and
Tornhill and Eberhardt both explicitly use it to scope their own arguments. Without it the page reads as
if the sceptics are attacking Dilger's position; mostly they are not.

**Where:** insert as a new `##` section immediately **after** `## The core argument` and **before**
`## Relationship to the rest of the KB`.

**Paste:**

```markdown
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
```

### 1.2 — REPLACE the Adzic misattribution block with the corrected account

**Why:** the primary is now captured and the block itself asks to be replaced. Adzic is currently the
one voice on this page whose position is materially misrepresented, and the correction runs the *other*
way from the page's framing — he is the warmest of the four critics, not a hostile one.

**Where:** in `## The outside-in critique — and the numbers pointing the other way (Ng, 2026-03)`,
find the bullet at line ~163 beginning **`- **[[gojko-adzic]]**, from inside the BDD tradition — *but see the correction below*:`** together with the
whole `> **⚠ Misattribution, corrected 2026-08-31.**` blockquote that follows it, and **replace both**
with:

**Paste:**

```markdown
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
```

### 1.3 — REPAIR a mis-piped wikilink (the label and the target are different articles)

**Why:** the page cites *SDD and the Illusion of Known Scope* through a pipe onto
`tornhill-merge-conflicts-agentic-bottleneck`, which is a **different Tornhill article** (about merge
conflicts). The real source page now exists. This is a citation-integrity bug, and it appears in three
more places (see §14, §15.2, §16).

**Where:** in `## The failure mode, named by its own evangelist (Dilger, 2026-08-14)`.

**Find:** `[[tornhill-merge-conflicts-agentic-bottleneck|Tornhill's "SDD and the Illusion of Known Scope"]]`

**Replace with:** `[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill's "SDD and the Illusion of Known Scope"]]`

### 1.4 — REWRITE the empirical-record list from the primaries

**Why:** the block is the page's evidence base and every entry in it is currently secondhand through
Ng, with a chronology-correction banner on top saying so. All four primaries are now source pages.
Replace the relayed list with a grounded one and **delete the banner**, since its job is done.

**Where:** in `## The outside-in critique — and the numbers pointing the other way (Ng, 2026-03)`.
Delete the opening `> **⚠ Chronology correction, 2026-08-31 …**` blockquote entirely. Then replace the
list items for **Scott Logic**, **Böckeler's Kiro analysis**, **Augment Engineer** and **Marmelab**
with the text below. (Leave the Adzic bullet as replaced in 1.2, and leave contribution **2** — the
interface/authorship argument — untouched; it is Ng's own and still stands.)

**Paste:**

```markdown
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
  **Natural Language Development**.
```

### 1.5 — CREATE a section for the strongest objection on the page: requirements explosion

**Why:** the page's critique material is currently all about *artifact volume and provenance*. Tornhill
supplies a **different and deeper objection** that no other source makes, and it is aimed precisely at
the KB's own end of the ladder. It deserves its own section, not a bullet.

**Where:** insert as a new `##` section immediately **after** the (now-rewritten)
`## The outside-in critique — and the numbers pointing the other way (Ng, 2026-03)` section and
**before** `## "Requires suitable language" — and the counter-position (2026-08)`.

**Paste:**

```markdown
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
```

### 1.6 — EXTEND the "requires suitable language" section with the DSL claim

**Why:** the page has Dilger's position as "prose is the wrong language". His three September notes
sharpen it into a claim about the **medium of specification** with a named replacement, and one of them
supplies the batch's most quotable line. This is the Dilger side of
[[model-as-code-vs-model-as-language]] the page currently states only by inference.

**Where:** in `## "Requires suitable language" — and the counter-position (2026-08)`, immediately
**after** the paragraph beginning **"**[[martin-dilger]]** answers with a formal modeling language"**
and its quoted ratio test, **before** the `**[[jeremy-miller]]** answers with…` paragraph.

**Paste:**

```markdown
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
```

### 1.7 — ADD the stack-agnostic claim to the four-phases section as the thesis's sharpest live test

**Why:** the page's standing complaint about Dilger is that his claims are unfalsifiable reframings.
This one **is** falsifiable, it is the strongest form of the spec-as-specification claim, and it lands
exactly on the MDA-repeats objection added in 1.5.

**Where:** at the end of `## The scoping counter-argument — SDD needs four phases (Dilger, 2026-08-29)`,
after the third observation bullet (*"Phase 4 is a genuine hole in this KB"*).

**Paste:**

```markdown
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
```

### 1.8 — REWRITE the "Open questions" section

**Why:** two of the three standing questions are changed by this batch, and one new one is now the
sharpest thing on the page.

**Where:** replace the whole `## Open questions` section body (keep the heading).

**Paste:**

```markdown
The standing ask — *a production case study quantifying spec-first vs. prompt-first agent output* — is
**partially answered, against the thesis, and now grounded in the primary**:
[[eberhardt-putting-spec-kit-through-its-paces|Eberhardt's]] ~10x is the only such figure the KB holds,
and it remains one person, one hobby project, one toolkit, and a **self-reported impression rather than
a measurement**. Still open, and now more sharply: **nothing comparable exists for *model-first* SDD as
[[martin-dilger]] practises it**, so the 10x indicts document-generating toolchains and cannot be
transferred to [[event-modeled-agent-design]] — which is also the reason it is not a refutation of this
page.

**The new sharpest question, from this batch: does the model-first route repeat MDA, or escape it?**
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
```

### 1.9 — Frontmatter

**Where:** `sources:` list. **Add:** `adzic-spec-driven-development-revenge-of-waterfall-or-bdd`,
`bockeler-understanding-sdd-kiro-speckit-tessl`,
`zaninotto-spec-driven-development-waterfall-strikes-back`,
`eberhardt-putting-spec-kit-through-its-paces`,
`tornhill-blast-from-the-past-sdd-illusion-of-known-scope`,
`dilger-communicating-intent-to-an-agent-needs-a-dsl`,
`dilger-ux-as-first-class-in-spec-driven-development`,
`dilger-only-engineers-care-about-consistent-systems`,
`dilger-agentic-engineer-program-stack-agnostic-spec`,
`dilger-goto-cph-2026-event-modeling-ai-native-software-design`.
Set `updated: 2026-09-04`. Append the new source pages to the trailing `_Sources: …_` line.

---
## 2. `wiki/concepts/model-as-code-vs-model-as-language.md` — UPDATE (5 items)

**Why this page matters most after §1:** the batch adds a **fourth voice on the model-as-code side**
(Eberhardt, and his is the only *empirical* statement of it), the **strongest external historical
argument against the model-as-language side** (Böckeler's MDD paragraph, Tornhill's MDA experience),
and **the name of the thing Dilger's camp is asking for** (a DSL for flow, behaviour and business
rules). The page's central open question — *has anyone run the comparison?* — now has a concrete
experimental design attached.

### 2.1 — CREATE a section for the MDA/MDD precedent

**Why:** the page currently has no historical dimension at all. Two independent 2025–26 sources reach
for the same precedent, and it cuts across both columns rather than joining one.

**Where:** insert as a new `##` section immediately **after** `## Where they actually agree` and
**before** `## Why the disagreement matters here`.

**Paste:**

```markdown
## The precedent both camps have to answer: MDA / MDD (2025–26)

Two sources arrive independently at the same historical analogy, and it is the strongest external input
this page has received.

**[[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler]]** (2025-10-15) worked on model-driven
development projects early in her career and Tessl's spec-as-source design reminded her of them: MDD
models *were* specs — UML or a textual DSL — fed to hand-built code generators. Her verdict is
double-edged, and both edges land here:

> "Ultimately, MDD never took off for business applications, it sits at an awkward abstraction level and
> just creates too much overhead and constraints. But LLMs take some of the overhead and constraints of
> MDD away… With LLMs, we are not constrained by a predefined and parseable spec language anymore, and
> we don't have to build elaborate code generators. The price for that is LLMs' non-determinism of
> course. **And the parseable structure also had upsides that we're losing now: We could provide the
> spec author with a lot of tool support to write valid, complete and consistent specs.** I wonder if
> spec-as-source, and even spec-anchoring, might end up with the downsides of both MDD and LLMs:
> Inflexibility and non-determinism."

*(**NOT INDEPENDENT** — martinfowler.com is [[thoughtworks]]' own channel and Böckeler is a Thoughtworks
Distinguished Engineer.)*

Read carefully, that paragraph is **evidence for both columns**. Against
[[martin-dilger|model-as-language]]: MDA is the precedent for a formal model that failed on abstraction
level and overhead. *For* it: **a parseable structure buys tool support for validity and
completeness** — precisely the property Dilger's structural-diff rubric exploits
([[dilger-one-million-tokens-self-training-modeling-agent]]) and precisely what natural-language SDD
threw away. Her framing is the sharpest statement anywhere of what the model-as-language camp is *for*,
written by someone sceptical of it.

**[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill]]** (2026-05-28) supplies the
lived version, and it is a warning about a specific failure trajectory rather than about modelling as
such. Hand-drawn UML plus a design review **worked** and paid off for onboarding and extension. Then the
vendors closed the loop with an "action language" so all code could be generated, and *"the first victim
was the documented design. The executable diagrams turned so bloated and verbose that they became
literally incomprehensible. After all, the new audience was a compiler, not humans."* The tooling
regressed with it — no pipelines, CLIs, IDEs, linters: *"Imagine coding in a Microsoft Word document."*
His closing rule is the page's hardest test:

> "The moment a model becomes the implementation, it ceases to be a good model."

**How each column has to answer it:**

- **Model-as-language** must show its artifact stays at a *different* level of abstraction from the code
  while still being complete enough for generation. Dilger's answers are the **Build Kits** (stack-
  specific generators fed by a stack-agnostic model) and the claim that the model *"almost doesn't
  matter"* which stack it drives ([[dilger-agentic-engineer-program-stack-agnostic-spec]]) — which is
  structurally the MDA architecture. Tornhill's tooling objection, at least, is answered directly by
  [[dilger-git-as-primary-persistence-for-event-models|git-as-primary persistence]]: the model gets the
  whole git toolchain instead of a vendor design tool.
- **Model-as-code** is arguably what Tornhill's *first* employer had and liked — a readable diagram
  alongside code, not generating it. [[jeremy-miller]]'s derived-visualisation design is the modern form
  of the thing that worked, which is the strongest lineage argument available to him and one he does not
  make.
```

### 2.2 — ADD Eberhardt as a fourth voice, in the Model-as-Code case section

**Why:** the page notes Miller's case is *"from lineage and cost, not from principle."* Eberhardt makes
the **principled** version and backs it with the only instrumented run in the material — and he is not
in the .NET/JasperFx orbit, so he is genuinely a second, independent statement of the position.

**Where:** at the end of `## The Model-as-Code case`.

**Paste:**

```markdown
**A second, independent statement of this position — and the only instrumented one
([[eberhardt-putting-spec-kit-through-its-paces|Eberhardt]], 2025-11-26).** Where Miller argues from
cost and lineage, Colin Eberhardt (CTO, [[scott-logic]]) argues from formality, having rebuilt a
deleted ~1,000-line feature with Spec Kit and measured every step:

> "Code is law because it is formal language you can reason about. You can test it. You can prove it is
> right or wrong. Specifications, or at least ones expressed in the markdown format of Spec Kit, lack
> this formality. **They are not a law I would put my trust in.**"

He adds two arguments neither camp on this page had made. **(1) Training-distribution:** code is a far
larger share of a model's training data and a language it can reason about, so *"asking an agent to write
1000s of lines of markdown rather than just asking it to write the code is a misuse of this technology"*
(he concedes this is not compelling on its own). **(2) Cheap code changes the economics of the whole
question:** *"Code is now cheap; we can create it quickly and throw it away just as fast. Spec Kit, and
SDD, don't capitalise on this."* If code is disposable, the artifact worth authoring and keeping is the
**decision record** ([[adr]], [[decision-trace]]) — *"code can give you the 'what', but cannot tell you
the 'why'"* — and not the requirement.

**Where it collides with Dilger, precisely.** Both agree code is a formal language. Dilger's objection is
that it is formal about the wrong thing — implementation rather than **behaviour over time** — and that
the business cannot review it. Eberhardt's rejoinder is not that behaviour doesn't matter but that a
*markdown* spec has no formality to trade for, and *"in most development processes specifications are a
point-in-time tool for steering implementation. Once complete, and fully tested, how often do you
re-visit a user story?"* That last point is the one thing on this page that argues against
**spec-anchoring itself**, independent of notation.

*(**IMPRESSION NOT MEASUREMENT** for his "around ten times faster"; n=1, his own hobby app, and he had
already built the feature once. **NOT INDEPENDENT** in the weak sense that both arms of the comparison
are his own work. His own stated defences travel with the figures: Spec Kit is immature, *"I am willing
to entertain the possibility that I am simply just using it wrong"*, and he wonders whether a
"vibe engineer" is even the target audience.)*
```

### 2.3 — SHARPEN the Model-as-Language case with the DSL requirement

**Why:** the page states Dilger's position as a rejection of prose plus a preference for Event
Modeling. He has now named the missing *thing* and given four properties it must have, which is what
makes the position comparable to Miller's rather than merely opposed to it.

**Where:** in `## The Model-as-Language case`, immediately after the blockquote of the 2026-08-25
"Markdown we use is a suggestion" passage.

**Paste:**

```markdown
He names the missing artifact nine days later
([[dilger-communicating-intent-to-an-agent-needs-a-dsl]], 2026-09-03):

> "Somehow the software industry has chosen raw markdown as the medium of choice… **What's missing is a
> DSL to unambiguously describe flow, behavior + business rules.** … The medium itself - nobody cares in
> the end ( you can export Json, Markdown, Toon.. from my tools ). … For me, Eventmodeling is that DSL."

Two clarifications this forces onto the table above. **First, his target is the *language*, not the file
format** — he says explicitly that his tools export markdown and that the medium is irrelevant, so the
framing caution at the top of this page applies to him too: this is not an anti-markdown-file position.
**Second, he states four properties an agent-facing spec must have** — *specific, unambiguous,
information complete, structured* — which is the closest thing the KB has to a testable statement of the
model-as-language requirement. They are asserted, not defended. And the supporting claim is his own:
*"Battle-tested over hundreds of projects by many companies"* (**VENDOR SELF-REPORT, his own figure, no
project or company named, no independent corroboration anywhere in this KB**), resting on a **2024 JSON
interchange format that is not captured in `raw/`**.

Note that this puts Dilger and [[jeremy-miller|Miller]] in flat contradiction on the *category*, not
just the artifact: Miller rejects *"intermediate DSL approaches… using YAML, XML, or custom built textual
DSLs"* by name, and Dilger asks for exactly one.
```

### 2.4 — EXTEND the third-position section: Tune's own boundary

**Why:** the page presents Tune as the model-as-constraint position. His event-sourced-workflow post
shows *how far he will go with automation* and his rapport post shows *where he stops* — which converts
his position from "a third notation" into "a claim about which layers may be delegated". That is a
sharper reading and the page should carry it.

**Where:** at the end of `## A third position: model-as-constraint (added 2026-09-02)`, before the
`*Sourcing note: …*` line.

**Paste:**

```markdown
**Where Tune himself draws the line (added 2026-09-04).** Two further captures from the same author bound
the position from both sides. In [[nick-tune-event-sourced-claude-code-workflows]] (2026-03-04) he
event-sources his own Claude Code workflow so the log yields per-state timings, rejection counts and
hook-denial counts, then **feeds those events back to Claude to have it rewrite the harness** — maximal
delegation of the *process*. In [[tune-no-rapport-with-a-model-you-didnt-code]] (2026-08-28) he doubts he can build rapport with a domain model he did not hand-code:
*"the domain model is going to be worse because I'm clearly missing some nuances that could lead to big
modelling breakthroughs… Maybe it's not even possible."*

So his position is not "constraints instead of a model" but **"delegate and instrument the loop; author
the domain model yourself."** That is a boundary claim, and it cuts against the model-as-language camp's
strongest ambition — that a good enough DSL lets agents do the modelling
([[dilger-podcast-episode-47-agentic-modeling-audit-trails|two agents modelling alongside him,
"indistinguishable from modeling with humans"]] — **IMPRESSION NOT MEASUREMENT, VENDOR SELF-REPORT**).
It also happens to be the same boundary [[bockeler-tdd-inside-the-agent-loop]] and
[[dilger-describing-without-solving-burns-you-out]] land on from opposite directions: own the problem,
delegate the process.
```

### 2.5 — UPDATE the "Open questions" section with the experiment that would settle it

**Where:** in `## Open questions`, replace the first bullet (*"Has anyone run the comparison
directly…"*) with:

**Paste:**

```markdown
- Has anyone run the comparison directly — same requirements, model-first vs
  code-first-with-visualization, measured on agent output quality? Nothing in the KB does. **But the
  experiment now has a concrete design, supplied by the model-as-language camp itself:** Dilger claims
  one event model drives builds in five runtimes via Build Kits, with participants free to *"switch
  stacks mid-course or build in parallel in all Stacks"*
  ([[dilger-agentic-engineer-program-stack-agnostic-spec]] — **VENDOR SELF-REPORT, marketing, hedged as
  *"almost doesn't matter"*, demonstrated nowhere**). A model-as-code artifact is derived from *one*
  implementation and structurally cannot have that property, so **one model, five stacks, measured
  output** is the discriminating test. It is also the test
  [[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler]] predicts will fail, on the grounds that
  separating functional from technical spec is something *"we don't have a good track record as a
  profession"* at.
- Does either camp survive the MDA precedent (§ *The precedent both camps have to answer*)? Tornhill's
  *"the moment a model becomes the implementation, it ceases to be a good model"* is a constraint on
  Dilger's generation route; Böckeler's *"the parseable structure also had upsides that we're losing"*
  is a point in its favour. Neither camp has answered either.
```

### 2.6 — Frontmatter

**Add to `sources:`** `bockeler-understanding-sdd-kiro-speckit-tessl`,
`eberhardt-putting-spec-kit-through-its-paces`,
`tornhill-blast-from-the-past-sdd-illusion-of-known-scope`,
`dilger-communicating-intent-to-an-agent-needs-a-dsl`,
`nick-tune-event-sourced-claude-code-workflows`,
`dilger-agentic-engineer-program-stack-agnostic-spec`,
`adzic-spec-driven-development-revenge-of-waterfall-or-bdd`. Set `updated: 2026-09-04`.

---

## 3. `wiki/concepts/event-modeled-agent-design.md` — UPDATE (5 items)

### 3.1 — CREATE a section for the agent-as-model-reviewer evidence, and its new limit

**Why:** the page's "third direction of fit — agent *critiques* the model" currently rests on the
`/wdyt` announcement. Episode 47 gives a **worked interaction** *and* a **tuning failure**, and the
failure is the more valuable half: it is the first evidence in the KB that an agent grading a spec can
make the spec worse.

**Where:** insert as a new `##` section immediately **after**
`## The model as *rubric*, not just as spec (Dilger, 2026-08) — the missing evidence` and **before**
`## The sharpest external challenge: whose model is it? (Ng, 2026-03)`.

**Paste:**

```markdown
## Agents modelling *with* you, and the over-specification failure (Ep 47, date unresolved)

[[dilger-podcast-episode-47-agentic-modeling-audit-trails]] pushes two rungs of this page forward and
puts a real limit on a third.

> **⚠ The date of this source is unresolved and must stay that way.** The page carries no publication
> date in HTML, metadata or body. Ep 47 is **absent from the podcast RSS feed and from
> podcast.eventmodeling.org**, both of which still end at **Ep 46 (2026-04-26/27)**, so it post-dates
> 2026-04-27 and nothing further can be established. It announces [[golo-roden]] for an *"already
> sold-out"* conference and the site banner reads *"September cohort sold out"*. **It may well be a
> channel prior sweeps never polled** (`eventmodelers.ai/docs/podcast` is a separate, more current index
> than the `.org` one) **rather than a genuinely new item.** Also **show-notes level, not verified
> against audio**, and **VENDOR SELF-REPORT** — the platform and the skill are Dilger's products.

**Agents as co-modellers.** Dilger ran a Claude Code instance and a **Hermes** agent modelling alongside
him simultaneously, adding slices and comments, and reports it *"was indistinguishable from modeling
with humans"* — **IMPRESSION NOT MEASUREMENT**, and a felt comparison rather than an evaluation, but the
furthest the agent-authors-the-model rung has gone.

**The `/wdyt` skill, worked.** The agent reads the slices and **posts clarifying-question comments on
them**: *"He commented on the slice and asked: well, what happens if a user clicks this twice? What
should be the behavior? … And this is perfectly valid — a perfectly valid question."* Note the shape:
the agent's output is a **question on the artifact**, not an edit to it — a model-level review gate
above the code-level [[given-when-then|GWT]] gates.

**And the failure, which is the transferable finding.** The first version *"flooded the model with 100
comments inventing hypothetical gaps."* The fix was a restriction: *"don't just look at what is there —
don't comment on something because it's not specified. Just look at what is there and make sense of it,
then give me comments. And then it got significantly better."* [[adam-dymitruk]] adds why it matters
more here than in code review: an over-eager agent flooding a GWT list with edge cases *"can make a
simple slice look far more complex than it really is, since event modeling is visual"* — so the noise
does not merely waste attention, it **degrades the artifact's primary affordance**. The method's own
answer predates the tooling: *"event modeling already solves the 'infinite possibility tree' problem:
draw a few representative example paths and trust the implementer to infer the rest."*

**What this costs the model-as-rubric optimism above.** The rubric section argues a schema'd model makes
agent output gradeable. This shows the converse risk: **an agent pointed at a spec can inflate it**, and
the inflation is invisible to a structural diff (a bloated slice is still well-formed). It is the same
mechanism [[bockeler-tdd-inside-the-agent-loop|Böckeler]] found one altitude down — an agent inventing
its own acceptance criteria — and the same remedy applies: **the criteria must come from outside the
loop.** See [[event-modeling-anti-patterns]] for the anti-pattern this creates.
```

### 3.2 — ADD Nick Tune to the "what's solid vs open" ladder, as the seam inverted

**Why:** this page's whole question is "can Event Modeling design agent systems?" Tune answers a
neighbouring question nobody in the KB had answered: **event-source the agent loop itself.** It is the
closest published thing to a worked event-driven model *of* a harness, and the page's standing "wanted
next" should say so precisely — including why it still doesn't close the gap.

**Where:** in `## What's solid vs. open`, immediately **before** the
`- **Adjacent cross-check (captured):**` bullet.

**Paste:**

```markdown
- **The seam, inverted — event sourcing on the agent loop (2026-03-04).**
  [[nick-tune-event-sourced-claude-code-workflows]] models a Claude Code workflow as a state machine
  (DEVELOPING → REVIEWING → COMMITTING → RESPAWNING) and persists **only the events**, deriving state by
  replay in SQLite. The payoff is entirely observational: per-state dwell times, **rejection counts**
  (review failed) and **hook-denial counts** (the agent attempted something disallowed in that state),
  a journal enforced at ≥1 entry per iteration by hard blocks, and the events fed **back to Claude** to
  propose CLAUDE.md or system-prompt changes. His reading of one session — *"my agents spent 15 minutes
  in the RESPAWN state whereas they only spent 2 minutes actually building the feature"* — is an
  instrument reading from **one session of his own personal-project harness, and he says so**
  (**IMPRESSION NOT MEASUREMENT · NOT INDEPENDENT**). He scopes the value honestly: it pays off for
  autonomous loops, not for chatbot-style or hand-held sessions, and *"if we get to that point [where
  workflows just work], the observability and analysis doesn't provide any value."*

  **Why it matters to this page and why it does not close the gap.** This is *not* an event model of a
  multi-agent system in the Dymitruk sense — no swimlanes, no commands, no read models, no timeline
  notation — so the standing "wanted next" (a **worked event model of a harness**, using the method)
  stays open. What it *is*, is the first published system where the **agent loop's own history is the
  source of truth**, which makes it the nearest empirical cousin of this page's central mapping and the
  strongest evidence that treating agent runs as an event stream buys something concrete. Note also the
  boundary the same author draws: he instruments and automates the **loop** while doubting he can
  delegate the **domain model** at all ([[tune-no-rapport-with-a-model-you-didnt-code]],
  2026-08-28) — which is a direct challenge to the claim that a good
  enough DSL lets agents do the modelling work.
```

### 3.3 — ADD the git-persistence rung to the file-format section

**Where:** at the end of `## The file-format + linter rung (ESDM, 2026-07)`.

**Paste:**

```markdown
**The persistence rung (2026-09-02).** [[dilger-git-as-primary-persistence-for-event-models]] makes
**git a primary store for the model, not an export**: one repository per board, branching supported,
under a "BYODS — bring your own datastore" design (Redis, S3, YAML, SharePoint all named), with
*"you can store your models in a Worm-Drive for auditability."* Two consequences for this page. **(1) It
collapses the file-first-vs-board+MCP framing entirely** — the board *is* files, so an agent can read
the model and its whole history with ordinary git tooling, and **model↔code drift becomes a diff between
two repos** rather than a bespoke check. Compare [[dilger-drawio-model-in-code]], where model-in-git was
right but raw XML gave the agent *"no framework to follow, no rules"*; this is that idea with a schema
and a platform behind it, and [[esdm-event-sourced-domain-modeling|ESDM]]'s file-first position reached
from the hosted-board side. **(2) Branching a *specification* is new**, and it is the natural pairing
for a fleet of agents claiming slices off one board
([[dilger-loop-engineering-never-argue-with-agent]]) — though nothing in the source says how a
two-dimensional board serialises for meaningful diffs, what happens when two agents diverge on the same
slice, or how branching interacts with the claim-lock. *(**VENDOR SELF-REPORT** — EM-Studio is Dilger's
own platform, and the git backend is **announced as being added, not reported in use**.)*
```

### 3.4 — EXTEND the Ng-challenge section with the batch's partial answers and one new challenge

**Where:** at the end of `## The sharpest external challenge: whose model is it? (Ng, 2026-03)`.

**Paste:**

```markdown
**What this batch adds to the answer (2026-09-04), and it is partial in a specific way.** Three captures
bear directly on the flattening objection. [[dilger-only-engineers-care-about-consistent-systems]]
reaches **Ng's own diagnosis from the opposite camp** — every hop between end user and engineer reshapes
the requirement, and *"now with AI - we are just adding one more hop to the chain. Engineers talking to
AI, writing tons of markdown.. one more handover"* — and prescribes calling the end user and then
*"invit[ing] them to a short Event Modeling Session. Show them what you planned, show them the screens
you sketched."* [[dilger-ux-as-first-class-in-spec-driven-development]] and
[[dilger-ui-only-interactions-filtering]] supply the mechanism: **the screen is the artifact a
non-developer can react to**, and it is in the model rather than derived from it (see
[[screens-as-specification]]). Ep 47 adds Dymitruk's blunt version: *"all the arguments about not having
screens and design sessions is just gatekeeping by architect wannabes."*

That is a real answer to *"nobody will open a `.specify` folder"* — a sketched screen needs no folder.
It is **not** an answer to *"nobody else signed it"*: the KB still holds **no captured source measuring
stakeholder participation in a model that later drove agents**, and every one of these sources is
[[martin-dilger]] on his own platform (**VENDOR SELF-REPORT**). The gap named on this page stands; what
changes is that the camp now has a stated mechanism rather than only a claim about workshop practice.

**And a second external challenge, sharper for this page than Ng's.**
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill's]] requirements-explosion argument
says each specified requirement spawns *tens of implicit design requirements* that cannot be known up
front, because **implementation is the discovery process** — so the acceptance-gate story on this page
(GWT scenarios as the machine-checkable contract an agent must satisfy) is checking the small share of
decisions that were specifiable. His obstacle (3) closes the obvious escape: enrich the model until it
resolves the implicit decisions and *"the moment a model becomes the implementation, it ceases to be a
good model."* Note this is **not** the waterfall objection — he explicitly declines that — and it is
aimed at strong-form [[spec-driven-development|SDD]], which is where this page sits. The KB has no
answer to it, and no captured source even attempts one.
```

### 3.5 — Frontmatter

**Add to `sources:`** `dilger-podcast-episode-47-agentic-modeling-audit-trails`,
`nick-tune-event-sourced-claude-code-workflows`,
`dilger-git-as-primary-persistence-for-event-models`,
`tornhill-blast-from-the-past-sdd-illusion-of-known-scope`,
`dilger-ux-as-first-class-in-spec-driven-development`,
`dilger-only-engineers-care-about-consistent-systems`,
`dilger-ui-only-interactions-filtering`,
`dilger-loop-engineering-never-argue-with-agent`. Set `updated: 2026-09-04`; append to the trailing
`_Sources: …_` line.

---
## 4. `wiki/concepts/loop-engineering.md` — UPDATE (3 items)

### 4.1 — CREATE a section for Dilger's loop-engineering primary, **and correct a date the KB has wrong**

**Why:** the page's own open question is *what supplies the task list?* Dilger answers it by
construction (the [[slice]]), and the KB does not have this primary at all — his loop material reaches
the page only via `describing-without-solving` and the self-training loop. **It also moves a date:** the
KB dates the Event Modeling Agent Harness to `dilger-event-modeling-agent-harness` (2026-06-17), but
this article is **2026-06-10** and already contains the full board mechanic, claim-lock and timeout
recovery. It is the earlier and fuller primary.

**Where:** insert as a new `##` section immediately **after**
`## A loop that rewrites its own skills, and grades itself against artifacts (Dilger, 2026-08)` and
**before** `## Open questions`.

**Paste:**

```markdown
## The task list is the hard part — and Event Modeling supplies it (Dilger, 2026-06-10)

[[dilger-loop-engineering-never-argue-with-agent]] is this page's Event-Modeling entry, and it answers
the page's own standing question — *what supplies the task list?* — with one sentence:

> "The hard part in Loop Engineering is not implementing the loop, it's defining the list of tasks. In
> Event Modeling this happens naturally and is part of the process. **Every 'slice' of functionality
> becomes a task.**"

**Chronology correction this ingest establishes:** the KB dates the *Event Modeling Agent Harness* to
[[dilger-event-modeling-agent-harness]] (2026-06-17). **This article is a week earlier (06-10)** and
already carries the whole mechanic, so the idea's date should move to 2026-06-10 and 06-17 read as the
restatement.

**The loop, minimally:** define a task list; run tasks one at a time; **record what you learned after
each**; then **clear the context completely** — *"No bias. No bad decisions lingering. No wrong
information. Just the learnings - and the next task."* Provenance he states himself: he read Geoffrey
Huntley in **2025**, dismissed the [[ralph-loop|RALPH loop]] (*"running an agent in a loop?
Nonsense"*), then realised he was already doing it. He also frames loop engineering as *"the 'new
thing' after Spec-Driven Development"* — his own ordering of the two disciplines.

**"I never argue with an agent."** *"Every agent will immediately tell you how right you are. That's not
learning. That's hand-waving agreement… The agent isn't learning from your corrections. It's just
agreeing with you - and carrying the confusion forward."* Operationally: each iteration has defined
goals and rules, and **a broken rule ends the iteration with no discussion** — discard everything except
the learnings and retry. His mechanism claim for why — *"confusion is what produces hallucination. It's
not a random event. It's the predictable result of a polluted context window"* — is **asserted with no
evidence**; the KB holds better-evidenced versions at [[context-rot]].

**Do not engineer the loop.** Asked to make an agent stop, revert and restart when its task changes
mid-flight, his answer is that the loop already handles it: *"The moment you start overengineering it -
adding more state, more memory, more decision-making between iterations - you start reintroducing
exactly the problems the loop was designed to eliminate. You're building back the noise. Simplicity
isn't a limitation of loop engineering. It is loop engineering."* **This is a direct counter-position to
the elaboration this page documents elsewhere** — LangChain's four stacked loops, Osmani's five
primitives plus four memory channels, Miracle's trust ledger. Dilger's claim is that the machinery is
mostly compensating for a missing task list.

**The board as the loop's control surface** (the concrete mechanism, and the fullest statement of it in
the KB): slices carry status; **Planned** means an agent may claim it; agents subscribe to
`slice:changed` (Claude Code, Codex and Hermes named); a claiming agent moves it to **In Progress**,
which **locks it against other agents**. Three terminal outcomes: **Done**; **Blocked**; or **the agent
dies, the slice times out in progress, and another agent picks it up** — the timeout being what makes an
unattended fleet safe to leave running ([[unattended-coding-agents]], [[long-running-agents]]). Editing
finished work: move Done → In Progress, edit, move to Planned, and an agent **diffs the specified slice
against the code and reconciles the code to the spec**. Hints go in **comments on the slice**, which the
agent checks off. *"There's no manual prompting involved. Just change a slice and wait until the agent
did the work."*

**The load-bearing claim, and the batch's cleanest disagreement.** *"If something fails, the problem is
in the spec, not the prompt."* That is [[spec-driven-development]]'s thesis stated as a debugging rule —
and it is exactly what the SDD sceptics deny.
[[eberhardt-putting-spec-kit-through-its-paces|Eberhardt]] hit a trivial unpopulated-variable bug and
*"asked Copilot, and it concurred, this isn't an issue with the spec"*;
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill's]] requirements-explosion argument
says most defects **cannot** be spec defects, because the spec cannot contain the implicit design
decisions. Whether loop failures are spec failures is now a live, testable question this page should
carry as open.

*(**VENDOR SELF-REPORT** — eventmodelers.ai/EM-Studio is Dilger's own platform; every mechanism above is
one of its features, and the piece closes selling his book, the build-kits and paid training
(*"as I did for hundreds of engineers already"* — **his own figure**). **No evidence of any kind**
appears in it, and the central claim is stated absolutely: *"Clean iterations with recorded learnings
will outperform long, polluted conversations every single time. Not sometimes. Every time."* Carry that
as a position, not a finding.)*
```

### 4.2 — ADD the shipping instance of the hill-climbing rung

**Why:** the page describes an improvement/hill-climbing loop (LangChain's fourth rung, AHE's measured
version) but has no *shipping practitioner instance* where loop telemetry rewrites the harness. Tune's
is one, and it is built on the KB's own focus-area substrate.

**Where:** at the end of `## The hill-climbing loop, measured ([[ahe-agentic-harness-engineering|AHE, Lin et al. 2026]])`.

**Paste:**

```markdown
**A practitioner instance of the same rung, built on an event log (Tune, 2026-03-04).**
[[nick-tune-event-sourced-claude-code-workflows]] persists **only events** from his Claude Code workflow
state machine and derives state by replay, which turns the loop's own history into the instrument:
per-state dwell time, **rejection counts** (code review failed) and **hook-denial counts** (the agent
attempted something disallowed in that state), plus a journal enforced at ≥1 entry per iteration by hard
blocks. His stated target for the last two is **zero** — *"they indicate a waste of time, waste of
tokens, and indicate our agent has sub-optimal instructions"* — which is the cleanest **defect signal on
the harness rather than on the code** the KB holds. And the hill-climbing step is explicit: *"Don't just
build metrics from your events, feed them to your AI assistant… It can identify why problems exist and
suggest how to optimize the context or workflow"* — a CLAUDE.md edit or a review-agent prompt change.

Read against [[dilger-modeling-agent-improved-by-learning-loop|Dilger's self-training loop]], the two
differ in **what grades the run**: Dilger's grader is a structural diff against a corpus of hand-crafted
artifacts, Tune's is the execution log of the loop itself. The page's own warning about metric-shaped
graders applies to Tune's and not to Dilger's — a zero-denials target is exactly the kind of proxy an
agent can satisfy by narrowing what it attempts.

*(**IMPRESSION NOT MEASUREMENT · NOT INDEPENDENT** — his own harness, and the "15 minutes in RESPAWN vs
2 minutes DEVELOPING" reading is from **one session of a personal project**, which he states. His
"great results on real projects" carries no number, and cross-session analysis and the control centre
are **explicitly unbuilt**.)*
```

### 4.3 — UPDATE `## Open questions`

**Where:** append two bullets to the existing list.

**Paste:**

```markdown
- **Is loop failure spec failure?** [[dilger-loop-engineering-never-argue-with-agent|Dilger]] asserts
  *"if something fails, the problem is in the spec, not the prompt"* and rebuilds his whole workflow on
  it. [[eberhardt-putting-spec-kit-through-its-paces|Eberhardt's]] broken dev server and
  [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill's]] requirements explosion both
  say a large class of defects cannot be spec defects. Nobody has classified a real run's failures
  against that distinction — and it is cheap to do.
- **Does the loop need machinery, or a task list?** The page documents steadily more elaborate loop
  stacks; Dilger's position is that elaboration is compensating for the absence of a well-formed unit of
  work, and that a [[slice]] supplies one. Both cannot be right about the same workloads.
```

**Frontmatter:** add `dilger-loop-engineering-never-argue-with-agent` and
`nick-tune-event-sourced-claude-code-workflows` to `sources:`; `updated: 2026-09-04`; append both to the
trailing `_Sources: …_` line.

---

## 5. `wiki/concepts/event-sourced-agentic-patterns.md` — UPDATE (2 items)

### 5.1 — CREATE a section: "audit trail, not snapshot" and the three layers now answering it

**Why:** the page's synthesis is that current state should be a replay of a ledger. This batch supplies
**the argument stated as a requirement for agents** (Dymitruk) and **three independently built answers at
three different layers**, none citing the others. That triangulation is the strongest thing in the batch
and this is its home page.

**Where:** insert as a new `##` section immediately **after** `## The unifying claim` and **before**
`## Open edge — now largely closed (2026-06-12)`.

**Paste:**

```markdown
## "Agents need an audit trail, not a snapshot" — and three layers of answer

[[adam-dymitruk]] states this page's thesis as a *requirement for agents*, in
[[dilger-podcast-episode-47-agentic-modeling-audit-trails]]:

> "Agents need an audit trail, not a snapshot. Events are the truth, the full story, not just the
> current state. Read models are derived and disposable. If an agent goes sideways, follow the event
> trail, find the divergence, fix it, replay. No mystery, no data surgery."

*(Provenance: the hosts are relaying a LinkedIn post by **Svet Angelov**, which is **not captured in
`raw/`** — so Dymitruk's endorsement is the citable part, not the origin. The episode's **date is
unresolved**: no date in HTML, metadata or body; absent from the RSS feed and from
podcast.eventmodeling.org, both still ending at Ep 46 (2026-04-26/27), so it post-dates 2026-04-27 and
may be a previously unpolled channel rather than a new item. **Show-notes level, not verified against
audio. VENDOR SELF-REPORT** for the tooling.)*

The claim is a *should*. What is new as of 2026-09 is that it has been answered at three distinct layers,
by three parties, **none of whom cite each other**:

| Layer | Answer | Source |
| --- | --- | --- |
| The **domain** the agents build | the event log itself — the KB's existing synthesis | this page; [[esaa-event-sourcing-for-autonomous-agents]] |
| The **specification** the agents work from | **git as primary persistence** for the event model: one repo per board, branching, BYODS, and *"you can store your models in a Worm-Drive for auditability"* | [[dilger-git-as-primary-persistence-for-event-models]] |
| The **agent loop** itself | persist **only events** from the workflow state machine, derive state by replay; the log yields per-state timings, rejection counts, hook-denial counts and a journal | [[nick-tune-event-sourced-claude-code-workflows]] |

**Why the middle row is the interesting one.** Every audit-trail argument in this KB so far has been
about the agent's *actions*. Making the **model's own history** the audit trail means you can prove what
the agent was *told* to build, not only what it did — a feedforward control on the spec rather than a
feedback control on the output ([[feedforward-and-feedback-controls]], [[agent-governance]]). *(**VENDOR
SELF-REPORT**; the git backend is **announced as being added, not reported in use**, and no auditability
requirement, regulation or auditor is named for the WORM claim.)*

**Why the bottom row is not the same claim as this page's.** Tune's consumers are harness-optimisation
questions — where did time go, which instructions are being violated — not domain queries, and his
purpose is *efficiency* where Dymitruk's is *correctness* (*"follow the event trail, find the
divergence, fix it, replay"*). Same substrate, different use. *(**IMPRESSION NOT MEASUREMENT · NOT
INDEPENDENT** — one session of his own personal-project harness, which he states.)*
```

### 5.2 — AMEND the "still genuinely open" sentence

**Where:** at the very end of the page, in the paragraph closing
`## Open edge — now largely closed (2026-06-12)`.

**Find:** `*Still genuinely open:* an external source connecting the five patterns specifically to
[[event-modeling]] (the method), and a **worked** model — see [[event-modeled-agent-design]].`

**Replace with:**

```markdown
*Still genuinely open:* an external source connecting the five patterns specifically to
[[event-modeling]] (the method), and a **worked** model — see [[event-modeled-agent-design]]. The
nearest arrival since is [[nick-tune-event-sourced-claude-code-workflows]] (2026-03-04), which
event-sources the **agent loop** rather than the domain: a real running system whose source of truth is
the loop's own event history. It is **not** the method — no swimlanes, commands, read models or
timeline — so the gap stands, but it is the first published instance where an agent harness's state
*is* a projection of its events. *(**NOT INDEPENDENT · IMPRESSION NOT MEASUREMENT** — his own harness,
personal projects.)*
```

**Frontmatter:** add `dilger-podcast-episode-47-agentic-modeling-audit-trails`,
`dilger-git-as-primary-persistence-for-event-models`,
`nick-tune-event-sourced-claude-code-workflows`; `updated: 2026-09-04`.

---

## 6. `wiki/concepts/agent-readable-model-artifacts.md` — UPDATE (2 items)

### 6.1 — ADD the persistence rung and note it collapses a framing the page draws

**Where:** at the end of `## The ladder of surfaces` (after the last rung, before
`## Three things the pattern shows`).

**Paste:**

```markdown
**A rung the ladder implied but never had: the model's *store* (2026-09-02).**
[[dilger-git-as-primary-persistence-for-event-models]] makes **git a primary persistence layer for the
model itself** rather than a versioning extension: *"No relational database. All data lives in Git."*
One repository per board, configurable, **branching supported**, under a **"BYODS — bring your own
datastore"** design (Redis, S3, YAML, SharePoint named as possibilities), and *"you can store your
models in a Worm-Drive for auditability."*

Three things follow for this page:

- **The board-vs-file framing collapses.** The ladder has treated *board via MCP* and *linted file
  format* as different rungs. If the board's primary store is a git repo, they are the same rung: an
  agent can read the model, and its whole history, with ordinary `git` and `grep`, or via MCP, without
  an export step.
- **Addressability gains a time axis.** The page's central claim is that what makes a model
  agent-usable is a **shared handle to instruct and report against**. A commit adds *which version* to
  that handle, and makes **model↔code drift a diff between two repos** rather than a bespoke check
  ([[dilger-keep-command-handlers-pure]], [[esdm-event-sourced-domain-modeling]]).
- **Branching a specification is genuinely new**, and unexamined. Nothing in the source says how a
  two-dimensional board serialises so diffs and merges are meaningful, what happens when two agents (or
  humans) diverge on the same slice, or how branching interacts with the board-level claim-lock that
  keeps parallel agents from colliding ([[dilger-loop-engineering-never-argue-with-agent]]).

It also answers, squarely, one objection the KB holds against model-first work:
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill's]] MDA complaint that vendor design
tools lacked pipelines, CLIs, IDEs and linters — *"imagine coding in a Microsoft Word document."* A model
in git gets the whole toolchain. It answers nothing about
[[eberhardt-putting-spec-kit-through-its-paces|Eberhardt's]] opposite objection, that specs are
point-in-time artifacts rarely revisited, so versioning them is cost without return.

*(**VENDOR SELF-REPORT** — EM-Studio is [[martin-dilger]]'s own platform; the git backend is
**announced as being added, not reported in use**, and no auditability requirement, regulation or
auditor is named for the WORM claim.)*
```

### 6.2 — ADD a pointer to the screens surface

**Where:** at the end of `## Read/write, not just read`.

**Paste:**

```markdown
**A surface this page under-weights: the screen.** Beyond text, coordinates and freeform marks, the
model's **UI mockups** are themselves an agent-readable artifact —
[[dilger-ui-only-interactions-filtering]] states it plainly: *"Using the UI mockup - which is also
accessible for a connected agent building from the model - it's quite clear what needs to be done."*
With HTML Views authored in the model, region-scoped screen markers
([[dilger-highlighting-markers-give-context-to-agents]]) and a Screen Preview that puts hand sketches,
HTML mockups and Figma in one storyline
([[dilger-only-engineers-care-about-consistent-systems]]), the screen becomes both the
human-reviewable surface and an agent input. Treated as its own claim at
[[screens-as-specification]]. *(**VENDOR SELF-REPORT** throughout — all EM-Studio features.)*
```

**Frontmatter:** add `dilger-git-as-primary-persistence-for-event-models`,
`dilger-ui-only-interactions-filtering`, `dilger-ux-as-first-class-in-spec-driven-development`;
`updated: 2026-09-04`.

---
## 7. `wiki/concepts/screens-as-specification.md` — **CREATE** (1 item)

**Why a new page, and the judgement call.** This is the batch's second mechanism claim
(*UX/Given-When-Then as first-class in the spec instead of markdown-derived UX*), and it has four
sources in this batch alone plus two already in the KB. Individually each is thin — one is a
~100-word LinkedIn note whose demonstration is an uncaptured webinar — but together they make a claim no
existing page owns: **the screen is part of the specification the agent builds from, and it is the
artifact non-developers can actually review.** [[event-modeling]] owns the notation,
[[agent-readable-model-artifacts]] owns addressability, [[given-when-then]] owns the rules, and none of
them owns the screen.

**Orchestrator's call.** If you would rather not add a page, the fallback is a `##` section on
[[agent-readable-model-artifacts]] with §6.2 expanded — but then the Ng/Zaninotto/Böckeler
"who-can-review-this" thread has no home, because that is a claim about *audience*, not about machine
readability. **Recommend creating it.** Slug is new; it is not a variant of an existing page.

**Paste as the whole file:**

```markdown
---
title: Screens as Specification
type: concept
created: 2026-09-04
updated: 2026-09-04
sources: [dilger-ux-as-first-class-in-spec-driven-development, dilger-ui-only-interactions-filtering, dilger-podcast-episode-47-agentic-modeling-audit-trails, dilger-only-engineers-care-about-consistent-systems, dilger-highlighting-markers-give-context-to-agents, zaninotto-spec-driven-development-waterfall-strikes-back, eberhardt-putting-spec-kit-through-its-paces, ng-spec-driven-development-is-waterfall-in-markdown]
tags: [event-modeling, spec-driven-development, given-when-then, agentic-coding, focus]
---

# Screens as Specification

**The claim:** in an agent-facing specification, the **screen is first-class content, not derived
output** — and it is the part of the spec a designer, a product owner or an end user can actually
review. [[martin-dilger]] states it as a workflow property
([[dilger-ux-as-first-class-in-spec-driven-development]], 2026-08-31):

> "Instead of deriving the UX from markdown files ( which become unreadable and impossible to maintain
> from a certain size on ), we focus on the functionality, the UX and the business rules described as
> Given / When / Then ( BDD Style ). **Spec-Driven Development does not need Markdown Files.**"

So the division of labour is **screens carry the interaction, [[given-when-then|GWT]] carries the
rules** — which is narrower and more checkable than the general "use a DSL" claim in
[[model-as-code-vs-model-as-language]].

> **VENDOR SELF-REPORT throughout.** Every mechanism on this page is a feature of Dilger's own
> commercial platform ([[eventmodelers-ai]] / EM-Studio, [[nebulit]]). The fullest primary for the
> workflow is an **uncaptured 60-minute webinar** the LinkedIn note links to; the note itself is
> ~100 words and contains no demonstration. Read the claims here as a stated position with worked
> illustrations, not as evidence that it works.

## Why the method already had room for it

[[event-modeling]] has always put wireframes and mockups in swimlanes across the top of the board, one
lane per actor — screens are original equipment, not an addition. [[adam-dymitruk]] defends this
directly in [[dilger-podcast-episode-47-agentic-modeling-audit-trails]], where a DDD-community post
*"rediscovers"* that showing users' screens carries real information:

> "That's why all the arguments about not having screens and design sessions is just gatekeeping by
> architect wannabes."

*(That episode's **date is unresolved** — see its source page. **Show-notes level, not verified against
audio.**)*

## The mechanism, worked

[[dilger-ui-only-interactions-filtering]] (2026-07-31) is the concrete instance, and its method
content matters independently: **most screen interactions are not state changes and must not be
modelled as Commands and Events.**

> "Filtering, sorting, expanding a row, switching a tab - these are all views on data you already have.
> Model them as Views, not as Commands looking for an Event to justify them."

The filtering example uses **Multi-Screen Views** — an unfiltered page and a filtered page backed by
the *same* `Books[]` read model — with behaviour specified on the read side using the **Query WHEN**
(*"Given two `Book registered` events… When you query by title with the key 'Harry Potter', Then the
`Books` Read Model returns just that one match"*). Note the Query WHEN is used here as ordinary
practice, but its status per [[dilger-extending-event-modeling-query-when]] is **optional, proposed and
not ratified**; that status travels.

The screen is authored *in* the model (plain HTML views, or generated cheaply by a connected agent), and
the agent-facing payoff is stated explicitly: *"Using the UI mockup - which is also accessible for a
connected agent building from the model - it's quite clear what needs to be done."* Two adjacent
surfaces complete the picture: **region-scoped screen markers** an agent reads, validates and builds UI
from ([[dilger-highlighting-markers-give-context-to-agents]]), and a **Screen Preview** placing hand
sketches, HTML mockups and Figma screens in one storyline
([[dilger-only-engineers-care-about-consistent-systems]]).

## The audience argument — and why it matters more than the machine one

The KB's sharpest external objection to spec-first work is about **who can read the artifact**, not
whether an agent can. [[ng-spec-driven-development-is-waterfall-in-markdown|Ng]]: a spec flattens a
cross-functional set of mental models into the author's single voice, and no designer, PM or DevOps
engineer will ever open a `.specify` folder — *"a contract between you and the LLM that nobody else
signed."* [[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler]] asks the same thing as *who is the
target user?*, noting SDD tools import product vocabulary while presenting a lone developer as author.
And [[zaninotto-spec-driven-development-waterfall-strikes-back|Zaninotto]] — arguing *against* SDD
entirely — ends with the one wish this page answers:

> "Coding agents use text, not visuals. Sometimes I want to point to a specific zone… if we need new
> tools to make coding agents more powerful, I think the focus should be on richer visual
> interactions."

A sketched screen needs no folder, and it is the artifact an end user reacts to — which is exactly
Dilger's own prescription in [[dilger-only-engineers-care-about-consistent-systems]]: *"invite them to a
short Event Modeling Session. Show them what you planned, show them the screens you sketched… you do
not have to write a single line of code for that."*

**How far this answer goes.** It answers *"nobody will open the artifact."* It does **not** answer
*"nobody else signed it"*: the KB holds **no captured source measuring non-developer participation in a
model that later drove agents**, and every source on this page is one interested party. See the named
gap on [[event-modeled-agent-design]].

## The counter-evidence, which is real

- **Generated UI rationale is where SDD looks worst, and that supports the diagnosis while rejecting
  the cure.** [[eberhardt-putting-spec-kit-through-its-paces|Eberhardt's]] exemplar of AI *"detail that
  fundamentally lacks depth of value"* is invented UX reasoning: *"Karting users need to log data
  trackside on mobile devices, often with gloves or in suboptimal lighting."* Markdown-derived UX doing
  precisely what Dilger says it does — from an author who concludes SDD is not viable at all.
- **Agents can inflate the visual artifact too.** Ep 47's `/wdyt` tuning lesson: an agent flooding a
  slice with hypothetical edge cases *"can make a simple slice look far more complex than it really is,
  since event modeling is visual"* (Dymitruk). The screen's advantage is legibility, and legibility is
  destroyable ([[event-modeling-anti-patterns]]).
- **"BDD Style" is doing loose work.** Screens-plus-GWT is not what specification by example normally
  means by *executable* specification, and [[gojko-adzic]] — who wrote the book — finds SDD tools' GWT
  output *"is not a spec, it lacks a ton of detail"*
  ([[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]]). Dilger's version may be stronger; it
  is not established.
- **No worked case where an authored screen drove agent-built UI end to end** is captured anywhere.

## Related

[[event-modeling]] · [[given-when-then]] · [[agent-readable-model-artifacts]] ·
[[spec-driven-development]] · [[event-modeled-agent-design]] · [[event-modeling-anti-patterns]] ·
[[slice]] · [[decision-trace]] · [[eventmodelers-ai]]

_Sources: [[dilger-ux-as-first-class-in-spec-driven-development]] ·
[[dilger-ui-only-interactions-filtering]] ·
[[dilger-podcast-episode-47-agentic-modeling-audit-trails]] ·
[[dilger-only-engineers-care-about-consistent-systems]] ·
[[dilger-highlighting-markers-give-context-to-agents]] ·
[[zaninotto-spec-driven-development-waterfall-strikes-back]] ·
[[eberhardt-putting-spec-kit-through-its-paces]] ·
[[ng-spec-driven-development-is-waterfall-in-markdown]]._
```

---

## 8. `wiki/concepts/given-when-then.md` — UPDATE (3 items)

### 8.1 — ADD Adzic's first-party verdict as a new section

**Why:** the page treats GWT as the acceptance-gate unit. The author of *Specification by Example* has
now judged the SDD toolkits' GWT output, and the judgement is that **it looks like specification by
example and isn't** — with a specific test the page should carry.

**Where:** insert as a new `##` section immediately **after**
`## The provenance condition: agreed in the room, not written at a desk (Ng, 2026-03)` and **before**
`## The *given* arrived at from outside — declared preconditions (2026-08)`.

**Paste:**

```markdown
## GWT-shaped is not GWT — the first-party test (Adzic, 2025-09-29)

[[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]] is [[gojko-adzic]], author of
*Specification by Example*, assessing whether [[spec-driven-development|SDD]] is *"BDD taken to a new
level."* His answer: **"It does not, really."**

The generated Spec Kit spec has Given-When-Then acceptance scenarios and MUST/SHOULD functional
requirements — it is GWT-shaped — and his verdict is that *"this is on such a high level that it fits
more the scope of work than a specification… **This is not a spec, it lacks a ton of detail.**"* What
happens instead:

> "The real 'spec' then ends up being in unit and integration tests that are generated based on these
> requirements… readable only for developers. It just seems as a missed opportunity to create
> human-readable specs and drive the work from that."

So the failure is not that GWT is absent but that the **executable** specification and the
**human-reviewable** one have come apart — the exact thing specification by example exists to prevent.
The test he offers is the most checkable one the KB holds for any spec artifact: *"a source of truth
that's detailed enough for people to approve/complain about, but not just in code."*
**Can a non-developer approve or complain about it?**

Two things this changes on this page:

- **A GWT scenario at scope-of-work granularity is not an acceptance gate.** The KB's strongest GWT
  claims ([[jwilger-agent-skills-event-modeling]]'s TDD gates rejected unless they exercise an external
  boundary; [[adaptech-given-when-then-executable-tests-before-implementation]]) all depend on
  scenarios being specific enough to fail for the right reason. Adzic's finding is that generated ones
  routinely are not — which is [[bockeler-tdd-inside-the-agent-loop|Böckeler's]] *"a self-confirmed red
  test proves only that the agent saw a failure, not that the failure was for the right reason"*
  arriving from the requirements side.
- **It is a *scoping* complaint, not a notation one.** His second objection is a **missing scoping
  phase**: with a spec at that granularity *"the tool tried to do too much and kind of went off the
  rails… the whole 'human in the loop' idea was no longer feasible."* That converges independently with
  [[dilger-spec-driven-development-needs-four-phases|Dilger's phase 1]], neither citing the other.

*(One session at a conference workshop, one greenfield toy problem, three weeks into Spec Kit's life,
and **no figures in the piece**. He is also the interested party in the comparison, being the author of
the tradition whose ground is in question — and his overall verdict is warmer than any other critic's:
*"definitely something to keep an eye on."*)*
```

### 8.2 — ADD the Query WHEN's move from proposal to ordinary use

**Where:** at the end of `## Storylines — one scenario instead of several (Dilger, 2026-08)`.

**Paste:**

```markdown
**The read-side "Query" WHEN, now used as ordinary practice (2026-07-31).**
[[dilger-extending-event-modeling-query-when]] (2026-06-29) proposed an optional WHEN named *Query* for
read-side scenarios and was explicit it was **not ratified** — *"I wouldn't add this myself — I'm seeking
feedback."* A month later [[dilger-ui-only-interactions-filtering]] simply uses it, without restating
the status: *"Given two `Book registered` events - one for Harry Potter, one for Lord of the Rings -
When you query by title with the key 'Harry Potter', Then the `Books` Read Model returns just that one
match."* And it draws the point that makes it worth having: *"Nothing about this Scenario depends on the
UI plumbing. It's stated purely in terms of the data."* — i.e. the Query WHEN lets a **UI-only
interaction** be specified without inventing a Command or an Event
([[screens-as-specification]], [[event-modeling-anti-patterns]]).

**Status has not changed, only usage.** No ratification is reported anywhere; it remains an opt-in
extension on one vendor's platform (**VENDOR SELF-REPORT**), and any page citing it must carry that.
```

### 8.3 — ADD the over-specification limit

**Where:** at the end of `## Why it matters here`.

**Paste:**

```markdown
**A limit that only shows up once agents write the scenarios (Ep 47).** In
[[dilger-podcast-episode-47-agentic-modeling-audit-trails]], a gap-finding agent's first version
*"flooded the model with 100 comments inventing hypothetical gaps"*, and [[adam-dymitruk]] names the
specific damage: an over-eager agent flooding a given-when-then list with edge cases *"can make a simple
slice look far more complex than it really is, since event modeling is visual."* The method's own answer
is older than the tooling — *"draw a few representative example paths and trust the implementer to infer
the rest, rather than trying to specify everything"* — which is specification by example's whole
premise, and the reason **more GWT is not monotonically better**. The tuning fix was a restriction:
comment only on **what is present**, never invent scenarios. *(Date unresolved; show-notes level;
**VENDOR SELF-REPORT**.)*
```

**Frontmatter:** add `adzic-spec-driven-development-revenge-of-waterfall-or-bdd`,
`dilger-ui-only-interactions-filtering`,
`dilger-podcast-episode-47-agentic-modeling-audit-trails`,
`dilger-ux-as-first-class-in-spec-driven-development`; `updated: 2026-09-04`.

---

## 9. `wiki/concepts/event-modeling.md` — UPDATE (2 items)

### 9.1 — CREATE a section on UI-only interactions

**Why:** the page states the negative rule ("user viewed the calendar is not an event") and never the
positive one. This is a genuine method clarification the KB did not hold, and it is the most-asked
question in the source's own account (*"I've answered it dozens of times already"*).

**Where:** insert as a new `##` section immediately **after** `## The 4 patterns` (and its two
subsections) and **before** `## The 7-step workshop`.

**Paste:**

```markdown
## UI-only interactions — model them as Views (Dilger, 2026-07-31)

The method's "only state changes are events" rule stated positively.
[[dilger-ui-only-interactions-filtering]] answers *"how would you model filtering?"* with: usually you
don't — not as a Command and an Event.

> "Filtering, sorting, expanding a row, switching a tab - these are all views on data you already have.
> Model them as Views, not as Commands looking for an Event to justify them."

The worked form uses **Multi-Screen Views**: an unfiltered page and a filtered page backed by the *same*
`Books[]` read model, so one slice shows how the system behaves *"without inventing state changes that
don't exist in the domain."* Behaviour is specified on the read side with the **Query WHEN** — *"Given
two `Book registered` events… When you query by title… Then the `Books` Read Model returns just that one
match"* — which keeps the scenario *"stated purely in terms of the data"*, independent of whether the
implementation filters client-side or refetches. (That WHEN is the **optional, proposed, unratified**
extension from [[dilger-extending-event-modeling-query-when]]; the status travels.)

Two consequences worth carrying: the completeness bar for such a slice is **mockup + GWT scenario and
nothing more** (*"This is enough to implement it"*), and the corresponding
**[[event-modeling-anti-patterns|anti-pattern]]** is now nameable — *Commands invented to justify Events
for interactions that change nothing*. The honest edge the source does not discuss: sometimes *which
filter a user applied* **is** a business fact worth recording, and nothing here says how to tell.
*(**VENDOR SELF-REPORT** — Multi-Screen Views, HTML Views and Query support are features of
[[eventmodelers-ai]] / EM-Studio, and the article closes selling a paid programme.)*
```

### 9.2 — EXTEND the podcast section to Ep 47

**Where:** at the end of `## Practitioner lens — the weekly podcast (Dymitruk & Dilger)`.

**Paste:**

```markdown
**Episode 47 (date unresolved).** [[dilger-podcast-episode-47-agentic-modeling-audit-trails]] is the
newest podcast item published anywhere and **carries no date** — no date in HTML, metadata or body, and
it is **absent from the RSS feed and from podcast.eventmodeling.org**, both of which still end at
**Ep 46 (2026-04-26/27)**. So it post-dates 2026-04-27 and nothing more can be said; **it may be a
channel prior sweeps never polled** (`eventmodelers.ai/docs/podcast` is a separate, more current index
than the `.org` one) **rather than a genuinely new item**. Method-relevant content: two AI agents
modelling alongside Dilger in real time; the `/wdyt` gap-finding skill and the **over-specification
tuning lesson** (restrict the agent to what is present, forbid invention —
[[event-modeling-anti-patterns]]); **specification by example** as the method's existing answer to the
"infinite possibility tree"; **screens are legitimate, information-only artifacts** and dismissing them
is *"gatekeeping by architect wannabes"* (Dymitruk — [[screens-as-specification]]); **events as an
audit trail rather than a snapshot** for agents ([[event-sourced-agentic-patterns]]); and shared
industry vocabulary — command handlers, event handlers — as the durable payoff
([[em-standardization-foundation]]). Show-notes level only, as with Eps 1–46.
```

**Frontmatter:** add `dilger-ui-only-interactions-filtering`,
`dilger-podcast-episode-47-agentic-modeling-audit-trails`; `updated: 2026-09-04`.

---

## 10. `wiki/concepts/event-modeling-anti-patterns.md` — UPDATE (2 items)

### 10.1 — CREATE a section for the second *class* of anti-pattern

**Why:** the page's taxonomy ("The Shapes") is about bad models humans draw, readable off a silhouette.
Ep 47 introduces a different class: **anti-patterns an agent reviewer induces**, invisible to a
structural check because the result is well-formed.

**Where:** insert as a new `##` section immediately **after** `## Why it matters for agents` and
**before** `## Relationships`.

**Paste:**

```markdown
## A second class: anti-patterns the *agent* induces (Ep 47, date unresolved)

"The Shapes" catalogues bad models humans draw. [[dilger-podcast-episode-47-agentic-modeling-audit-trails]]
surfaces the inverse — a model degraded by an agent pointed at it.

The `/wdyt` skill's first version *"flooded the model with 100 comments inventing hypothetical gaps."*
[[adam-dymitruk]] names why that is worse than ordinary review noise: an over-eager agent flooding a
[[given-when-then|given-when-then]] list with edge cases *"can make a simple slice look far more complex
than it really is, **since event modeling is visual**."* The damage is to **legibility**, the property
the whole method trades on — and a bloated slice is still *well-formed*, so neither a linter nor a
structural diff against a reference catalog would flag it.

**Name it over-specification, and note the fix is a restriction on the reviewer, not on the model:**
*"don't just look at what is there — don't comment on something because it's not specified. Just look at
what is there and make sense of it, then give me comments. And then it got significantly better."*
The method's own defence predates the tooling: **specification by example** — *"draw a few
representative example paths and trust the implementer to infer the rest, rather than trying to specify
everything."*

This is the same failure [[bockeler-tdd-inside-the-agent-loop|Böckeler]] found one altitude down, where
agent-authored micro-tests suppressed up-front design: **an agent inventing its own acceptance criteria
degrades the artifact it is checking.** Both point at the same rule — the criteria come from outside the
loop.

*(**Date unresolved** — see the source page; it post-dates 2026-04-27 and may be a previously unpolled
channel. **Show-notes level, not verified against audio. VENDOR SELF-REPORT** — the skill ships on
[[eventmodelers-ai]]. The comment counts are impressions.)*
```

### 10.2 — ADD the UI-only anti-pattern

**Where:** at the end of `## "The Shapes"` (as a closing paragraph, clearly marked as *not* one of the
Shapes).

**Paste:**

```markdown
**Not a Shape, but an anti-pattern the method names elsewhere: Commands invented to justify Events.**
[[dilger-ui-only-interactions-filtering]] (2026-07-31) — filtering, sorting, expanding a row, switching
a tab *"are all views on data you already have. Model them as Views, not as Commands looking for an
Event to justify them."* Unlike the Shapes this is not readable off a silhouette; it shows up as
domain-meaningless events on the swimlane. See [[event-modeling]] and [[screens-as-specification]].
```

**Frontmatter:** add `dilger-podcast-episode-47-agentic-modeling-audit-trails`,
`dilger-ui-only-interactions-filtering`; `updated: 2026-09-04`.

---
## 11. `wiki/concepts/agent-observability-and-evals.md` — UPDATE (1 item)

**Why:** the page's Observability section has no practitioner instance where the *loop's own* telemetry
is the observable. Tune supplies one, with two counters that have a stated target of zero.

**Where:** at the end of `## Observability`.

**Paste:**

```markdown
**Observability derived from replay, not from a tracing SDK (Tune, 2026-03-04).**
[[nick-tune-event-sourced-claude-code-workflows]] persists **only events** from a Claude Code
workflow's state machine and rebuilds state by replay, which makes the loop's history the instrument.
Four observables fall out with no extra plumbing:

- **Per-state dwell time**, computed from transition events — *"when the workflow transitions from
  DEVELOPING to REVIEWING or COMMITTING to RESPAWNING we can deduce how long was spent in each state."*
- **Rejection count** — code review failed.
- **Hook-denial count** — the agent attempted something disallowed in that state. Both are read as
  defects in the *instructions*: *"Our goal is for these to always be 0, because they indicate a waste
  of time, waste of tokens, and indicate our agent has sub-optimal instructions."* This is the KB's
  clearest example of a **deterministic sensor pointed at the harness rather than at the code**
  ([[feedforward-and-feedback-controls]], [[harness-engineering]]).
- **A journal** as event-stream entries, with hard blocks enforcing ≥1 per iteration — post-hoc
  analysis, and context for newly spawned team members ([[decision-trace]]).

Then the eval step: *"Don't just build metrics from your events, feed them to your AI assistant… It can
identify why problems exist and suggest how to optimize the context or workflow"* — a CLAUDE.md edit or
a review-agent prompt change ([[loop-engineering]]). Named but **unbuilt**: cross-session trend analysis
and a real-time control centre over all in-progress sessions.

Two cautions. His one worked reading — *"my agents spent 15 minutes in the RESPAWN state whereas they
only spent 2 minutes actually building the feature"* — is an instrument reading from **one session of
his own personal-project harness, and he says so** (**IMPRESSION NOT MEASUREMENT · NOT INDEPENDENT**);
*"I've seen great results on real projects"* carries no number. And a **zero-denials target is a proxy an
agent can satisfy by attempting less**, which is precisely the metric-shaped-grader risk
[[loop-engineering]] warns about.
```

**Frontmatter:** add `nick-tune-event-sourced-claude-code-workflows`; `updated: 2026-09-04`.

---

## 12. `wiki/concepts/agent-governance.md` — UPDATE (1 item)

**Why:** every audit-trail argument on this page is about the agent's *actions*. The batch adds the
first proposal to make the **specification** tamper-evident — a control on the input, not the output.

**Where:** at the end of `## Approaches`.

**Paste:**

```markdown
**A control on the *input*: versioning and WORM-ing the specification (2026-09-02).** The governance
sources on this page audit what an agent *did*. [[dilger-git-as-primary-persistence-for-event-models]]
proposes auditing what it was *told to do*: make **git a primary store for the event model** (one
repository per board, branching supported, under a "bring your own datastore" design), so every change
to the specification is versioned and attributable — and *"you can store your models in a Worm-Drive for
auditability."*

Why it is a distinct governance move: an event log proves the sequence of actions; a versioned,
write-once specification proves the **instruction set in force at the time**. Together they close a loop
the KB's governance material leaves open — an audit trail of behaviour with no comparable record of
intent. In [[feedforward-and-feedback-controls]] terms this is a **feedforward** artifact, and it pairs
directly with [[adam-dymitruk]]'s *"agents need an audit trail, not a snapshot"*
([[dilger-podcast-episode-47-agentic-modeling-audit-trails]]) and with the loop-level version in
[[nick-tune-event-sourced-claude-code-workflows]] — three layers, one instinct
([[event-sourced-agentic-patterns]]).

**What it is not.** *(**VENDOR SELF-REPORT** — EM-Studio is [[martin-dilger]]'s own platform, and the git
backend is **announced as being added, not reported in use**.)* **No requirement is cited** — no
regulation, standard, auditor or customer is named, unlike
[[axoniq-government-ai-explainability-requirements]] where the KB does hold a sourced requirements
argument. And a commit history records what the spec *became*, not **who agreed to it**, so it does not
touch the authorship objection ([[decision-trace]],
[[ng-spec-driven-development-is-waterfall-in-markdown]]).
```

**Frontmatter:** add `dilger-git-as-primary-persistence-for-event-models`,
`dilger-podcast-episode-47-agentic-modeling-audit-trails`; `updated: 2026-09-04`.

---

## 13. `wiki/concepts/comprehension-debt.md` — UPDATE (1 item)

**Why:** the page has a "requirements-side variant" sourced to Dilger (over-delegating the problem).
Tornhill supplies the *mechanism* for why that debt is unavoidable at scale rather than a discipline
failure — which is a stronger and differently shaped claim.

**Where:** at the end of `## The requirements-side variant (Dilger, 2026-08-14)`.

**Paste:**

```markdown
**The mechanism version, and it is not about discipline (Tornhill, 2026-05-28).** Dilger's variant is a
choice — teams that *"stop solving problems and just describe them."*
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]] argues the debt accrues even when nobody
checks out, via **requirements explosion**: invoking Robert Glass — *"for every 10-percent increase in
problem complexity, there is a 100-percent increase in the software solution's complexity"* — he
concludes *"each requirement in the spec will lead to tens of implicit design requirements that need to
be resolved. We cannot leave that as guesswork for an agent to figure out."* *(**Glass's assertion as
relayed**; Tornhill names no specific work and measures nothing. Never write "research shows".)*

The debt-shaped consequence is his second obstacle: if agents resolve those implicit requirements for
you, recovering them later is *"like reverse engineering a legacy codebase. **That's the position we'd
be in. Constantly.**"* That is comprehension debt stated as a **structural property of delegated
implementation**, not as a failure to read the diff — and it is why he insists *"implementation is an
essential part of the discovery process itself."* Pair with his own
[[tornhill-compressed-cognition-cost-of-faster-coding]] for the cognitive-load half.

*(**NOT INDEPENDENT** for the remedy he prescribes — *"intention-revealing software design, automated
safeguards for our code and its behavior"* is the category CodeScene, his own company, sells. The piece
contains **no figures at all**.)*
```

**Frontmatter:** add `tornhill-blast-from-the-past-sdd-illusion-of-known-scope`; `updated: 2026-09-04`.

---

## 14. `wiki/concepts/ai-readable-code.md` — UPDATE (1 item, a citation repair)

**Why:** the page names *SDD and the Illusion of Known Scope* in prose with no link, in a sentence whose
neighbouring citation points at the wrong article. The source page now exists.

**Where:** near the end of the paragraph beginning `CLEAR was distilled from concrete refactorings`.

**Find** (verbatim, three lines, mid-paragraph — the word "Two" ends the previous line and stays put):

```
counter-weights from the same author are worth holding here: *Compressed Cognition* (the cost of agentic
speed is decision density) and *SDD and the Illusion of Known Scope* (a pragmatic check on
[[spec-driven-development|spec-first]] optimism).
```

**Replace with:**

```markdown
counter-weights from the same author are worth holding here:
[[tornhill-compressed-cognition-cost-of-faster-coding|*Compressed Cognition*]] (the cost of agentic
speed is decision density) and
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|*SDD and the Illusion of Known Scope*]] — not
merely "a pragmatic check on [[spec-driven-development|spec-first]] optimism" but a positive claim about
readability's limits: **implementation is the discovery process**, each specified requirement spawns tens
of implicit design decisions (Glass's requirements explosion, **as relayed by Tornhill**), and *"the
moment a model becomes the implementation, it ceases to be a good model."*
```

**Frontmatter:** add `tornhill-blast-from-the-past-sdd-illusion-of-known-scope` to `sources:` if the
page lists source slugs; `updated: 2026-09-04`.

---

## 15. Entities — 6 UPDATEs, 4 CREATEs (10 items)

### 15.1 — `wiki/entities/gojko-adzic.md` — UPDATE *(do this one first; it repairs a misattribution)*

Add a section recording the primary and **the correction**. Paste-ready:

```markdown
## On Spec-Driven Development (2025-09-29) — and a misattribution the KB carried

[[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]] is the **earliest** primary in the KB's
SDD critique cluster, written three weeks after GitHub's Spec Kit launched and five months before
[[ng-spec-driven-development-is-waterfall-in-markdown|Ng's]] synthesis.

**The correction.** *"The revenge of Waterfall or BDD taken to a new level"* is **the title, posed as a
question**, not his verdict. Ng relayed it as a judgment and the wiki repeated it. Adzic answers the BDD
half **"It does not, really"**, **never calls SDD waterfall in the body**, and is the warmest of the four
critics: *"definitely something to keep an eye on… Teams looking for more structure in their AI code
generation workflows might find it useful now."*

His actual objections, both first-party (he wrote *Specification by Example* and *Impact Mapping*):
**(1) scope-of-work, not specification** — *"This is not a spec, it lacks a ton of detail"*, with the
real spec migrating into unit and integration tests *"readable only for developers"*, *"a missed
opportunity"*; **(2) a missing scoping phase**, so the tool *"tried to do too much and kind of went off
the rails"* until human-in-the-loop was no longer feasible. His test for any spec artifact — *"detailed
enough for people to approve/complain about, but not just in code"* — is the most checkable one the KB
holds. The scoping complaint converges independently with
[[dilger-spec-driven-development-needs-four-phases|Dilger's phase 1]], neither citing the other. See
[[spec-driven-development]], [[given-when-then]].
```

### 15.2 — `wiki/entities/adam-tornhill.md` — UPDATE

Two changes. **(a) Repair the citation:** the line reading *"…Illusion of Known Scope* (a pragmatic
challenge to spec-first optimism)"* should link to the new source page —
`[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]]` — and its parenthetical should be
strengthened, since the article is a positive argument, not just a caution. **(b) Add:**

```markdown
His fullest statement on [[spec-driven-development|SDD]]
([[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]], 2026-05-28) scopes itself to the **strong
form** (spec as ground truth, per [[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler's]] ladder)
and explicitly **declines the waterfall argument** others make: *"Not due to waterfall thinking — many
SDD practitioners evolve their systems iteratively — but rather due to the nature of problem solving."*
The argument is **requirements explosion** (Glass, as relayed by him) plus lived MDA/Executable-UML/RUP
experience, closing on *"the moment a model becomes the implementation, it ceases to be a good model."*
**NOT INDEPENDENT for the alternative he prescribes** — *"intention-revealing software design, automated
safeguards for our code and its behavior"* is CodeScene's category — and the piece contains **no figures
at all**. He was also programmed at **GOTO Copenhagen 2026** one day after
[[martin-dilger]]'s Event Modeling masterclass
([[dilger-goto-cph-2026-event-modeling-ai-native-software-design]]) — the batch's advocate and its
sharpest sceptic on the same programme.
```

### 15.3 — `wiki/entities/birgitta-bockeler.md` — UPDATE

```markdown
**She originated the KB's SDD vocabulary.** [[bockeler-understanding-sdd-kiro-speckit-tessl]]
(2025-10-15) is the source of the **spec-first / spec-anchored / spec-as-source** ladder the wiki uses as
working vocabulary, and it predates every other primary in the critique cluster
([[zaninotto-spec-driven-development-waterfall-strikes-back|Zaninotto]] and
[[eberhardt-putting-spec-kit-through-its-paces|Eberhardt]] both cite her;
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill]] uses her distinction to scope his
own critique; [[ng-spec-driven-development-is-waterfall-in-markdown|Ng]] is five months downstream).
**Correction:** the KB previously credited this as "the Fowler/Böckeler Kiro analysis" — she is **sole
author**, published on Fowler's site.

Its **MDD parallel** is the strongest external input [[model-as-code-vs-model-as-language]] has
received, and it cuts both ways: model-driven development *"never took off for business applications, it
sits at an awkward abstraction level"*, **but** *"the parseable structure also had upsides that we're
losing now: We could provide the spec author with a lot of tool support to write valid, complete and
consistent specs"* — so spec-as-source risks *"the downsides of both MDD and LLMs: Inflexibility and
non-determinism."*

**NOT INDEPENDENT** — martinfowler.com is [[thoughtworks]]' own publishing channel and she is a
Thoughtworks Distinguished Engineer. She is a *primary* for her own trials; she is **not** external
corroboration for Thoughtworks-originated framings. Note also that she is **pro-spec-first herself**
(*"the general principle of spec-first is definitely valuable in many situations"*) — filing her as an
SDD opponent is wrong. Through-line across her three captured pieces
(also [[bockeler-tdd-inside-the-agent-loop]], [[bockeler-context-engineering-coding-agents]]): **an
agent following instructions is not the same as the instructions being right.**
```

### 15.4 — `wiki/entities/nick-tune.md` — UPDATE

```markdown
**Event-sourced agent loops (2026-03-04).** [[nick-tune-event-sourced-claude-code-workflows]] is the
third of a series (workflows as state machines → declarative DSLs → fully event-sourced, the last
suggested to him by **Yves Reynhout**) and the KB's only source that applies [[event-sourcing]] to the
**agent loop** rather than to the domain: persist only events, derive state by replay, and read
per-state dwell time, rejection counts and hook-denial counts off the log — then feed the events back to
Claude to rewrite the harness. Code in his `autonomous-claude-agent-team` repo.
**NOT INDEPENDENT · IMPRESSION NOT MEASUREMENT** — his own harness, personal projects, and the
*"15 minutes in RESPAWN vs 2 minutes DEVELOPING"* reading is from one session, which he states.

**Hold his two positions together; the pair is the interesting thing.** He instruments and automates the
**loop** to the point of having an agent optimise its own harness, while doubting he can build rapport
with a **domain model** he did not hand-code — *"the domain model is going to be worse because I'm
clearly missing some nuances… Maybe it's not even possible"*
([[tune-no-rapport-with-a-model-you-didnt-code]], 2026-08-28).
That is a boundary claim — delegate the process, author the model — and it cuts against the
[[martin-dilger]]/[[eventmodelers-ai]] thesis that a sufficiently good spec DSL lets agents do the
modelling. With his [[nick-tune-enforced-application-architecture-agents-humans|model-as-constraint]]
position it makes him the KB's most fully articulated third voice in
[[model-as-code-vs-model-as-language]].
```

### 15.5 — `wiki/entities/martin-dilger.md` — UPDATE

```markdown
## Five short-form notes and two articles (2026-06 → 2026-09), and a date correction

**A date the KB had wrong.** [[dilger-loop-engineering-never-argue-with-agent]] (**2026-06-10**) already
contains the full Event Modeling Agent Harness mechanic — Draft → Planned → In Progress → Done, board
subscription, claim-lock, timeout recovery — a **week before**
[[dilger-event-modeling-agent-harness]] (2026-06-17), which the KB has treated as the origin. It is
also his fullest statement of loop engineering, including the rules *"I never argue with an agent"*,
*"do not fine-tune the loop"*, and the load-bearing *"if something fails, the problem is in the spec,
not the prompt."*

**The late-August/September position, read as one argument.** Five short notes in four days:
[[dilger-ux-as-first-class-in-spec-driven-development]] (08-31) — *"Spec-Driven Development does not
need Markdown Files"*, UX and business rules carried by screens and [[given-when-then|GWT]];
[[dilger-only-engineers-care-about-consistent-systems]] (09-01) — AI is *"one more handover"* in an
already-lossy chain, and *"only engineers care about absolutely consistent systems"*;
[[dilger-git-as-primary-persistence-for-event-models]] (09-02) — git as **primary** persistence for the
model, one repo per board, branching, BYODS, WORM auditability;
[[dilger-communicating-intent-to-an-agent-needs-a-dsl]] (09-03) — *"What used to be a Jira Ticket became
Markdown Files. Same old stuff, some new paint… What's missing is a DSL to unambiguously describe flow,
behavior + business rules"*; [[dilger-agentic-engineer-program-stack-agnostic-spec]] (09-03) — the
3-week paid programme, and the falsifiable claim that one model drives builds in five stacks in
parallel. Plus [[dilger-ui-only-interactions-filtering]] (07-31), the method clarification that UI-only
interactions are Views, and [[dilger-goto-cph-2026-event-modeling-ai-native-software-design]], a
two-day GOTO Copenhagen masterclass at 11,000 DKK.

**The marker, and it applies to all of it.** EM-Studio / [[eventmodelers-ai]] is his commercial product,
the training programme is priced, the *Spec Driven* book ships 2026-10-16, and the two quantified claims
in this material are **his own figures with no independent corroboration anywhere in this KB**:
*"battle-tested over hundreds of projects by many companies"* (Event Modeling as a DSL) and
*"as I did for hundreds of engineers already"* (training). **VENDOR SELF-REPORT**; treat the framings as
positions to test, not findings.

**Two places he concedes ground worth recording.** Real users *"are perfectly fine correcting things
manually"* — an argument against the enforcement instinct in
[[dilger-keep-command-handlers-pure]]. And his handover diagnosis is
[[ng-spec-driven-development-is-waterfall-in-markdown|Ng's]] provenance objection reached from the
opposite camp: they agree the problem is who was in the room, and split only on what the room produces.
```

### 15.6 — `wiki/entities/adam-dymitruk.md` — UPDATE

```markdown
**"Agents need an audit trail, not a snapshot"** ([[dilger-podcast-episode-47-agentic-modeling-audit-trails]],
**date unresolved** — see the source page): *"Events are the truth, the full story, not just the current
state. Read models are derived and disposable. If an agent goes sideways, follow the event trail, find
the divergence, fix it, replay. No mystery, no data surgery."* He is **endorsing, not originating** — the
hosts are relaying a LinkedIn post by Svet Angelov that is not captured in `raw/`. It is the crispest
statement of the KB's [[event-sourced-agentic-patterns]] thesis as an *agent requirement*, and the batch
supplies three independent implementations of it, at the domain, specification and loop layers.

Same episode, two more positions: **screens are legitimate model content** — *"all the arguments about
not having screens and design sessions is just gatekeeping by architect wannabes"*
([[screens-as-specification]]) — and a caution on agentic modelling: an over-eager agent flooding a
[[given-when-then|GWT]] list with edge cases *"can make a simple slice look far more complex than it
really is, since event modeling is visual"* ([[event-modeling-anti-patterns]]). He also restates
**specification by example** as the method's existing answer to over-specification: *"draw a few
representative example paths and trust the implementer to infer the rest."*
```

### 15.7 — `wiki/entities/eventmodelers-ai.md` — UPDATE

```markdown
**Platform changes recorded in the 2026-07 → 2026-09 captures** (all **VENDOR SELF-REPORT**; several are
announcements rather than reports of use):

- **Git as primary persistence, and BYODS** — one repository per board, branching supported, no
  relational database required, with Redis/S3/YAML/SharePoint named as possible stores and WORM-drive
  storage offered for auditability. Prior stores: Supabase/Postgres, then SQLite (*"Both are live and
  used heavily"*, unquantified). The model store is itself event-sourced.
  ([[dilger-git-as-primary-persistence-for-event-models]], 2026-09-02 — **announced as being added**.)
- **Multi-Screen Views, HTML Views, built-in Query support**, and `npx @eventmodelers/cli init-modeling`
  to connect an agent in ~15 seconds ([[dilger-ui-only-interactions-filtering]], 2026-07-31).
- **Screen Preview** — hand-sketched screens, HTML mockups and Figma screens in one storyline
  ([[dilger-only-engineers-care-about-consistent-systems]], 2026-09-01).
- **The `/wdyt` gap-finding skill, worked and tuned** — an agent reads slices and posts
  clarifying-question comments; restricting it to comment only on what is *present* (no invented
  scenarios) turned ~100 noisy comments into useful ones. And **two agents (Claude Code + Hermes)
  modelling concurrently** alongside Dilger, reported as *"indistinguishable from modeling with humans"*
  — **IMPRESSION NOT MEASUREMENT**.
  ([[dilger-podcast-episode-47-agentic-modeling-audit-trails]], **date unresolved**.)
- **Build Kits** named for Axon, Marten, Cratis, Emmett (Node) and Python, with a 12-month commercial
  EM-Studio licence bundled into the paid **Agentic Engineer** programme (on-prem hostable for
  enterprises); the *Spec Driven* book ships **2026-10-16**
  ([[dilger-agentic-engineer-program-stack-agnostic-spec]], 2026-09-03).
- **Channel note for the research config:** `eventmodelers.ai/docs/podcast` is a **separate and more
  current episode index** than podcast.eventmodeling.org — Episode 47 exists only there and appears in
  neither the RSS feed nor the `.org` index. It should be polled as its own channel.
```

### 15.8 — `wiki/entities/colin-eberhardt.md` — **CREATE**

```markdown
---
title: Colin Eberhardt
type: entity
created: 2026-09-04
updated: 2026-09-04
sources: [eberhardt-putting-spec-kit-through-its-paces]
tags: [spec-driven-development, agentic-coding, person, focus]
---

# Colin Eberhardt

**CTO of [[scott-logic]]**, a UK software consultancy, and author of the KB's most instrumented
hands-on [[spec-driven-development|SDD]] trial ([[eberhardt-putting-spec-kit-through-its-paces]],
2025-11-26). Until 2026-08-31 the wiki knew of him only as an unnamed "Scott Logic SpecKit trial"
reached second-hand through [[ng-spec-driven-development-is-waterfall-in-markdown|Ng]].

**Method:** deleted a ~1,000-line feature from his own hobby PWA (KartLog — go-kart race data; JS,
Firestore, SvelteKit) and rebuilt it with GitHub Spec Kit + Copilot, committing and timing every step,
then compared against his ordinary iterative workflow.

**Findings that travel:** 33m30 agent time, 689 loc, **2,577 lines of markdown**, 3.5 hrs review, and a
broken dev server — against 8m agent time, 1,000 loc, no markdown, 24 min review and no bugs his usual
way. *"Around ten times faster"* without SDD — **his own impression, not a measurement** (n=1, one hobby
app, one toolkit, feature previously built by him). The *"2,500 lines in the spec phase"* figure the KB
once carried was wrong: Specify alone was **230** lines; **Plan** was the bloated step at **2,067**.

**His argument, and it puts him in the model-as-code camp:** *"Code is law because it is formal language
you can reason about… Specifications, or at least ones expressed in the markdown format of Spec Kit,
lack this formality. They are not a law I would put my trust in."* Plus: code is now cheap and
disposable, so SDD fails to capitalise on the one thing agents changed; and specs are point-in-time
artifacts rarely revisited — the only argument in the KB against **spec-anchoring itself**, independent
of notation. He is not anti-documentation: architectural decisions and *why* are worth keeping
([[adr]], [[decision-trace]]).

**Hedges he states himself, and which should travel with the figures:** Spec Kit is immature; *"I am
willing to entertain the possibility that I am simply just using it wrong"*; he echoes
[[birgitta-bockeler|Böckeler's]] *"I wasn't quite sure what size of problem to use it for"*; and he
wonders whether an architect-reviewer "vibe engineer" is even the target audience. Verdict: *"an
interesting concept, a radical idea… But I don't consider it a viable process, at least not in its
purest form."*

_Related: [[scott-logic]] · [[spec-driven-development]] · [[model-as-code-vs-model-as-language]] ·
[[agentic-coding]] · [[vibe-modeling]]._
```

### 15.9 — `wiki/entities/francois-zaninotto.md` — **CREATE**

```markdown
---
title: François Zaninotto
type: entity
created: 2026-09-04
updated: 2026-09-04
sources: [zaninotto-spec-driven-development-waterfall-strikes-back]
tags: [spec-driven-development, agentic-coding, agile, person, focus]
---

# François Zaninotto

**Founder and CEO of [[marmelab]]** (a French development agency, maintainers of react-admin and Atomic
CRM), and author of *"Spec-Driven Development: The Waterfall Strikes Back"*
([[zaninotto-spec-driven-development-waterfall-strikes-back]], 2025-11-12 — 225 points on Hacker News).
The wiki previously knew him only as "**Marmelab**, independently", relayed in one sentence through
[[ng-spec-driven-development-is-waterfall-in-markdown|Ng]]; his title is close enough to Ng's
*"waterfall in markdown"* to suggest direct lineage, four months earlier.

**His seven failure modes** are the KB's fullest such list: context blindness, markdown madness,
systematic bureaucracy, faux agile, **double code review**, false sense of security, and diminishing
returns on brownfield (*"For large existing codebases, SDD is mostly unusable"*). The
**1,300-lines-of-markdown-across-8-files to display a date** figure the KB attributed to "Augment
Engineer" via Ng **originates here**, linked to a public PR.

**His distinctive argument is about audience, not volume:** *"You must be a business analyst to catch
errors during the requirements phase, and a developer to catch errors during design. As such, it doesn't
solve the problem it claims to address (removing developers), and it can only be used by the rare
individuals who master both trades. SDD repeats the same mistake as No Code tools."* And the structural
claim underneath: *"software development is fundamentally a non-deterministic process, so planning
doesn't eliminate uncertainty."*

**His alternative — "Natural Language Development":** a Lean-Startup loop (riskiest assumption →
simplest experiment → build → repeat), with a 3D sculpting tool built in *"about 10 hours"* with no spec
at all and session logs published. **NOT INDEPENDENT · self-report** — his own project on his own
company's blog, as the counter-example to the thing he argues against. *"80% of your time reading instead
of thinking"* is his stated opinion, not a measurement.

**The line worth keeping for the [[event-modeling]] thread:** his single frustration with coding agents
is that *"coding agents use text, not visuals… the focus should be on richer visual interactions"* —
which is the camp he is arguing against, agreed with unknowingly. See [[screens-as-specification]].

_Related: [[marmelab]] · [[spec-driven-development]] · [[agentic-coding]] · [[vibe-modeling]] ·
[[loop-engineering]] · [[birgitta-bockeler]]._
```

### 15.10 — `wiki/entities/scott-logic.md` and `wiki/entities/marmelab.md` — **CREATE (2 items, low priority)**

Short org stubs, so the two new people have employers with pages rather than dangling links. Both are
**consultancies/agencies with a commercial interest in development services**, which is the relevant
marker: neither is a neutral research body.

- **`scott-logic.md`** — UK software consultancy; [[colin-eberhardt]] is CTO; publishes at
  blog.scottlogic.com under CC BY-NC-SA 4.0. In the KB for
  [[eberhardt-putting-spec-kit-through-its-paces]], the most instrumented SDD trial captured. Tags:
  `[org, spec-driven-development, agentic-coding]`.
- **`marmelab.md`** — French development agency; [[francois-zaninotto]] is founder/CEO; maintainers of
  react-admin and Atomic CRM (the codebase used in the Kiro example). In the KB for
  [[zaninotto-spec-driven-development-waterfall-strikes-back]] and its seven failure modes. Tags:
  `[org, spec-driven-development, agentic-coding]`.

---

## 16. `wiki/sources/dilger-describing-without-solving-burns-you-out.md` — one-line citation repair

**Not touched by this batch** (it belongs to an earlier ingest), but it carries the same mis-piped
wikilink as §1.3 and §14.

**Where:** line ~54.
**Find:** `[[tornhill-merge-conflicts-agentic-bottleneck|Tornhill]]'s *SDD and the Illusion of Known Scope*`
**Replace with:** `[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill]]'s *SDD and the Illusion of Known Scope*`

Also check `wiki/sources/tornhill-ai-readable-code-series.md` (lines ~48 and ~62): it names the article
in prose without a link and can now link it.

---

## 17. `wiki/index.md` and `wiki/log.md` — not owned by this batch

Suggested lines for the orchestrator.

**`index.md`** — 15 new source pages (§ top of this file) plus, if created, one new concept
`screens-as-specification` (*"the screen as first-class spec content, and the artifact non-developers can
review"*), and up to four new entities (`colin-eberhardt`, `francois-zaninotto`, `scott-logic`,
`marmelab`).

**`log.md`** — one line, e.g.:

```
## [2026-09-04] ingest   | Batch E: EM×agents + the SDD controversy (15 sources) — touched: 15 source pages new; 13 concepts + 6 entities updated, 1 concept + 4 entities created (per outputs/ingest-deltas/batch-e-em-agents-sdd.md). Both sides of the SDD dispute now grounded in primaries (Adzic 2025-09-29 · Böckeler 2025-10-15 · Zaninotto 2025-11-12 · Eberhardt 2025-11-26 · Tornhill 2026-05-28) — Ng is confirmed downstream, the Adzic "revenge of waterfall" attribution is corrected (it is his title as a question; he answers the BDD half "it does not, really" and is the warmest of the four), and the Eberhardt/Zaninotto figures are re-cited to primaries. Dilger's five September notes sharpen his position into a claim about the MEDIUM ("what's missing is a DSL to unambiguously describe flow, behavior + business rules"; "hundreds of projects" is HIS OWN FIGURE, uncorroborated). New mechanisms: git as PRIMARY persistence for event models (WORM auditability) as the proposed answer to Dymitruk's "audit trail, not a snapshot"; UX/GWT as first-class instead of markdown-derived. Tune's event-sourced Claude Code workflows = event sourcing turned on the AGENT LOOP (IMPRESSION NOT MEASUREMENT, NOT INDEPENDENT). Date corrections: Dilger's loop-engineering primary is 2026-06-10, a week before the "harness" page's 06-17; Episode 47 stays DATE UNRESOLVED and may be a previously unpolled channel. Citation repair: four pages piped "SDD and the Illusion of Known Scope" onto the wrong Tornhill source page.
```

---

## Closing note for the fidelity pass

Three things in this batch are easy to get wrong and were deliberately resisted:

1. **The SDD dispute is not "for vs against".** Adzic is warm; Böckeler practises spec-first and
   recommends it; Eberhardt rejects the *purest* form and defends the debate; Tornhill scopes himself to
   the strong form and explicitly declines the waterfall argument; only Zaninotto says SDD is *"a step
   in the wrong direction"* outright. Any page that flattens them into one anti-SDD front is wrong.
2. **Sceptic and advocate agree on the diagnosis more often than the wiki's framing suggests** — three
   times in this batch (Zaninotto/Böckeler + Dilger on markdown bloat; Ng + Dilger on handovers and
   provenance; Zaninotto + Dilger on visual interaction) — and split every time on the remedy. Present
   the agreements; they are load-bearing evidence that the *diagnosis* is real.
3. **Nothing in this batch measures model-first SDD.** Every figure is about document-generating
   toolkits, and every Dilger claim is a vendor self-report. The dispute is unresolved and this batch
   does not resolve it.
