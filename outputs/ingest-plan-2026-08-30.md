# Ingest plan — the raw/ backlog as of 2026-08-30

**46 raw captures** are genuinely un-compiled. Oldest waiting: 2026-03-04 (Morris). Last ingest ran 2026-08-16.

> **Correction to this morning's digest.** The digest reported "~60 un-ingested" from a filename check;
> the log's own running estimate said "~43". **The log was closer — the true number is 46.** 27 raw
> captures are already compiled under a source-page slug that differs from their filename (e.g. raw
> `willison-what-is-agentic-engineering` → wiki `willison-agentic-engineering-patterns`), which defeats
> naive filename matching. See `outputs/lint-2026-08-30.md`, finding #1.

This plan groups the 46 into **10 themed batches**, ranked by focus priority (business capabilities →
Event Modeling × agents → design substrate). Batches are themed rather than chronological on purpose: a
batch that shares a thesis produces one coherent set of concept-page edits, whereas ingesting by date
scatters edits across the wiki and re-opens the same pages repeatedly.

**How to use this:** reply with a batch letter (e.g. *"run batch A"*), or a pair (*"A then B"*). Batches
are independent — reorder freely. Word counts are of the raw material, which is the honest predictor of effort.

---

## Recommended order

**B → A → C** first. B is one file and it's your flagged-important focus area. A is small and the
highest-value on-focus material in the queue. C resolves a live contradiction that is currently sitting
in a log entry rather than in the wiki.

---

### Batch B — Business capabilities ★ flagged-important focus
*1 file, 9,941 words.*

| File | Date | Words |
| --- | --- | --- |
| `articles/sadalage-chandrasekaran-making-data-ready-for-agentic-ai` | 08-27 | 9,941 |

**Why first, and why alone.** The good news from the recount: the rest of the capability corpus —
Devadoss's CEAD paper, Fritzsche's capability-over-layers and RPU/reactor pieces, Skelton, Homann's 2006
formal definition — **is already compiled**. `business-capabilities` is one of the better-sourced pages
in the wiki. This single Thoughtworks article is the only capability material outstanding, and it is the
one that most changes the page: a capability model where every capability declares permissions, an owner,
**preconditions checked against live state at the moment of acting**, and a **reversibility class**, with
the claim that *reversibility predicts safe autonomy better than transaction size*. That is a new axis for
`autonomy-ladder`, not a restatement.

Also carries: "agentic lineage" (traces recording *why*, keyed to EU AI Act Art. 12/19), "retrieved text
informs, it never gates" as a structural answer to prompt injection, "design capabilities, not endpoints"
with a Radar HOLD on naive API-to-MCP conversion, and the AtScale datum (text-to-SQL <20% on a raw schema
→ >92.5% with a semantic layer, same model).

**Expected wiki impact:** `business-capabilities`, `autonomy-ladder`, `agent-explainability`,
`context-engineering`, `prompt-injection`, `model-context-protocol`; new entities for
Sadalage/Chandrasekaran.

---

### Batch A — The self-improving Event Modeling agent ★
*3 files, ~980 words.*

| File | Date | Words |
| --- | --- | --- |
| `notes/dilger-one-million-tokens-self-training-modeling-agent` | 08-27 | 458 |
| `notes/dilger-modeling-agent-improved-by-learning-loop` | 08-28 | 316 |
| `notes/dilger-todo-lists-storylines-one-scenario` | 08-15 | 204 |

**Why.** The 08-27 post is Dilger's always-on modeling harness (already compiled, 06-17) given a **grader**
— a corpus of hand-crafted good models it structurally diffs against and then rewrites its own skills from.
The 08-28 post reports what that produced, plus the failure mode. Together they are the KB's first worked
instance of Event Modeling used as a *verification rubric* for a self-improving agent, which is the exact
claim `event-modeled-agent-design` has been asserting without evidence. Cheapest batch in the queue, highest
payoff per word.

The storylines note belongs here because the loop independently rediscovered storylines-over-plain-GWT for
read models attached to automations — a nice case of the agent converging on something Dilger had already
written down separately.

**Expected wiki impact:** `loop-engineering`, `event-modeled-agent-design`, `agent-harness`,
`given-when-then`, `martin-dilger` (stub), `eventmodelers-ai`; likely a new page for the **token-budget
quality cliff** ("ever 5th iteration or so is really bad… the model taking shortcuts when it reaches certain
budget thresholds"), which nothing in the wiki covers.

---

### Batch C — The DSL-vs-code controversy
*2 files, ~2,170 words.*

| File | Date | Words |
| --- | --- | --- |
| `articles/miller-jasperfx-critterstack-ai-event-modeling-strategy` | 08-21 | 1,873 |
| `notes/dilger-markdown-is-a-suggestion-dressed-as-a-spec` | 08-25 | 297 |

**Why.** `wiki/concepts/model-as-code-vs-model-as-language.md` was written today, and it is currently the
only page in the wiki whose two central quotes cite raw files rather than source pages — because these two
captures have no source pages. This batch fixes that, and slots Miller's position into
`agent-readable-model-artifacts`, whose ladder he explicitly rejects. The supporting Miller/Dilger tooling
captures I'd expected to need here (AI Skills 1.6.0, draw.io-model-in-code, the EmLang knowledge hub, the
Miro/Eventmodelers alliance) all turn out to be **already compiled**.

**Expected wiki impact:** `model-as-code-vs-model-as-language` (grounding — revisit immediately after),
`agent-readable-model-artifacts`, `vertical-slice-architecture`, `jeremy-miller`, `critter-stack`,
`spec-driven-development`.

---

### Batch D — Dilger's method extensions
*10 files, ~3,300 words. Focus: Event Modeling method-wide.*

`dilger-element-slice-chapter-story-context-ladder` (08-25) · `dilger-slicing-keeps-the-cost-curve-flat-triplet-architecture` (08-29) · `dilger-spec-driven-development-needs-four-phases` (08-29) · `dilger-event-modeling-is-a-shift-left-on-the-organization` (08-25) · `dilger-join-considered-harmful` (08-24) · `adaptech-given-when-then-executable-tests-before-implementation` (08-28) · `dilger-trust-needs-to-be-engineered` (08-15) · `dilger-lights-off-software-factory-dead-end` (08-16) · `dilger-voice-to-sketch-api-event-sourced-board` (08-14) · `dymitruk-move-prompts-into-scripts-deterministic` (08-15)

**Why together.** All short, all method-level, all Dilger/Dymitruk. The keystone is the **Element → Slice →
Chapter → Story → Context** vocabulary ladder — a real method extension with no page anywhere in the wiki.
The four-phase SDD post and the slicing-economics post both feed `spec-driven-development`. Note the wiki
already holds `dilger-triplet-flexible-agent-enabled-architecture`, so the 08-29 Triplet post is a
restatement to fold in, not a new concept.

**Expected wiki impact:** new concept page for the vocabulary ladder; `slice`, `spec-driven-development`,
`event-modeling`, `given-when-then`, `software-factory` (stub), `martin-dilger` (stub).

---

### Batch E — Verification instead of reading
*4 files, ~3,600 words.*

`tornhill-controlling-the-uncertainty-machine` (08-20, 1,284w) · `addyosmani-agentic-code-quality` (08-08, 1,802w) · `willison-more-than-just-code-review` (08-22, 237w) · `willison-conceptual-integrity-and-counting-lines-of-code` (08-19, 666w)

**Why together.** Three practitioners reached the same conclusion independently inside two weeks — reading
every line is the wrong unit — and each replaced it with a different verification artefact. The triangulation
is the point and only shows if they're compiled together. Tornhill's reviewed-e2e-test boundary is arguably a
slice's given/when/then arrived at from outside the method, which is worth stating explicitly on
`given-when-then`.

---

### Batch F — Loop engineering & harness evolution
*13 files, ~21,000 words. The largest cluster.*

`addyosmani-human-judgment-relocates` (08-21, 4,859w) · `miracle-my-loop-engineering-workflow` (08-10, 3,830w) · `addyosmani-practical-loop-engineering` (08-14, 3,028w) · `mcateer-evolution-of-the-agent-harness` (08-22, 2,071w) · `voss-what-the-hell-is-a-loop-anyway` (07-29, 1,977w) · `morris-humans-and-agents-in-software-engineering-loops` (03-04, 1,943w) · `macmanus-schott-react-for-agents-flue-meta-harness` (08-15, 1,579w) · `dilger-loop-engineering-never-argue-with-agent` (06-10, 1,472w) · `macmanus-pocock-wayfinder-skill-fog-of-war` (08-20, 1,441w) · `breunig-harnesses-are-situated-agents` (08-14, 866w) · `breunig-fable-and-the-end-of-the-free-lunch` (08-23, 540w) · `papers/evo-bench-can-language-models-improve-agent-harness` (08-10) · `papers/sbco-verifier-grounded-harness-optimization` (08-10)

**Why together.** Heavily internally-referential; piecemeal ingest means re-editing `loop-engineering` and
`agent-harness` a dozen times. McAteer's Harness-Bench figure (52.4→76.2 across harnesses, same model, 106
tasks) is the quantitative anchor the thread currently lacks. **Ingesting Morris also resolves one of the
wiki's two dangling links** — `ng-spec-driven-development-is-waterfall-in-markdown` forward-links to it.

**Cost warning:** budget two sessions. Sensible split: Osmani/Breunig/McAteer core first; the two arXiv
papers and the practitioner workflows second.

---

### Batch G — The bounds on agent autonomy
*2 files, ~860 words.*

`willison-breaking-claude-code-auto-mode` (08-27) · `willison-just-a-rumour-of-a-bug` (08-28)

**Why together.** Two consecutive captures bounding the same question from opposite ends — *exposure* (the
classifier permitted the malware and then blocked the cleanup) and *capability* (a hint of a bug yields an
exploit in ten minutes). Add Batch A's budget-threshold cliff and you have three independent limits on
unattended loops, which is a concept page in itself. Small, fast, sharpens `unattended-coding-agents`.

---

### Batch H — Production evidence at scale
*4 files, ~8,100 words.*

`zalando-agentic-engineering-snapshot` (08-14, 3,925w) · `nick-tune-enforced-application-architecture-agents-humans` (08-13, 1,888w) · `laycock-citizens-build-agents-execute-experts-govern` (08-19, 1,279w) · `laycock-the-conductor-developer` (07-31, 1,022w)

**Why together.** Non-vendor accounts of agents at organizational scale. Zalando's 33%-auto-approved /
20–40% lead-time numbers and its cyclomatic-complexity inflection study are the only hard organizational
data in the queue; Laycock and Tune supply the governance framing around it.

---

### Batch I — Event sourcing substrate
*4 files, ~9,000 words.*

`fritzsche-why-the-entity-model-is-an-illusion` (08-26, 1,407w) · `fritzsche-thinking-in-events` (07-03, 2,483w) · `dudycz-vertical-slices-ownership-and-external-dependencies` (08-10, 3,828w — **20 days waiting**) · `dudycz-fixing-bugs-in-event-sourcing` (07-27, 2,660w)

**Why together.** Smaller than expected — most of the Fritzsche CCC/DCB corpus is already compiled, which is
itself the answer to the Topic-3 complaint (see `outputs/topic-3-watch-diagnosis-2026-08-30.md`). What remains
is Fritzsche's sharpest statement of entity-vs-event and Dudycz's VSA-ownership piece, which is the explicit
VSA↔slice mapping the watch config has wanted since June.

---

### Batch J — Evergreen backfill
*3 files, ~2,400 words.*

`dilger-ui-only-interactions-filtering` (07-31, 954w) · `miller-open-core-model-sustainable-oss-dotnet` (08-28, 1,087w) · `dilger-goto-cph-2026-event-modeling-ai-native-software-design` (342w)

**Why last.** Evergreen or largely off-thread. Miller's Open Core post matters only for one line — JasperFx
has "commercial tools related to AI assisted development and Event Modeling coming soon" — plus a
counterweight to `dudycz-fork-can-you-own-it` on vibe-coding your dependencies.

---

## Two notes on the queue

1. **It's healthier than it looked.** 46, not 60; the capability corpus is compiled; the Fritzsche substrate
   is largely compiled; the Miller/Dilger tooling captures are compiled. The genuinely overdue material is
   concentrated in **loop engineering (13 files)** and **Dilger's August method posts (10 files)**.
2. **Only Batch F is decaying.** It's a fast-moving thread where each capture reframes the previous ones, so a
   stale partial compile is worse than none. Everything else keeps.
