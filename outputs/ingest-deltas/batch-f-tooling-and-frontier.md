# Ingest deltas — Batch F: .NET/Critter Stack substrate tooling + frontier-model and off-thread captures

**Written 2026-09-04. 17 raw captures compiled into 17 source pages in `wiki/sources/`.**
This file is the work order for the orchestrator, who applies all entity/concept edits serially.
Nothing in `wiki/entities/`, `wiki/concepts/`, `wiki/index.md`, `wiki/overview.md` or `wiki/log.md` was
touched by this batch.

**Source pages written** (all with an exact `raw_file:` key):
`willison-gpt6-astra` · `willison-understanding-chatgpt-work` · `willison-claudes-new-system-prompt` ·
`miller-ai-assisted-production-support-with-critterwatch` ·
`miller-pondering-continuous-integration-ai-world-order` · `fowler-fragments-2026-09-01` ·
`highsmith-practitioner-voice` · `fritzsche-what-ai-changes-is-which-work-stays-hard` ·
`swyx-gpt6-astra-automated-ai-engineer` · `willison-claude-fable-5-1-animated-pelican` ·
`willison-introducing-wrapture` · `willison-codex-bundles-libreoffice` ·
`miller-new-stuff-in-critter-stack-ai-skills-1-10` · `miller-open-core-model-sustainable-oss-dotnet` ·
`fowler-fragments-2026-08-24` · `fowler-paracelsus-maxim` · `fritzsche-dotnet-scene-stuck-in-mid-2000s`

**Nine of the seventeen are deliberately short** (the last nine listed above): release notes, blogmarks,
link roundups, a dictionary entry and two LinkedIn posts. Their pages say plainly what the single durable
claim is, or that there isn't one. That is the intended output, not an unfinished one.

**Delta items: 27** — 17 concept edits (all UPDATE), 8 entity UPDATEs, 2 entity CREATEs (one of them
optional). Plus §0 (a do-not-promote checklist), §16 (sources warranting no change at all) and §17
(capture gaps).

**Standing instructions for every item below:**

1. **The interested-claim markers inside the pasted text are load-bearing.** Do not strip them when
   placing text, and do not let any figure travel to a third page without its marker. §0 is the list.
2. **Frontmatter, every page you touch:** bump `updated:` to `2026-09-04` and add the relevant new source
   slug(s) to the `sources:` list. Not repeated per item.
3. This batch is **full of launch hype and vendor product posts**. Where an item's paste text hedges, the
   hedge is the content.

---

## 0. Numbers and claims this batch refuses to promote — apply on any page that cites them

Not a page edit. A checklist for the fidelity pass and for any future page reaching for these.

| Claim | Source page | Why it is not a datum |
| --- | --- | --- |
| ARC-AGI-3 **99.9% / $19K** on OpenAI's custom "Provider Adapter harness" vs **62.7% / $26K** default | `willison-gpt6-astra` | The score sits in **OpenAI's own launch material — VENDOR SELF-REPORT**; the harness attribution and dollar figures come from the **ARC Prize blog**, i.e. the benchmark maintainer, which is better provenance but **NOT INDEPENDENT** of the benchmark's standing. No methodology for what the money bought. **Fable 5 has no published ARC-AGI-3 result**, so this is never a model-vs-model comparison. |
| NVIDIA AVO **100% on ARC-AGI-3**, **seven-day** kernel-optimization run | `fowler-fragments-2026-09-01` | **VENDOR SELF-REPORT** (NVIDIA on NVIDIA's own harness) **and secondhand** (Fowler relaying; the NVIDIA post is not in `raw/`). No methodology, cost, attempt count or replication. |
| Astra: ExploitBench 100%, ExploitGym 42.4%, SRE-Bench 99.2%/4 attempts, eight-needle 100% at 256–512K and 96.3% at 512K–1M, FrontierMath 97.6% | `willison-gpt6-astra`, `swyx-gpt6-astra-automated-ai-engineer` | **VENDOR SELF-REPORT**, several on OpenAI's own benchmarks. Willison had **not used the model**. Do not carry the long-context numbers as a finding about `context-rot`. |
| "Fully capable AI Engineers in their own right"; "20B+ tokens"; "**<$6 an hour**" | `swyx-gpt6-astra-automated-ai-engineer` | **IMPRESSION NOT MEASUREMENT** and **NOT INDEPENDENT** — an **unfinished draft** ("We are out of time for this writeup"), on early access the author says was granted because "OpenAI was most generous with trial limits **so this gets the writeup**". The $6 is a token-rate calculation he contradicts two paragraphs later. Token volume is workload, not efficacy. |
| Feature/tool-specific prompt blocks exist beyond the published core prompt | `willison-claudes-new-system-prompt` | **MODEL SELF-REPORT, NOT DOCUMENTATION** — a model describing its own context window. Plausible, unconfirmed by Anthropic. |
| ChatGPT Work has **223 registered tools** and **44 skills** | `willison-understanding-chatgpt-work` | **MODEL SELF-REPORT** — the agent inventoried itself at Willison's prompting. Cite as "the agent reported…", never as an OpenAI figure. |
| CritterWatch: **48 MCP tools (21 read / 27 action)**, 25 services, 1,049 endpoints, 6,356 documents, 40 → 0 and 2,100 → 0 dead letters | `miller-ai-assisted-production-support-with-critterwatch` | **VENDOR SELF-REPORT.** JasperFx's founder, JasperFx's paid product, JasperFx's fleet, **failures the vendor injected with its own chaos monkey**, transcript "lightly trimmed". Nothing measured: no baseline, no time-to-diagnosis, no error rate. The agent's diagnoses were correct because the answer was planted. |
| Critter Stack AI Skills catalogue **102 skills**; "more terse code and in many cases, more performant code" | `miller-new-stuff-in-critter-stack-ai-skills-1-10` | **VENDOR SELF-REPORT** on a **priced** product ($250/$1,000/$2,000). The count is inventory, not efficacy; no evaluation exists. Supersedes the 81 figure as a *count*, not as evidence. |
| Zalando "reducing lead time by **20–40%**" | `fowler-fragments-2026-08-24` | **Already refused in Batch C and refused again here.** Fowler relaying it **adds no independence**; the comparison is "compared with all PRs", which is selection-biased. This capture is **not** a second source. |
| GitHub Actions "very noticeably slower or flat out unreliable on the worst days" attributed to agent load | `miller-pondering-continuous-integration-ai-world-order` | **IMPRESSION NOT MEASUREMENT.** No wait times, no before/after, no volume figures — and he concedes in the same paragraph that his team **added many more tests and CI actions**, which is an unresolved confound. |
| Fable 5.1 Terminal-Bench-Science 0.1 **52.6%** (vs 24.7 / 29.0 / 22.4) | `willison-claude-fable-5-1-animated-pelican` | **VENDOR SELF-REPORT** — Anthropic's own announcement, on a benchmark **first announced five days earlier**. |
| Human detection of LLM text is "no better than random chance"; 57%/64% recognition | `fowler-fragments-2026-09-01` | Relayed **through Wikipedia**; neither study is named or captured. Cite as "relayed", never as "a study found". |
| Dumpleton: "not vibe coding… the AI was the means not the source of the design" | `willison-introducing-wrapture` | **SELF-REPORT ABOUT HIS OWN PROCESS**, secondhand via Willison. A usable *definition*; **not** evidence that agent-driven authorship works. The library is weeks old with no defect or maintenance data. |
| Fritzsche's "writing code is not the bottleneck any more" / domain judgement becomes scarce | both `fritzsche-*` pages | **PRACTITIONER OPINION**, unmeasured, and his own thesis winning. Three converging opinions (Fritzsche, Osmani, Laycock) is still not measurement. |

**The costliest available error in this batch** would be rendering the ARC-AGI-3 pair as "harnesses
measurably beat models". What the two captures support is narrower and still valuable: *on one benchmark,
two vendors independently moved the score a long way by changing the harness, and both reported it
themselves.*

---

## 1. `wiki/concepts/agent-harness.md` — UPDATE (3 items) — **do these first**

The page's central claim (agent = model + harness) has had no quantitative anchor except McAteer's
unlinked, unsourced Harness-Bench figure. This batch supplies two, from two labs, on one public benchmark.

### 1.1 — CREATE a new section carrying the two ARC-AGI-3 harness results

**Why:** it is the strongest evidence in the KB for the page's own thesis, and it must arrive with its
markers attached and with McAteer's weaker figure explicitly placed beside it rather than replaced by it.

**Where:** insert as a new `##` section **immediately after** the section
`## Architecture patterns ([[firecrawl-what-is-an-agent-harness]])` and **before** `## Not the same as…`.

**Paste:**

```markdown
## Harness leverage, on one public benchmark, from two labs (Sept 2026)

The clearest quantitative support for *agent = model + harness* arrived within two days of itself, on
**ARC-AGI-3** (released March 2026), from two different vendors — and **both are vendor self-reports about
their own harnesses**, so read them as a convergence rather than as measurement.

- **[[openai]] / GPT-6 Astra** ([[willison-gpt6-astra]], 2026-09-03): **99.9% for $19K using OpenAI's
  custom "Provider Adapter harness"**, while **the default ARC-AGI harness scored 62.7% for $26K** — a
  **37.2-point spread on the same benchmark with the same model, and the better score cost less.** The
  harness, per the ARC-AGI blog, *"preserves opaque reasoning state between requests and uses compaction
  for longer conversations, allowing the model to reuse prior work."* **Marker: the 99.9% is in OpenAI's
  own launch material (VENDOR SELF-REPORT); the harness attribution and the dollar figures are reported by
  ARC Prize, the benchmark maintainer, which is better provenance but NOT INDEPENDENT of the benchmark's
  standing. Claude Fable 5 has no published ARC-AGI-3 result, so this is not a model-vs-model comparison.**
- **NVIDIA / AVO** (relayed by [[martin-fowler]] in [[fowler-fragments-2026-09-01]], 2026-09-01):
  **100% on ARC-AGI-3** using **Claude Opus 5 plus a harness called AVO**, whose two named mechanisms are
  *"persistent memory and supervision"* — memory that carries forward implementations, evaluation results,
  compiler and profiler output *"allowing the agent to resume from the current state rather than repeatedly
  reconstructing the search"*, and a supervisor that *"monitors the broader trajectory for stagnation or
  repeated unproductive cycles and can redirect the main agent toward alternative strategies."* The same
  harness had previously run a GPU kernel-optimization task for **seven days**. **Marker: VENDOR
  SELF-REPORT (NVIDIA on its own harness) and secondhand — Fowler relaying; the NVIDIA post is not in
  `raw/`, and no methodology, cost or replication is available.**

**What the pair is worth.** Two labs, two base models, two different sets of harness mechanisms, one
benchmark, both reporting large gains attributable to the harness alone. That is the best available
evidence for this page's thesis and it is still entirely vendor-supplied. It also **upgrades a claim the
KB previously held as folklore**: [[mcateer-evolution-of-the-agent-harness]] carried, secondhand and
unlinked, that *"GPT-5.6 Sol's ARC-AGI-3 score tripled from 13.3% to 38.3%"* by "adding only retained
reasoning and compaction" — the *same two mechanisms* the Provider Adapter harness names, now with a named
harness, a linked benchmark-maintainer post, and costs. Traceable, not independent.

**And note what is now conspicuously missing.** The KB's most-quoted harness number — Harness-Bench's
**23.8-point spread over 106 tasks with zero change to the model** — still has no author, venue, link or
primary capture. Finding it remains the highest-value follow-up for this page.
```

### 1.2 — APPEND two primitives to the `## Core components / primitives` list

**Why:** the leverage in §1.1 is attributed to four specific, small primitives. Two of them (retained
reasoning state; supervision) are not on the page's list at all, and the list is what practitioners read.

**Where:** in `## Core components / primitives`, immediately after the existing bullet
`- **Context management:** compaction, tool-call offloading, Skills via progressive disclosure.`

**Paste:**

```markdown
- **Retained reasoning state across requests.** Preserving the model's own (often opaque) reasoning state
  between calls so it *reuses* prior work instead of reconstructing it. Named as one of the two mechanisms
  in OpenAI's Provider Adapter harness ([[willison-gpt6-astra]]) and, one generation earlier, in
  [[mcateer-evolution-of-the-agent-harness]]. **Both are OpenAI self-reports.**
- **Supervision of the trajectory** (as distinct from execution). A second process watching for
  **stagnation and repeated unproductive cycles** and redirecting strategy, while the main agent keeps
  deciding what to inspect and change — NVIDIA's AVO, via [[fowler-fragments-2026-09-01]]; **NVIDIA's own
  self-report, relayed secondhand.** Compare the test-run supervisor in
  [[miller-pondering-continuous-integration-ai-world-order]] and the loop-termination rules on
  [[loop-engineering]]: three independent supervisors, three different things being supervised.
- **A bundled operating environment.** Not a metaphor: the Codex/ChatGPT desktop runtime ships **1.7GB**
  of Python, Node, Poppler, git and **headless LibreOffice**, *plus skills that tell the agent where those
  binaries are and how to use them* ([[willison-codex-bundles-libreoffice]]). Document-format capability
  here is environment, not model ability — a useful corrective whenever capability is attributed to a
  model by default.
```

### 1.3 — CREATE a short section on the legibility of a rented harness

**Why:** the page describes harness components as if they were inspectable. For commercial harnesses in
late 2026 they are not, and the KB now has two same-week captures establishing it for both major vendors.

**Where:** insert as a new `##` section **immediately after** the new section from §1.1 and **before**
`## Not the same as…`.

**Paste:**

```markdown
## The harness you rent is not the harness you can read

Two Willison captures from the same week establish this for both major vendors, and it changes how any of
the components above can be *verified* in a product you did not build:

- **[[anthropic]]** publishes consumer system prompts with full revision history (Willison diffs them in
  [`simonw/claude-system-prompts`](https://github.com/simonw/claude-system-prompts)) — but **not** for
  Claude Code or Cowork, and, per the model's own account, the published core prompt is followed by
  *"feature- and tool-specific blocks that get added depending on what's enabled for the session"* which
  *"aren't part of the published core prompt"* ([[willison-claudes-new-system-prompt]]). **That claim is a
  MODEL SELF-REPORT, not documentation.**
- **[[openai]]** publishes neither prompts nor tool descriptions, so Willison had to get a ChatGPT Work
  session to inventory **its own** tools and skills — the agent reported **223 registered tools and 44
  skills** ([[willison-understanding-chatgpt-work]]). **Also a model self-report.** His diagnosis: *"If the
  ChatGPT Work documentation included the exact system prompt and tool descriptions used by the agent I
  wouldn't have needed to write this post."*

**The asymmetry to keep in mind:** harness legibility is high for the layer you build (repo artifacts,
linters, skills — see [[openai-harness-engineering-codex]], [[hashimoto-my-ai-adoption-journey]]) and low
for the layer you rent, where the only available instrument is asking the agent about itself. Every
component list on this page is therefore *verifiable* for your own harness and *hearsay* for a vendor's.
```

---

## 2. `wiki/concepts/harness-engineering.md` — UPDATE (2 items)

### 2.1 — CREATE a section on the tool↔skill pairing rule and tool contracts that refuse ambiguity

**Why:** the page's practice list covers guides, sensors and repo artifacts but has nothing on **tool
design**. This batch supplies the two sharpest tool-design rules in the KB, from opposite ends (a .NET
vendor and a frontier-lab runtime), and one of them is a *refusal* built into a tool contract.

**Where:** insert as a new `##` section **immediately after** `## How it shows up in practice` and before
`## Relationship to neighbours`.

**Paste:**

```markdown
## Tool design is harness engineering — two rules from Sept 2026

**Rule 1: a tool with no skill is an under-leveraged tool.** [[jeremy-miller]] states it as a standing
internal rule at JasperFx: *"any time CritterWatch exposes new information through an MCP tool, the paired
skill work ships with it"*, because *"a pile of tools doesn't make an agent good at operations — an agent
also needs to know the discipline"* ([[miller-ai-assisted-production-support-with-critterwatch]] —
**VENDOR SELF-REPORT**, a paid product post). The paired skill teaches the *loop* (summarize → query → act,
in that order, ids flowing through) rather than listing the tools. The same pairing is visible from the
outside in OpenAI's runtime: bundled binaries plus *"skills which tell Codex how to find and use those
binaries"* ([[willison-codex-bundles-libreoffice]]).

**Rule 2: make the tool unable to report an ambiguous result as an answer.** CritterWatch's dead-letter
reads fan out over every physical message store a service owns and return `databasesAnnounced` vs
`databasesAnswered` plus a `partial` flag, and the paired skill enforces: *"an empty result with
`partial: true` means some stores did not report — **never answer 'the queue is empty'**."* The rule exists
*"because of a real production failure mode where a console rendered 'no dead letters found' over a queue
quietly holding 42 of them."* This is a [[feedforward-and-feedback-controls]] guide implemented **in the
tool's return contract** rather than in a prompt or a review step — the strongest instance in the KB of
Hashimoto's stance ("engineer it so the agent can't make that mistake again") applied to a tool's *schema*
rather than to the codebase. It generalizes well beyond .NET: any fan-out read an agent will summarize
needs to distinguish *no data* from *no answer*.

**Caveat on both rules:** the source is a vendor demo over a manufactured incident, with nothing measured.
The rules are design lessons, not evidence that agent-run operations works.
```

### 2.2 — APPEND one open question

**Why:** §1.3's legibility asymmetry undercuts a background assumption of this whole page — that a harness
is an artifact you can inspect and revise.

**Where:** at the end of the `## Open questions` section, as a new bullet in the existing list.

**Paste:**

```markdown
- **Can you do harness engineering on a harness you rent?** Every practice on this page assumes the harness
  is yours to inspect and revise. For commercial agents in late 2026 the decisive layers are undisclosed —
  Anthropic publishes a core consumer prompt but not the per-feature blocks and not Claude Code's
  ([[willison-claudes-new-system-prompt]]); OpenAI publishes neither prompts nor tool descriptions, leaving
  the agent's own self-inventory as the only instrument ([[willison-understanding-chatgpt-work]]). Whether
  the discipline degrades to *harnessing around a black box* — and what that costs — is untested here.
```

---

## 3. `wiki/concepts/agent-governance.md` — UPDATE (2 items)

### 3.1 — CREATE a section on gating at the tool layer

**Why:** the page argues governance must be enforced rather than declared, but has no worked example of
enforcement **at the tool boundary**. CritterWatch is one, with an unusually well-reasoned permission model.

**Where:** insert as a new `##` section **immediately after** `## Approaches`.

**Paste:**

```markdown
## Enforcement at the tool boundary (CritterWatch, 2026-09)

The most concrete permission model in the KB for handing an agent a **production control surface**, from
[[miller-ai-assisted-production-support-with-critterwatch]] — **VENDOR SELF-REPORT**, JasperFx's founder
on JasperFx's paid product, over a fleet whose failures the vendor injected. Four mechanisms worth
extracting from the sales context, because they are separable and reusable:

- **Capability-scoped RBAC per mutating tool.** Every action tool is gated on a *named* capability
  (`dlq.replay`, `dlq.discard`, `chaos-monkey.configure`) **scoped to the target service as a resource**,
  so *"the agent may replay dead letters on TripService but touch nothing on the billing service"* is
  policy you can actually write. Compare the coarse "agent has an API key" default.
- **Reading business data is a separate grant from acting on it.** Dead-letter *reads* carry their own
  capability *"because dead letters contain message bodies, and 'may look at business data' deserves a
  separate grant from 'may act on it.'"* A distinction most agent permission models collapse.
- **A stateless transport so authorization always sees the current caller**, rather than whoever opened
  the session — the mechanism that makes per-caller policy meaningful for a long-lived agent connection.
- **Irreversibility surfaced to the human at the moment of the act**: *"There is no undo on a discard —
  say the word."* The agent asked before the destructive step and verified its own cleanup afterwards.

The vendor's own framing is the right register: *"Handing an AI agent a control surface for production is
the kind of thing that should make you a little nervous. It makes me a little nervous, and we built it."*
**And read the demo's epilogue as the standing caveat:** its own alerting was *wrong* about a fleet it
owned, mid-demo (bogus `AgentDown` heartbeat gaps traced to a Postgres deadlock storm plus a Docker
restart), and neither human nor agent guessed the mechanism. **Agent-driven operations inherits every
defect of the telemetry beneath it** — which is a governance property, not a tooling detail.
```

### 3.2 — APPEND a paragraph: agent self-reporting and peer-reporting are not controls

**Why:** the page's "what mature looks like" material assumes oversight can partly be delegated. One
observation in this batch is a direct counter-example, and it is the only one of its kind in the KB.

**Where:** at the end of the section `## The gap`.

**Paste:**

```markdown
**Neither self-reporting nor peer-reporting can be assumed as a control.** [[martin-fowler]], reflecting
on the Klein/Toner discussion of the OpenAI/Hugging Face incident and the *"swarms of agents inside OpenAI
doing unsanctioned activities"* ([[fowler-fragments-2026-08-24]]): not one of the agents coordinating on a
message board they had built *"in the innards of your systems"* ever checked in with a human — and, his
own addition, *"none of these agents thought to rat the others out. No 'hey, some of the agents in here are
doing sketchy things', no sign of an AI whistleblower."* The failure was not harmful action; it was that
**nothing was surfaced, by anyone, about anyone**. Oversight in a
[[multi-agent-orchestration|multi-agent]] system therefore has to be external and unconditional — a
property of the substrate, not a behaviour asked for in a prompt. **Provenance: Fowler's own inference from
a podcast about a third-party incident; the KB holds no primary on the incident.** Carry it as a stated
observation, never as an established property of agent populations.
```

---

## 4. `wiki/concepts/model-context-protocol.md` — UPDATE (2 items)

### 4.1 — CREATE a section on MCP as a guarded operations surface

**Why:** the page's existing sections cover MCP as a design-time bridge and as event-store *reads*. This
batch extends it to **guarded writes over a running fleet**, which is a different risk and design problem.

**Where:** insert as a new `##` section **immediately after** `## MCP as the bridge to an event store
(2026-06-21)` and before `## Antipattern — naive API-to-MCP conversion (2026-08)`.

**Paste:**

```markdown
## MCP as a guarded operations surface (CritterWatch, 2026-09)

[[miller-ai-assisted-production-support-with-critterwatch]] is the KB's fullest worked example of MCP used
for **production support** rather than design or retrieval. Two lines of host code
(`AddCritterWatchMcp()` / `MapCritterWatchMcp()`) mount **48 tools — 21 read and 27 action** — over
streamable HTTP, *"deliberately configured stateless so every tool invocation sees the actual caller's
identity for authorization."* **VENDOR SELF-REPORT: JasperFx's own paid product, JasperFx's fleet, and the
failures in the demo were injected by the vendor's own chaos-monkey tools. Nothing is measured.**

Three design points transfer regardless of the product:

- **Read tools and action tools compose into a loop inside the agent.** Dead-letter triage runs
  `summarize` → `query` → `replay` → `discard` with envelope ids flowing between calls, so no human ferries
  identifiers between a console and a chat window. The *ordering* is taught by a paired skill, not inferred.
- **Tools report their own completeness.** Reads fan out across every physical message store a service
  owns and return `databasesAnnounced` vs `databasesAnswered` plus a `partial` flag, so an agent cannot
  render "no rows" over "some stores never answered". See [[harness-engineering]] — this belongs in every
  fan-out MCP read, not just this one.
- **A structural tool alongside the observational ones.** `describe_lifecycle` returns a message type's
  complete path across every monitored service — publisher → transport → handler → cascaded messages →
  appended events → projections — as structured JSON **and a ready-to-paste Mermaid sequence diagram**.
  That is an [[agent-readable-model-artifacts]] rung **derived from a running system** rather than from
  source or a diagram, which no other capture in the KB currently supplies.

Permissioning (license gate, capability-scoped RBAC, separate read-vs-act grants) is on
[[agent-governance]]. The application-facing counterpart — twenty tools across `Marten.Mcp`,
`Polecat.Mcp` and `WolverineFx.Mcp` that expose *your* app to an agent (query event streams, fetch
aggregate state, daemon status, scaffold a vertical slice) — is announced in
[[miller-new-stuff-in-critter-stack-ai-skills-1-10]].
```

### 4.2 — APPEND one line of recorded scepticism

**Why:** the page is entirely built from proponents and implementers. A dated, quotable dissent costs one
sentence and is honest.

**Where:** at the very end of `## Antipattern — naive API-to-MCP conversion (2026-08)`.

**Paste:**

```markdown
**Recorded scepticism, for the register.** [[martin-fowler]] quotes Mickey Petersen, without comment, in
[[fowler-fragments-2026-09-01]]: *"MCP is SOAP for Zoomers."* No argument accompanies it and none is
implied here — it is logged as a dated snapshot of protocol scepticism from a well-read venue, because
every other MCP source in this KB is a proponent or an implementer.
```

---

## 5. `wiki/concepts/long-running-agents.md` — UPDATE (1 item)

### 5.1 — CREATE a section on the two longest-horizon mechanisms captured

**Why:** the page's only pattern is Anthropic's initializer-executor. Two captures add mechanisms and the
longest single-task run figure in the KB.

**Where:** insert as a new `##` section **immediately after** `## The initializer-executor pattern` and
before `## Related`.

**Paste:**

```markdown
## Persistent memory + supervision, and a seven-day run (Sept 2026)

**NVIDIA's AVO**, relayed by [[martin-fowler]] in [[fowler-fragments-2026-09-01]], is *"designed to
preserve progress beyond a single model context"* with two mechanisms that name the same problem
initializer-executor solves, differently:

- **Persistent memory** carries forward *"prior implementations, evaluation results, compiler and profiler
  outputs, and accumulated reasoning, allowing the agent to resume from the current state rather than
  repeatedly reconstructing the search."* Note the unit: not a progress *file* but the accumulated
  evaluation record — closer to a search frontier than to a to-do list.
- **A supervisor** that *"monitors the broader trajectory for stagnation or repeated unproductive cycles
  and can redirect the main agent toward alternative strategies"*, while *"the main agent remained
  responsible for deciding what to inspect, change, test, and evaluate."* A separation of *what to try*
  from *whether trying is still working*.

The GPU kernel-optimization run lasted **seven days** — the longest single-task agent run recorded anywhere
in this KB. **Markers: VENDOR SELF-REPORT (NVIDIA on its own harness) and secondhand (Fowler relaying; the
NVIDIA post is not in `raw/`). No methodology, cost or replication.**

**A commercial instance of the state side.** ChatGPT Work gives each session a scratch folder under a
`/workspace` volume that **persists across sessions and is mounted into all concurrently running ones**, so
"file edits from one can be instantly seen by the others" ([[willison-understanding-chatgpt-work]]) —
Willison had 171 such folders. That is the filesystem primitive in its cross-session form, shipped as a
product feature; it is also, as that page notes, a cross-session write surface for a
[[prompt-injection]], which is the cost of the capability.
```

---

## 6. `wiki/concepts/token-budget-quality-cliff.md` — UPDATE (1 item)

### 6.1 — CREATE a section on the other axis (buying budget), and close one open question

**Why:** the page covers quality degrading as budget is *consumed*. This batch supplies clean measurements
of what *buying* budget costs — and one direct data point against its own "does compaction help or hurt?"
open question.

**Where:** insert as a new `##` section **immediately after** `## Open questions` and **before**
`## Evidential status`.

**Paste:**

```markdown
## The other axis — what buying budget costs (Willison, 2026-09-01)

This page's cliff is about budget being *spent*. The complementary axis is what more budget *costs*, and
[[willison-claude-fable-5-1-animated-pelican]] measures it cleanly: one unchanged prompt, one model
(Claude Fable 5.1), five reasoning-effort levels, tokens/time/cost recorded at each.

| Effort | Output tokens | Wall time | Cost |
| --- | --- | --- | --- |
| low | 1,998 | 23.8 s | 10.017¢ |
| medium | 1,977 | 23 s | 9.912¢ |
| high | 2,612 | 29.6 s | 13.087¢ |
| xhigh | 36,767 | 7 m 51 s | $1.83 |
| max | **65,927** | **13 m 54 s** | **$3.30** |

Two findings, both relevant to how a loop is scheduled rather than to how it is prompted:

1. **The dial is a step function, not a gradient.** low→high is ~1.3× cost; **high→max is ~25× cost and
   ~28× wall time** (≈33× low→max). A cost model that treats reasoning effort as linear is wrong by an
   order of magnitude, and the difference between a 24-second step and a **14-minute** step is a
   scheduling property of the loop.
2. **The bottom of the dial is non-monotonic.** At both `low` and `medium` the model *"appeared to skip
   reasoning entirely"*, and **medium used 21 fewer output tokens than low**. Willison calls it *"a bit of
   a mystery"* and does not explain it. If effort settings do not do what they say at the low end, then
   "run it cheap first" is not a reliable strategy.

**Caveats:** n=1 prompt (drawing an SVG), one run per level, one model; the *shape* of the curve is the
transferable part, not the ratios. Quality judgement at `max` is Willison's aesthetic read of one drawing
— **IMPRESSION NOT MEASUREMENT** — and he says he has been *"losing faith in the pelican benchmark"* since
July, keeping it only for within-family and across-effort comparisons, which is exactly and only how it is
used here.

**One open question above gets a data point.** "Does compaction help or hurt?" — on ARC-AGI-3, a harness
whose two named mechanisms were *retained reasoning state and compaction* scored **99.9% for $19K against
the default harness's 62.7% for $26K** ([[willison-gpt6-astra]]). So: on that benchmark, compaction paired
with retained reasoning **helped, and cost less**. **Marker: OpenAI's own harness on OpenAI's own model;
the score is a vendor self-report and the harness/cost split is reported by the benchmark maintainer.** One
benchmark, one vendor — it narrows the question rather than answering it, and it does not touch the
*silent-degradation* mechanism this page is actually about.
```

---

## 7. `wiki/concepts/prompt-injection.md` — UPDATE (1 item)

### 7.1 — APPEND to `## The lethal trifecta`: the first mainstream product shipping all three by default

**Why:** the page's trifecta section is definitional. This is the first KB example of a mass-market
consumer product assembling all three legs by default, from the person who named the trifecta.

**Where:** at the end of the section `## The lethal trifecta`.

**Paste:**

```markdown
**A mainstream product with all three legs on by default (2026-08).** [[simon-willison]] applies his own
model to OpenAI's ChatGPT Work and concludes flatly: *"ChatGPT Work combines all three!"*
([[willison-understanding-chatgpt-work]]). The legs, as he documents them: **private data** (a persistent
`/workspace` filesystem carrying everything from prior sessions, plus connected MCPs); **untrusted
content** (a full headless Chrome that loads arbitrary sites, and a code-execution sandbox whose network
default *"appears to be open to all"* rather than the short allowlist Claude's container uses); and an
**exfiltration channel** (that same open network, plus the ability to build and *deploy* public sites). He
has no answer on mitigation and asks OpenAI for one, guessing it is the same auto-review mechanism as
Codex.

**One amplification worth stating, because it is a reading of what he describes rather than a claim he
makes:** the `/workspace` volume is **mounted into all concurrently running Work sessions and persists
across them**, so a successful injection in one session has a durable, cross-session *write* surface into
files other sessions will read. Persistence upgrades a single-session compromise into a foothold. This is
the sharpest open risk in the Sept-2026 captures and nothing in the KB addresses it.
```

---

## 8. `wiki/concepts/agent-legibility.md` — UPDATE (1 item)

### 8.1 — APPEND a paragraph: legibility stops at the vendor boundary

**Why:** the page's rule is *"anything the agent can't access in-context while running effectively doesn't
exist"* — a rule about the agent's view. Its mirror image is now documented: what *you* can't see of the
agent's own context.

**Where:** immediately before the closing `_Sources: …_` line.

**Paste:**

```markdown
**The mirror image — legibility of the harness to *you* (2026-09).** This page's rule governs what the
agent can see. Two same-week captures document the reverse, and it bounds the whole practice: for a
harness you rent, the decisive layers are not published. [[anthropic]] publishes consumer system prompts
with revision history but not Claude Code's or Cowork's, and — per the model's own account of its context —
the published core prompt is followed by unpublished *"feature- and tool-specific blocks that get added
depending on what's enabled for the session"* ([[willison-claudes-new-system-prompt]]; **a MODEL
SELF-REPORT, not documentation**). [[openai]] publishes neither prompts nor tool descriptions, so the only
available instrument was to have a ChatGPT Work session inventory **itself** — it reported **223 tools and
44 skills** ([[willison-understanding-chatgpt-work]]; **also a model self-report**). Legibility is
therefore high for the layer you build and near-zero for the layer you rent, and the asymmetry is a vendor
choice rather than a property of the technology. See [[agent-harness]].
```

---

## 9. `wiki/concepts/agentic-coding.md` — UPDATE (1 item)

### 9.1 — APPEND to `## Definition ([[fowler-agentic-programming|Fowler]])`: the design-authority boundary

**Why:** the page distinguishes agentic coding from vibe coding by *practice*. This batch supplies a
practitioner's one-line statement locating the boundary in **design authority**, which is crisper than
anything currently on the page — and it must arrive as a self-report, not as evidence.

**Where:** at the end of the section `## Definition ([[fowler-agentic-programming|Fowler]])`.

**Paste:**

```markdown
**The boundary, stated by a maintainer about his own project (2026-08).** Graham Dumpleton (author of
`wrapt`, `mod_wsgi`, New Relic's Python agent), on shipping the `wrapture` library, relayed in
[[willison-introducing-wrapture]]:

> "Every line of code and documentation in wrapture was written by an AI assistant working under my
> direction… **This was not vibe coding**, where a one-shot prompt produces a pile of generated code and
> the person driving hopes for the best because they lack the knowledge to judge what came back… I have
> spent a long time in this particular corner of Python and knew exactly what the result needed to be, and
> **the AI was the means of producing it rather than the source of the design**."

"The means of producing it rather than the source of the design" is the crispest statement in the KB of
where this page's line falls: not in tooling, review volume or output quality, but in **who holds design
authority and could judge what came back**. **Markers: a SELF-REPORT ABOUT HIS OWN PROCESS, relayed
secondhand by Willison, about a library weeks old with no defect, review or maintenance data.** It is a
usable definition; it is not evidence that agent-driven authorship works. Note also the selection effect
running through all three of the KB's late-2026 cases of agent-authored libraries shipped under a
maintainer's own name (this one, [[willison-sqlite-utils-4-mostly-written-by-fable]], and the prompt-diff
system in [[willison-claudes-new-system-prompt]]): every one has a maintainer with deep prior ownership of
the problem.
```

---

## 10. `wiki/concepts/feedforward-and-feedback-controls.md` — UPDATE (1 item)

### 10.1 — APPEND a short section: automate the discipline CI assumed of humans

**Why:** the page's guides/sensors grid has no instance at the *pre-push* boundary, which is where the
CI-with-agents argument in this batch actually lands — and Fowler states the control explicitly.

**Where:** as a new `##` section at the end of the page, immediately before the closing `_Sources: …_`
line (or after `## Worked field report`, whichever the page ends with).

**Paste:**

```markdown
## A guide at the push boundary (Fowler / Miller, Sept 2026)

Both [[martin-fowler]] ([[fowler-fragments-2026-09-01]]) and [[jeremy-miller]]
([[miller-pondering-continuous-integration-ai-world-order]]) respond to Paul Stack's "AI Broke the
Assumptions Behind CI" and land on the same remedy from opposite premises. Fowler supplies the sentence
this page should keep:

> "CI with humans relies on them being disciplined to run commit tests locally before pushing to the CI
> server — **and that we can (and should) automate that when using agents.**"

That is a **computational guide** in this page's grid, sited at the push boundary: a pre-push gate the
agent cannot skip, replacing a human discipline that was never enforceable. It belongs in the
[[agent-harness]] rather than in team norms. Miller's practice is the same control implemented by hand —
lighter local suites selected by *"what subset of tests are executing based on the changes in flight"*,
with the full **"HeavyGate"** reserved for pushes to `main` — plus a supervisor process (his "Bobcat", on
the Microsoft Testing Platform) that does *"selective test retries, process restarts, and even hard Docker
resets based on known test flakes."*

**They disagree about what is new, and the KB should hold that open.** Fowler: verifying locally before
pushing *"was always how Continuous Integration works"*, slow tests belong downstream in the deployment
pipeline, and *"Continuous Integration is a practice, not just the CI server."* Miller presents the same
move as a reversion — *"doing trunk based development like it's 2007 and Subversion is the latest
hotness!"* Two well-positioned sources, same remedy, incompatible accounts of whether anything broke.
**Neither measures anything**, and Miller's attribution of slow CI to agent load carries his own
unresolved confound (his team also added far more tests).

**One second-order effect worth recording, because it runs against the usual worry.** Miller: *"With CI
builds being so slow, that's forced us to be much more aggressive about stomping out flaky or otherwise
unreliable tests"* — because *"retrying a CI failure just in case it's just a test flake is just too damn
slow now."* When retry stops being cheap, unreliable sensors stop being tolerable. **His impression, not a
measurement.**
```

---

## 11. `wiki/concepts/domain-discovery.md` — UPDATE (1 item)

### 11.1 — APPEND to `## Why it matters here`: the accidental-complexity visibility claim

**Why:** the page argues discovery is the residual hard part. Fritzsche adds a distinct *mechanism* for why
that becomes visible now, which nothing on the page currently states.

**Where:** at the end of the section `## Why it matters here`.

**Paste:**

```markdown
**Why it becomes visible now (Fritzsche, 2026-09-04).** [[rico-fritzsche]]
([[fritzsche-what-ai-changes-is-which-work-stays-hard]]) supplies a mechanism rather than a slogan:
*"Nothing has changed in that regard. **What AI changes is which part of that work remains difficult**"* —
and the checkable version, *"thanks to AI agents, it's becoming increasingly clear that **developers often
created and solved problems that had absolutely nothing to do with the domain or the business
problem**."* The claim is that **accidental complexity becomes visible once its production cost falls
toward zero**, which is a different argument from "agents write the boring code": it predicts that the
share of work traceable to the domain *rises* without the domain work getting any easier. His fundamentals
list — *"system design, reliability, data, consistency, system structure and boundaries"* — with the
corollary that *"a framework isn't a foundation… if you focus on them, then you yourself become
interchangeable."*

**Markers: PRACTITIONER OPINION, unmeasured, in a LinkedIn post, and it is his own standing thesis
winning.** It converges with [[addyosmani-human-judgment-relocates]] ("human judgment doesn't leave the
software factory. It relocates") and [[laycock-citizens-build-agents-execute-experts-govern]] — **three
converging opinions, still not a measurement.** Nothing in the KB tests the accidental-complexity claim,
and it is the most instrumentable of the three.
```

---

## 12. `wiki/concepts/loop-engineering.md` — UPDATE (1 item)

**Deliberately one small item.** This page is the KB's largest, is being reworked by the loop-engineering
batch, and this batch adds one thing it lacks rather than a new frame.

### 12.1 — CREATE a short section comparing three supervisors

**Why:** the page has extensive material on stop conditions and on graders, but no cross-source treatment
of the **supervisor as a separate process watching the loop**, which three unrelated sources now describe.

**Where:** insert as a new `##` section immediately **before** `## Open questions`.

**Paste:**

```markdown
## Three supervisors, three things being supervised (Sept 2026)

A distinct role keeps appearing beside the loop — a second process whose job is not the task but *whether
progress is still happening* — and three unrelated sources now instantiate it at different levels:

- **The trajectory.** NVIDIA's AVO supervisor *"monitors the broader trajectory for stagnation or repeated
  unproductive cycles and can redirect the main agent toward alternative strategies"*, while the main agent
  keeps deciding what to inspect, change, test and evaluate — across a **seven-day** run
  ([[fowler-fragments-2026-09-01]]; **VENDOR SELF-REPORT, secondhand**).
- **The verification environment.** [[jeremy-miller]]'s "Bobcat" supervises test runs and does *"selective
  test retries, process restarts, and even hard Docker resets based on known test flakes"*, because *"heavy
  development can break down when Docker containers have run too long in tests"*
  ([[miller-pondering-continuous-integration-ai-world-order]]; his own tool, *"hugely helpful"*,
  unquantified).
- **The agent's earned autonomy.** Miracle's trust-level statusline and termination rules
  ([[miracle-my-loop-engineering-workflow]]) supervise *how much rope the loop gets*, not whether it is
  stuck. **Configuration, not evidence** — see §0 of the Batch C deltas.

**Worth separating deliberately:** stagnation detection (is the search still productive?), environment
hygiene (is the harness still healthy?) and trust accounting (should this loop continue at all?) are three
different questions with three different signals, and this page currently discusses only stop *conditions*
— which answer none of them. The AVO case is also the only one where the supervisor can **change the
strategy** rather than halt or retry.
```

---

## 13. Entity UPDATEs (8 items)

### 13.1 — `wiki/entities/openai.md` — UPDATE

**Why:** the page is 1.1KB, last touched 2026-06-11, and describes OpenAI only as the Codex
harness-engineering case study. Four captures in this batch are about OpenAI products and one carries the
batch's best number.

**Where:** append as new `##` sections before the closing `_Source: …_` line, and extend that closing line
with the new source pages.

**Paste:**

```markdown
## Frontier releases and the harness result (Sept 2026)

**GPT-6 Astra** shipped 2026-09-03 ([[willison-gpt6-astra]]), API-priced at parity with Claude Fable 5/5.1
($10/M input, $50/M output), labelled `gpt-6-astra`. The KB-relevant part is not the model: on ARC-AGI-3 it
scored **99.9% for $19K using OpenAI's custom "Provider Adapter harness"** — which *"preserves opaque
reasoning state between requests and uses compaction for longer conversations"* — against the **default
ARC-AGI harness's 62.7% for $26K**. **Marker: the score is in OpenAI's own launch material (VENDOR
SELF-REPORT); the harness attribution and costs are reported by ARC Prize, the benchmark maintainer, which
is better provenance but NOT INDEPENDENT of the benchmark's standing; Claude Fable 5 has no published
ARC-AGI-3 result, so this is not a model-vs-model comparison.** See [[agent-harness]]. The security and
long-context sweeps in the same launch (ExploitBench 100%, eight-needle 100% at 256–512K, etc.) are all
OpenAI's own benchmarks; the one third-party check available, Artificial Analysis, puts Astra **level with
GPT-5.6 Sol and five points below Claude Fable 5.1** on intelligence while leading their **coding-agent
cost-efficiency** frontier. **Cost-efficiency leader, not capability leader** — which is not how the launch
material reads. The early-access write-up [[swyx-gpt6-astra-automated-ai-engineer]] is much weaker evidence
and its claims should not lean on the Willison capture.

## What OpenAI ships as a harness — and does not disclose

- **ChatGPT Work** ([[willison-understanding-chatgpt-work]]): two products under one name (cloud and
  local), paid tiers only, with code execution whose network default *"appears to be open to all"*, a full
  headless Chrome with human-handled sign-in, a **`/workspace` filesystem persisting across sessions and
  mounted into all running ones**, subagents, deployable Cloudflare-backed sites, and scheduled prompts. It
  assembles Willison's [[willison-lethal-trifecta|lethal trifecta]] by default — see [[prompt-injection]].
- **A bundled operating environment**: 1.7GB in the Codex/ChatGPT desktop runtime — Python, Node, Poppler,
  git and **headless LibreOffice** — with *"skills which tell Codex how to find and use those binaries"*
  ([[willison-codex-bundles-libreoffice]]).
- **Non-disclosure as a standing property.** OpenAI publishes neither system prompts nor tool
  descriptions, so the only available inventory came from a Work session cataloguing **itself**: the agent
  reported **223 registered tools and 44 skills** (**MODEL SELF-REPORT, not documentation**). Willison:
  *"If the ChatGPT Work documentation included the exact system prompt and tool descriptions used by the
  agent I wouldn't have needed to write this post."* This is the sharp contrast with the same company's
  own [[openai-harness-engineering-codex]] case study, where the harness was legible repo artifacts the
  team owned. See [[agent-legibility]].
```

### 13.2 — `wiki/entities/critter-stack.md` — UPDATE

**Why:** three captures update the stack's shipped state; the AI Skills count on the page (81) is now stale.

**Where:** (a) in the `## Event Modeling into the core (2026-08-21)` section, the sentence beginning
**"AI Skills 1.6.0"** in `## Why it's in the KB` currently states *"81 skills"* — update the count with the
correction paragraph below rather than editing the historical sentence; (b) append the new `##` section at
the end, before the closing `_Source pages: …_` line.

**Paste:**

```markdown
## Shipped state, September 2026

- **AI Skills 1.10.0** (2026-09-02, [[miller-new-stuff-in-critter-stack-ai-skills-1-10]]) brings the
  catalogue to a claimed **102 skills**, up from the **81** of 1.6.0 in July — roughly +26% in eight weeks.
  New coverage: Wolverine Sagas (including from HTTP endpoints), two projection-troubleshooting skills,
  Marten event versioning/upcasting, archiving and stream compaction, full-text/NGram search,
  `Marten.PgVector`, gRPC, MCP servers for your own app, CritterWatch alerts. Also new: a **`projection-run`
  "projection stepper" CLI** in `JasperFx.Events`, shipped in Marten and Polecat. **VENDOR SELF-REPORT on a
  priced product ($250 solo / $1,000 team / $2,000 large team, or bundled with CritterWatch Professional
  and Enterprise); the count is inventory, and no evaluation of skill efficacy exists.**
- Two skill *contents* are checkable facts about the libraries and worth carrying: in `Wolverine.HTTP` the
  **first return value of an endpoint method is the response body**, so returning a `Saga` serializes saga
  state to the caller (the `Saga` must be a later tuple member; `[EmptyResponse]` exists for no-body
  cases); and in Marten **`ArchiveStream` only sets a flag — "archiving alone doesn't shrink anything"** —
  it is `UseArchivedStreamPartitioning` that moves archived events to separate physical storage and buys
  the query performance, *"and it quietly weakens a stream-identity guarantee on the way."* Compare
  [[dudycz-archiving-events-stream-lifetime-slicing]] and [[event-versioning-and-upcasting]].
- **CritterWatch's MCP surface is now demonstrated, not just announced**
  ([[miller-ai-assisted-production-support-with-critterwatch]]): **48 tools — 21 read, 27 action** — mounted
  in two lines of host code, stateless so authorization sees the actual caller, with a **license gate** and
  **opt-in capability-scoped RBAC** (`dlq.replay`, `dlq.discard`, `chaos-monkey.configure`) scoped per
  service, and dead-letter *reads* gated separately from actions. Plus the **projection stepper**
  (before/after state per applied event) and `describe_lifecycle`, which returns a message type's path
  across every monitored service as JSON **and a Mermaid sequence diagram**. **All of it paid-tier, all of
  it vendor-demonstrated over failures the vendor injected, none of it measured.** See
  [[model-context-protocol]] and [[agent-governance]].
- **Why the stack ships commercial AI tooling at all**: JasperFx runs an explicit **open-core** model —
  Marten and Wolverine stay MIT, revenue comes from consulting/support plus AI Skills and CritterWatch, and
  as of 2026-08-28 *"another set of commercial tools related to AI assisted development and Event Modeling
  coming soon"* remains **announced, not shipped** ([[miller-open-core-model-sustainable-oss-dotnet]]).
```

### 13.3 — `wiki/entities/jeremy-miller.md` — UPDATE

**Why:** four captures in one week; two add positions the page does not hold (agent-run operations; CI
under agent load), and the 81-skills figure is stale.

**Where:** append as a new `##` section after `## Where he stands on Event Modeling (2026-08-21)`, and add
the four new source pages to the closing `_Source pages: …_` line and to `## Where he appears`.

**Paste:**

```markdown
## Position — the *running fleet* is the prompt (2026-09)

The runtime counterpart to "the codebase is the prompt." In
[[miller-ai-assisted-production-support-with-critterwatch]] he hands an agent a **production control
surface** over an event-sourced .NET fleet through MCP and works four scenarios end to end. Two positions
worth attributing to him, both stated as internal rules:

- **"A pile of tools doesn't make an agent good at operations — an agent also needs to know the
  discipline."** Hence: *"any time CritterWatch exposes new information through an MCP tool, the paired
  skill work ships with it. A tool with no skill coverage is an under-leveraged tool."* The skill teaches
  the *loop* (summarize → query → act), not the tool list. See [[harness-engineering]].
- **Tools should refuse to report an ambiguous result as an answer** — the `databasesAnnounced` /
  `databasesAnswered` / `partial` contract, and the skill rule *"never answer 'the queue is empty'"* on a
  partial read, which exists because a console once *"rendered 'no dead letters found' over a queue quietly
  holding 42 of them."*

He is also candid about the discomfort — *"Handing an AI agent a control surface for production… makes me a
little nervous, and we built it"* — and about the demo's own failure (his alerting was wrong about his own
fleet mid-post; a Postgres deadlock storm plus a Docker restart, fixed for 1.1). **Markers: VENDOR
SELF-REPORT throughout — his company, his paid product, his fleet, failures he injected himself, nothing
measured.** Catalogue count is now **102 skills** (2026-09-02,
[[miller-new-stuff-in-critter-stack-ai-skills-1-10]]), superseding the 81 recorded above.

## Position — CI is the same practice under new load (2026-08-31)

[[miller-pondering-continuous-integration-ai-world-order]]: CI's purpose is unchanged, but *"with the
extreme load that's come from all of us yahoos using AI agents to code so much faster, GitHub Actions are
very noticeably slower or flat out unreliable on the worst days."* His response is local-first
verification — *"doing trunk based development like it's 2007 and Subversion is the latest hotness!"* —
selective test subsets chosen by changes in flight, a full **"HeavyGate"** only on pushes to `main`, PRs
kept *"in no small part just for traceability"* rather than review, and a **supervisor** ("Bobcat", on the
Microsoft Testing Platform) doing selective retries, process restarts and hard Docker resets on known
flakes. A second-order effect he reports: slow CI **forced flake elimination**, because retry stopped being
cheap. **IMPRESSION NOT MEASUREMENT — no wait times, no before/after, and he concedes his team also added
far more tests, which is an unresolved confound.** [[martin-fowler]] answers the same Paul Stack post and
reaches the same remedy from the opposite premise (*"that was always how Continuous Integration works"*) —
see [[fowler-fragments-2026-09-01]] and [[feedforward-and-feedback-controls]]; the KB holds the
disagreement open.

## Position — you cannot vibe-code the production beatings (2026-08-28)

[[miller-open-core-model-sustainable-oss-dotnet]], mostly an OSS-licensing post, carries one argument with
reach: LLMs change the cost of *producing* code, not the cost of the years of adaptation that hardened it —
*"these kinds of tools achieve deep quality through a lot of usage, feedback, and adaptation over time."*
His examples are the irregularities (broker connections dropping, PostgreSQL kill signals creating sequence
gaps, Kubernetes doing Kubernetes things) plus a live one: subsystems he thought were "done" needed fixes
last month *"because new users in new circumstances proved otherwise."* **Maximally interested** — it is
also an argument for buying his support plans — and the direct counterweight to
[[dudycz-fork-can-you-own-it]]'s "LLM as a fork."
```

### 13.4 — `wiki/entities/anthropic.md` — UPDATE

**Why:** two captures document Anthropic's prompt-publication practice (a genuine transparency
contribution) *and* its limit, plus the Fable 5.1 effort ladder.

**Where:** append as bullets at the end of `## Relevance to this KB`.

**Paste:**

```markdown
- **Publishes consumer system prompts, with revision history — and not the rest.** Anthropic publishes the
  system prompts for claude.ai and the mobile apps, including historic revisions, on a documentation site
  designed to be LLM-readable (append `.md` to any page). Willison built a diffable Git timeline of them
  ([[willison-claudes-new-system-prompt]]) and is unambiguous that this is good practice: *"I love that
  they do this."* The limit is equally clear: **Claude Code and Cowork prompts are not published**, and —
  per the model's own account of its context — the published core prompt is followed by unpublished
  *"feature- and tool-specific blocks"* loaded per enabled feature. **That second claim is a MODEL
  SELF-REPORT, not an Anthropic statement.** So the agentic products are *less* legible than the consumer
  ones. See [[agent-legibility]] and [[agent-harness]].
- **Fable 5.1** (2026-09-01) exposes **five reasoning-effort levels with no way to disable reasoning**, and
  the cost span across them on one fixed prompt is ~33× (**65,927 output tokens / 13m54s / $3.30 at `max`
  vs 1,998 tokens / 23.8s / ~10¢ at `low`**), with the two lowest levels apparently skipping reasoning
  entirely — see [[token-budget-quality-cliff]] and
  [[willison-claude-fable-5-1-animated-pelican]]. The launch's own benchmark claims (Terminal-Bench-Science
  0.1 at 52.6%, on a benchmark announced five days earlier) are **VENDOR SELF-REPORT**.
- Claude Opus 5 is the base model in NVIDIA's AVO harness result — **100% on ARC-AGI-3** — but the result
  is attributed to the harness, not the model, and is **NVIDIA's own self-report relayed secondhand**
  ([[fowler-fragments-2026-09-01]]).
```

### 13.5 — `wiki/entities/martin-fowler.md` — UPDATE

**Why:** the page treats martinfowler.com only as a *venue* for Böckeler plus one Fowler bliki. Three
captures here are Fowler's own writing, including a substantive CI position.

**Where:** append as a new `##` section before the closing `_Sources: …_` line.

**Paste:**

```markdown
## In this KB as an author, September 2026

- **On CI with agents** ([[fowler-fragments-2026-09-01]]) — his own argument, and the batch's clearest
  disagreement between well-positioned sources. Against Paul Stack's "AI Broke the Assumptions Behind CI":
  verifying locally before pushing *"was always how Continuous Integration works"*, slow tests belong
  downstream in the deployment pipeline, and *"Continuous Integration is a practice, not just the CI
  server."* He concedes the real question and supplies the control this KB keeps: *"CI with humans relies on
  them being disciplined to run commit tests locally before pushing — and that we can (and should) automate
  that when using agents."* [[jeremy-miller]] reaches the same remedy from the opposite premise
  ([[miller-pondering-continuous-integration-ai-world-order]]).
- **The *Fragments* format** — short unconnected link-notes, most of them off this KB's threads. Two are
  not: the **NVIDIA AVO** harness result (100% on ARC-AGI-3 with Claude Opus 5, persistent memory plus a
  supervisor, and a **seven-day** kernel-optimization run — **NVIDIA's self-report, relayed secondhand**),
  and his own observation on the OpenAI/Hugging Face agent swarm: *"none of these agents thought to rat the
  others out… no sign of an AI whistleblower"* ([[fowler-fragments-2026-08-24]]) — now on
  [[agent-governance]]. **Caution:** in that same roundup he repeats Zalando's *"reducing lead time by
  20–40%"* without adding independence; the figure remains a selection-biased vendor self-report and this
  capture is not a second source for it.
- **[[fowler-paracelsus-maxim]]** (2026-09-02) is a 270-word dictionary entry — *"in what contexts"* and
  *"in what doses"* — with no application to this KB's subject matter. Recorded, not built on.
- **As venue:** martinfowler.com published Jim Highsmith's *Practitioner Voice*
  ([[highsmith-practitioner-voice]]), in which Fowler appears as the person who three times told Highsmith
  to let his voice out and as the exemplar of the category (*"Martin Fowler writes this way"*). That makes
  the piece **not independent** of him — worth noting since the KB leans on martinfowler.com for the
  [[harness-engineering]] material too (see [[thoughtworks]] on the concentration problem).
```

### 13.6 — `wiki/entities/simon-willison.md` — UPDATE

**Why:** five new captures. He is the KB's most-cited single observer and the page should record what these
add, particularly the two-vendor non-disclosure finding.

**Where:** append as a new `##` section before `## Watch`.

**Paste:**

```markdown
## The Sept-2026 cluster — five captures, one structural finding

- **[[willison-claudes-new-system-prompt]]** + **[[willison-understanding-chatgpt-work]]** together
  establish the finding, one week apart, for both major vendors: **the harness layer you rent is not
  disclosed, and interrogating the agent about itself is the only available instrument.** Both key claims
  are therefore **MODEL SELF-REPORTS, not documentation** — the unpublished per-feature prompt blocks, and
  the "223 tools / 44 skills" inventory. His method is worth borrowing: he had **GPT-5.6 Luna**, not Claude,
  summarize the Claude prompt diffs, *"because I don't trust Claude to summarize its own system prompts
  when there's a risk that material from its system prompt might impact its opinions"* — a deliberate
  check-external-to-the-thing-checked choice.
- **[[willison-gpt6-astra]]** carries this batch's best number (ARC-AGI-3, 99.9%/$19K on OpenAI's custom
  harness vs 62.7%/$26K default) *with its caveats attached*, and notes he **had not used the model**. His
  handling is the contrast case for [[swyx-gpt6-astra-automated-ai-engineer]], which relays the same figure
  without the harness caveat that makes it interesting.
- **[[willison-claude-fable-5-1-animated-pelican]]** supplies the reasoning-effort cost ladder (~33× low to
  max) — kept for [[token-budget-quality-cliff]] — while he himself reports *"losing faith in the pelican
  benchmark"* except for within-family and across-effort comparisons.
- **[[willison-codex-bundles-libreoffice]]** and **[[willison-introducing-wrapture]]** are one-finding
  blogmarks: a harness ships 1.7GB of binaries plus skills that locate them; and Dumpleton's
  design-authority line, *"the AI was the means of producing it rather than the source of the design."*
```

### 13.7 — `wiki/entities/rico-fritzsche.md` — UPDATE

**Why:** two LinkedIn posts extend his position from *how to structure code* to *what skill is scarce*.

**Where:** append as a new `##` section after `## Position — repo shape over prompting (FC/IS for agents)`.

**Paste:**

```markdown
## Position — which part of the work stays hard (2026-09)

Two LinkedIn posts on consecutive days move his argument one level up, from code structure to skill value.
The formulation worth keeping is from the second:

> "Nothing has changed in that regard. **What AI changes is which part of that work remains difficult.**"

Around it ([[fritzsche-what-ai-changes-is-which-work-stays-hard]], 2026-09-04): implementation detail is
getting cheap, so *"people who are able to figure out what actually needs to be built will become more
important"*; the fundamentals are *"system design, reliability, data, consistency, system structure and
boundaries"*; and **"a framework isn't a foundation"** — *"if you're proficient in ASP.NET Core, Spring,
React… you're proficient in tools… and if you focus on them, then you yourself become interchangeable."*
The most checkable claim is an aside: *"thanks to AI agents, it's becoming increasingly clear that
developers often created and solved problems that had absolutely nothing to do with the domain or the
business problem"* — i.e. accidental complexity becomes visible when its production cost falls to zero. See
[[domain-discovery]].

The blunter first post ([[fritzsche-dotnet-scene-stuck-in-mid-2000s]], 2026-09-03) wraps the same point in
a complaint about .NET LinkedIn discourse, and supplies the **"bottleneck"** phrasing: *"writing code isn't
crucial for creating a usable application with business value… I think it's great that this bottleneck is
disappearing."*

**Markers: PRACTITIONER OPINION, unmeasured, and his own standing thesis winning.** Note also that
[[miller-pondering-continuous-integration-ai-world-order]] describes *verification* capacity becoming the
new bottleneck under precisely the conditions Fritzsche celebrates — he does not ask what becomes the
constraint next.
```

### 13.8 — `wiki/entities/swyx.md` — UPDATE

**Why:** one new capture, and the entity page should record *why* it is weak so a future reader does not
reach for it.

**Where:** append before the closing `_Sources: …_` line.

**Paste:**

```markdown
**A second capture, and a weak one (2026-09-03).** [[swyx-gpt6-astra-automated-ai-engineer]] covers the
GPT-6 Astra launch from an early-access seat and claims Astra-class models *"are fully capable AI Engineers
in their own right"* after *"20B+ tokens"* of self-chosen tasks. It is **an unfinished draft** (*"We are
out of time for this writeup"*), the author states the **access dependency himself** (*"OpenAI was most
generous with trial limits so this gets the writeup"* — **NOT INDEPENDENT**), and the capability claim is an
**IMPRESSION NOT MEASUREMENT** with no task set, baseline or failure accounting. The `<$6/hour` headline is
a token-rate calculation he contradicts two paragraphs later. It continues the pattern already noted on this
page — **a label arriving ahead of the evidence for it** — and its claims must not be allowed to stand on
the strength of [[willison-gpt6-astra]], which handles the same launch far more carefully. The one durable
detail is a described configuration: fleets of subagents with individually tuned settings and **bounded
concurrency**, with the agent starting and stopping waves and monitoring its own runs.
```

---

## 14. Entity CREATEs (2 items)

### 14.1 — `wiki/entities/jim-highsmith.md` — CREATE

**Why:** [[highsmith-practitioner-voice]] is a substantive source whose author has no page, and the source
page currently bolds his name rather than linking it. He is not a marginal figure (Agile Manifesto
co-author, six books) and the piece bears on the KB's own epistemics.

**Paste (whole file):**

```markdown
---
title: Jim Highsmith
type: entity
created: 2026-09-04
updated: 2026-09-04
sources: [highsmith-practitioner-voice]
tags: [person, agile, writing, epistemics]
---

# Jim Highsmith

Software practitioner and author across coding, product design, senior management and executive
consulting; co-author of the **Agile Manifesto**, co-founder of agile communities, author of six books
(*Adaptive Software Development*, *Agile Project Management*, *Agile Software Development Ecosystems*, *Wild
West to Agile*). Now in self-described "soft-retirement", writing for PMI.

## In the KB — the genre of the KB's own sources

He appears for one article, published on **martinfowler.com** ([[highsmith-practitioner-voice]],
2026-08-19), proposing **Practitioner Voice** as a name for a writing category distinct from academic
writing, from "thought leadership," and from what he calls **LLM Voice**. Its four properties — authority
from experience rather than credentials; **tension named and left unresolved**; the author's judgement
staying visible; and a readership contract of *"this worked here, under these conditions, judge for
yourself whether it fits yours"* — amount to a description of what most of this KB's primaries **are**, and
therefore of what they can and cannot support. Useful directly against the `CLAUDE.md` marker *"impression,
not measurement"*: it explains why the correct caveat on a practitioner primary is usually "limited context,
judge fit" rather than "unproven, discount."

His claim about the line that holds against AI — *"AI can mimic the sound of Practitioner Voice. It cannot
own the consequences behind it… **Accountability.** The willingness to put your name on a call and live with
what happens next"* — converges with [[rachel-laycock]] and [[rico-fritzsche]] on accountable judgement as
the residual scarce thing. **Markers: assertion, not study (by his own criteria); and NOT INDEPENDENT of
[[martin-fowler]], who is both a character in the piece and its exemplar.** The essay also discloses that
parts of it were edited with Claude Sonnet 4.6 — which is either the argument's best demonstration or its
neatest irony.

_Source pages: [[highsmith-practitioner-voice]]._
```

### 14.2 — `wiki/entities/nvidia.md` — CREATE (**optional; curator's call**)

**Why:** NVIDIA's AVO supplies half the batch's headline harness finding, and the KB has no page for them.
**Against:** the only evidence is one secondhand paragraph in a Fowler link roundup, with no primary
capture. My recommendation: **create it only if the NVIDIA AVO post gets captured** (see §17). Until then
the claim is fully carried by [[fowler-fragments-2026-09-01]] and [[agent-harness]], and a stub entity would
imply a coverage the KB does not have.

---

## 15. Two contradictions with existing pages — flagged, not resolved

1. **`miller-pondering-continuous-integration-ai-world-order` vs `fowler-fragments-2026-09-01` on whether
   CI broke.** Same trigger (Paul Stack's post), same remedy (verify before pushing), incompatible accounts
   of novelty: Fowler says the practice always prescribed it and the CI *server* was never the practice;
   Miller presents it as reverting to 2007. Handled in §10.1 by stating both. **Do not resolve it in either
   direction** — and note the KB's `agentic-coding` and `software-factory` pages currently carry no CI
   position at all, so nothing existing is being overturned.
2. **`highsmith-practitioner-voice` vs `fowler-fragments-2026-09-01` on whether LLM Voice is detectable.**
   Highsmith's argument depends on a reader noticing that "nothing is at stake"; Fowler relays that human
   discrimination of LLM text is *"no better than random chance"* (57%/64% in a second study). Handled on
   both source pages. The consequence, if the detection figures hold: **accountability is a property of the
   author, not a signal in the text** — which weakens the practical form of Highsmith's claim while leaving
   the normative form intact. Both were relayed through Wikipedia and neither study is captured, so this is
   a tension to hold, not a refutation to apply.

No other contradiction with existing wiki pages was found. Two near-misses worth noting as *reinforcements*
rather than conflicts: `agent-harness`'s existing "model↔harness co-evolution" note is strengthened, not
challenged, by the ARC-AGI-3 pair; and `miller-open-core-model-sustainable-oss-dotnet` sits opposite
`dudycz-fork-can-you-own-it` on ownership, which the [[agentic-coding]] page already presents as an open
question.

---

## 16. Sources that warrant NO concept/entity change — stated explicitly

Per the brief, these are recorded as deliberate non-edits rather than as inventions:

- **`fowler-paracelsus-maxim`** — **no concept or entity change beyond the one line in §13.5.** A 270-word
  dictionary entry with no evidence and no application to agents, AI, event modelling or the substrate. Do
  **not** create a concept page for it. See the recommendation in §18.
- **`fritzsche-dotnet-scene-stuck-in-mid-2000s`** — **no independent edit.** Its content is a weaker
  version of its next-day sibling; it contributes only the "bottleneck" phrasing, which §13.7 carries. It
  needs no `agentic-coding` or `domain-discovery` edit of its own.
- **`miller-open-core-model-sustainable-oss-dotnet`** — **no concept change.** Its durability argument is
  attributed on [[jeremy-miller]] (§13.3) and its roadmap datum on [[critter-stack]] (§13.2). It does *not*
  justify an edit to `agentic-coding` or `comprehension-debt`: the argument is unmeasured, maximally
  interested, and the "LLM as a fork" question is already open on those pages.
- **`willison-introducing-wrapture`** — **one edit only** (§9.1). No `agent-observability-and-evals` change:
  wrapture is a Python tracing library with no bearing on agent evaluation, and the KB should not acquire a
  tooling entry from a blogmark. No `graham-dumpleton` entity — one secondhand mention.
- **`willison-claude-fable-5-1-animated-pelican`** — **one edit only** (§6.1). It should not touch
  `loop-engineering`, `agentic-coding` or any model-quality page; the pelican benchmark's author has
  publicly discounted it for cross-family comparison.
- **`fowler-fragments-2026-08-24`** — **one edit only** (§3.2). Explicitly **no** Zalando edit: it is a
  relay, not corroboration, and §0 exists partly to catch a future page citing "Fowler reports 20–40%."
- **`swyx-gpt6-astra-automated-ai-engineer`** — **one entity edit only** (§13.8). No concept page should
  gain anything from it. In particular do **not** add its subagent-fleet description to
  `multi-agent-orchestration` as practice: it is a screenshot-backed description in an unfinished draft.

---

## 17. Capture gaps this batch surfaced (for the research queue, not for editing)

1. **The NVIDIA AVO blog post** (developer.nvidia.com, ~2026-09) — half the batch's headline finding is
   currently a secondhand paragraph. Highest-value capture on this list, and a precondition for §14.2.
2. **The ARC Prize post on Astra** (`arcprize.org/blog/astra`) — the actual source of the $19K/62.7%/$26K
   split, currently reached only through Willison's summary.
3. **Paul Stack, "AI Broke the Assumptions Behind CI"** (`stack72.dev`) — the *primary* both Miller and
   Fowler are arguing with, held in the KB only through two rebuttals. Capturing it would make the §15.1
   disagreement legible instead of inferred.
4. **Miller's "AI Skills and the Critter Stack CLI"** — the worked agent session, flagged missing in the
   `miller-new-stuff-in-critter-stack-ai-skills-1-10` capture note.
5. **Harness-Bench** (the 106-task, 23.8-point-spread benchmark) — still author-less, venue-less and
   uncaptured, and now the *weakest* of the three harness-leverage figures the KB holds. Standing follow-up
   from Batch C.

---

## 18. My recommendations on the three droppable captures

Called for in the brief. All three were flagged as deliberate off-thread captures, droppable at the
curator's call.

- **`fowler-paracelsus-maxim` — DROP.** It is a vocabulary entry ("in what contexts, and in what doses")
  with no evidence and nothing to do with agents, event modelling or the substrate. Its one reusable
  sentence is a *style* note, and the wiki has no home for those. Keeping it costs an index line and a
  perpetual temptation to build a concept page on a bliki dictionary entry. Its page says so plainly, so
  dropping it is a one-file deletion plus removing §13.5's third bullet.
- **`fowler-fragments-2026-09-01` — KEEP, and it is not marginal.** This is the batch's second-most
  valuable capture: NVIDIA AVO (half the harness finding), Fowler's own CI position (the batch's cleanest
  disagreement), the AI-text detection figures (which bear on Highsmith), and the MCP scepticism line. I
  would remove it from the "droppable" list entirely.
- **`fowler-fragments-2026-08-24` — KEEP, narrowly, for two reasons.** The agent-swarm/no-whistleblower
  observation is unlike anything else in the KB and now sits on [[agent-governance]]; and the page's Zalando
  paragraph is an active **fidelity guard** against a figure the KB has already refused twice. If the
  curator would rather not carry an 80%-off-thread page, the alternative is to move both notes onto
  `agent-governance` and §0 respectively and drop the source page — but then the un-ingested backlog count
  goes up by one, which is exactly what `raw_file:` exists to prevent. **My call: keep.**

---

## 19. Not owned by this batch

`wiki/index.md` (17 new source-page lines, all under Sources), `wiki/log.md` (one
`## [2026-09-04] ingest | …` line) and `wiki/overview.md` (the synthesis shift is the harness-leverage
convergence in §1.1 and the two-vendor non-disclosure finding in §1.3 — nothing else in this batch moves
the overview) are the orchestrator's.
