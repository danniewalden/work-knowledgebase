# Batch F — two-session execution plan

**13 files, ~21,000 words. The largest cluster in the queue and the only decaying one.**

Written 2026-08-31, after batches B/A/C ran. Supersedes the one-paragraph sketch in
`outputs/ingest-plan-2026-08-30.md`, which recommended "Osmani/Breunig/McAteer core first; the two arXiv
papers and the practitioner workflows second." **I'd split it differently — see below.**

---

## Why this cluster decays and the others don't

Every other batch is a set of independent claims that keep. This one is a **conversation**: Voss is
answering Steinberger, Osmani and Cherny; McAteer is answering Kaiser; Breunig is answering Harrison
Chase; the two arXiv papers are measuring what Dilger and Osmani assert. Each capture reframes the
previous ones. A stale partial compile is worse than none, because `loop-engineering` would then hold
half a conversation and read as settled when it isn't.

Concretely: `loop-engineering` is already the wiki's largest concept page (27 KB, 16 sections) and
`agent-harness` is one of its smallest (3.7 KB, 4 sections). Ingesting these 13 files piecemeal means
re-opening both a dozen times.

---

## The change I'd make to the split

**Don't lead with Osmani.** The plan's original ordering puts the practitioner material first, but three
of these files are *definitional* and the rest attach to them. Ingest the vocabulary first, fix the two
concept pages once, then hang everything else off a stable frame.

The load-bearing case: **Laurie Voss's "What the Hell Is a Loop, Anyway?"** exists specifically because
"the people talking about loops aren't all discussing the same thing — I counted at least four distinct
architectures hiding behind that one word." Our `loop-engineering` page was built from advocates
(swyx, Osmani, LangChain) who each meant a different thing. Compiling more advocates before compiling the
disambiguation deepens the confusion the page already has.

---

## Session 1 — the definitional spine (4 files, ~6,700 words)

| File | Author, date | Words |
| --- | --- | --- |
| `voss-what-the-hell-is-a-loop-anyway` | Laurie Voss, O'Reilly Radar, 07-29 | 1,977 |
| `breunig-harnesses-are-situated-agents` | Drew Breunig, 08-14 | 866 |
| `mcateer-evolution-of-the-agent-harness` | Dan McAteer, Latent.Space, 08-22 | 2,071 |
| `morris-humans-and-agents-in-software-engineering-loops` | Kief Morris (Thoughtworks), 03-04 | 1,943 |

**Read in that order.** Voss defines the word, Breunig defines the neighbouring word, McAteer supplies the
dynamic that connects them over time, Morris supplies the antecedent that shows the taxonomy predates the
hype.

**What each contributes:**

- **Voss — the disambiguation.** At least four distinct architectures hide behind "loop," starting with
  the execution loop (the agent's own act–observe–decide cycle, which "nobody designs"). He is explicitly
  writing at "the peak of the hype cycle," tracing the June-2026 moment — Steinberger's "design loops
  that prompt your agents," Cherny's "I write loops; the loops do the work," Osmani's essay. **This should
  become a top-of-page vocabulary section on `loop-engineering`,** and every existing section on that page
  should be checked against it: several probably conflate two of his four.
- **Breunig — a harness is a *situated agent*.** Builds on Harrison Chase's four components (system
  prompt, planning tool, file system, subagents) and surveys the August-2026 wave: Databricks Omnigent
  (a meta-harness calling Claude Code/Codex/Pi), the fully modular DeepSeek Harness, Block's Buzz,
  YC's QM (org-shaped scoping — per-employee/room/project memory, credentials, sandboxes), Cloudflare's
  Flue (declarative, *hides the loop*), Meta's Muse Code (**model co-trained with the harness**). The KB's
  strongest definitional primary for `agent-harness` since Böckeler's guides/sensors framing.
- **McAteer — the absorption thesis, and the batch's quantitative anchor.** Models absorb the harness into
  their weights, engineers delete what got absorbed, and "what remains is a harness for **human
  attention** rather than for the model." Opens on the Christmas-2025 step change and quotes Lukasz
  Kaiser on how hard it is to attribute. Carries the Harness-Bench figure the whole thread lacks:
  the same model over the same **106 tasks** in different harnesses scored **52.4 to 76.2 — a
  23.8-point spread with zero change to the model.** "Half the agent is the harness."
- **Morris — the antecedent (an accept/reject call for you).** Published 2026-03-04, captured deliberately
  out-of-window as a gap-filler. Names the **out-the-loop / in-the-loop / on-the-loop** taxonomy and "the
  agentic flywheel" *four months before* Osmani's "Own the Outer Loop" and LangChain's hill-climbing loop,
  both already in the wiki. The capture note flags it for your accept/reject. **My recommendation: accept.**
  It changes the provenance story on two pages from "named in July 2026" to "named in March and
  independently renamed in July," which is a materially different claim about how settled this vocabulary
  is. It also **resolves dangling link #1** —
  `ng-spec-driven-development-is-waterfall-in-markdown` forward-links to it.

**Expected page impact:** `loop-engineering` (vocabulary section + a pass over existing sections for
conflation), **`agent-harness` substantially rewritten** — it currently cannot carry Breunig or McAteer —
`harness-engineering`, `agent-legibility`; new entities for Laurie Voss, Dan McAteer, Kief Morris
(Drew Breunig now exists in `watch-config.json` but has no wiki entity page yet).

**Stop here and check the diagram before starting session 2.** If `agent-harness` still reads thin after
Breunig and McAteer, the problem is the page's shape, not the sources — fix it before adding nine more.

---

## Session 2 — practice and measurement (9 files, ~14,300 words)

Ordered so each sub-group closes a question the previous one opens.

**2a — the practitioner loops (4 files, ~9,200 words)**

`addyosmani-human-judgment-relocates` (08-21, 4,859w) · `addyosmani-practical-loop-engineering`
(08-14, 3,028w) · `miracle-my-loop-engineering-workflow` (Andrew Miracle, 08-10, 3,830w) ·
`dilger-loop-engineering-never-argue-with-agent` (06-10, 1,472w)

Osmani's pair is the governance answer to session 1's dynamic: **"Human judgment doesn't leave the
software factory. It relocates."** — humans upfront on product intent, system design and the quality bar;
review where automated back-pressure breaks; and the sharp caveat **"number of checks ≠ quality."** He
also asks the question the `software-factory` page never does: *do you really need a factory yet?*
"Practical Loop Engineering" is the concrete counterpart (5–10 parallel agents; delegate fully only where
the stopping conditions and constraints are clear). Miracle's "triangle of loops" is an independent
practitioner topology with an unusual artifact — a **trust-level statusline (L2, 50 points)** — worth
comparing to `autonomy-ladder`. Dilger's is the oldest and the odd one out: *"clean iterations with
recorded learnings outperform long, polluted conversations"* — a context-hygiene claim that belongs as
much to `context-engineering` as to loops, and it now reads as the ancestor of his 2026-08 self-training
loop ([[dilger-one-million-tokens-self-training-modeling-agent]], ingested today).

**2b — harnesses as products (3 files, ~3,400 words)**

`macmanus-schott-react-for-agents-flue-meta-harness` (08-15, 1,579w) ·
`macmanus-pocock-wayfinder-skill-fog-of-war` (08-20, 1,441w) ·
`breunig-fable-and-the-end-of-the-free-lunch` (08-23, 540w)

Schott's Flue 2 brings **React-style "Agent Hooks"** to a meta-harness and argues agents are *defined by*
their harnesses — the applied form of Breunig's thesis, and a design-pattern borrowing worth naming.
Pocock's `/wayfinder` is a concrete **skill** artifact for the fog-of-war of greenfield planning, which
`loop-engineering`'s five-primitives section describes abstractly and never instantiates. Breunig's
"Fable & The End of the Free Lunch" is the economic frame: the Moore's-Law analogy — when capability
doubles every 18 months you don't optimize; when it stops you think about architecture — applied to
model pricing and harness efficiency. Short, and it reframes the whole thread as an **economics** story
rather than a capability one.

**2c — the measurement (2 papers, arXiv, both 2026-08-10)**

`evo-bench-can-language-models-improve-agent-harness` · `sbco-verifier-grounded-harness-optimization`

Save these for last, and read them **against the pages written today** — this is the connection the
original plan predates and the strongest reason not to defer Batch F much further:

- **Evo-Bench** benchmarks *harness evolution* — an agent optimizing its own operating harness — and is
  built specifically to "isolate harness improvements from base model strength" and "prevent
  task-specific overfitting." Those are precisely the two unanswered objections the new
  [[token-budget-quality-cliff]] page and the self-training-loop section of `loop-engineering` raise about
  Dilger's setup (one local model; the same requirements re-modeled each round). A benchmark designed to
  isolate exactly those confounds is the right instrument to judge his claim by.
- **SBCO** does verifier-grounded harness optimization for planning agents, situating itself against the
  Darwin Gödel Machine and Huxley Gödel Machine self-referential lineage — and notes those methods
  *require the competence to perform the task to align with the competence to improve the harness.*
  That is a formal statement of `loop-engineering`'s standing grader-leak question, and it bears directly
  on why Dilger's artifact-corpus rubric behaves differently from a scalar grader.

**Expected page impact:** `loop-engineering`, `software-factory`, `unattended-coding-agents`,
`autonomy-ladder`, `context-engineering`, `agent-harness`, `token-budget-quality-cliff`; likely a new
concept page for **harness absorption** (McAteer's thesis) if session 1 doesn't already force one, and
possibly one for **skills as artifacts** off Pocock. New entities: Fred Schott, Matt Pocock,
Andrew Miracle, Richard MacManus (or treat MacManus as a *venue* — he interviews rather than argues, and
two of these are his interviews; a `latent-space` entity may serve better than an author page).

---

## Sequencing notes

- **Two sessions, not one.** 21,000 words with a concept-page rewrite in the middle is more than one pass
  should carry, and session 1's output determines how session 2's material is filed.
- **Don't split 2c off into a third sitting.** The papers are the only external measurement in the batch;
  deferring them again leaves the thread advocate-only, which is the standing caveat on `loop-engineering`
  ("built almost entirely from advocate/practitioner primaries").
- **Check for overlap before capturing more.** `watch-config.json` now lists three arXiv harness/loop
  papers as candidate primaries (2607.00038, 2605.25665, 2604.17025). Verify none of them *is* Evo-Bench
  or SBCO under a different identifier before filing anything new.
- **After session 2, re-run the lint.** This batch touches the two largest pages in the KB plus half a
  dozen neighbours; it is the most likely thing in the queue to introduce contradictions.

## What's left after Batch F

40 files in the backlog as of today. Batch F is 13 of them, and the largest remaining clusters are
**D** (Dilger's method extensions, 10 — includes the un-written `triplet-architecture` concept page and
the Element→Slice→Chapter→Story→Context vocabulary ladder), **E** (verification instead of reading, 4),
**H** (production evidence at scale, 4) and **I** (event-sourcing substrate, 4 — includes the
21-day-old Dudycz VSA-ownership piece, the oldest on-focus capture in the queue).
