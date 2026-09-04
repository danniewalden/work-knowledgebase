---
title: "Source: Fowler — Fragments, September 1 2026"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [fowler-fragments-2026-09-01]
raw_file: [raw/articles/fowler-fragments-2026-09-01.md]
tags: [agent-harness, long-running-agents, ci-cd, model-context-protocol, link-roundup, focus]
---

# Source: Fowler — Fragments, September 1 2026

A *Fragments* link-roundup post by **[[martin-fowler]]**, 2026-09-01 — his format of short unconnected
notes. Raw capture: `raw/articles/fowler-fragments-2026-09-01.md`. Captured as an off-thread sweep of the
Fowler watch, but **two of its six fragments are squarely on-thread and one of them is load-bearing.**
Everything here is Fowler relaying and commenting on other people's work: **secondhand throughout**, with
no primary captured for any of it.

## Summary

Six fragments: AI-prose detection; **NVIDIA's AVO long-horizon agent architecture**; "MCP is SOAP for
Zoomers"; **Fowler's rebuttal of Paul Stack on CI with agents**; a bio-risk debunking; and a preprint on
LLMs inventing correlated fictional expert names. The AVO note and the CI rebuttal are why this page
exists.

## Key points

**1. NVIDIA AVO — a second harness-not-model result on ARC-AGI-3.** Fowler relays NVIDIA's technical blog
on an *"Architecture for Long-Horizon Autonomous Agents"*: their research group combined **Claude Opus 5
with a harness called AVO** and reached **100% on ARC-AGI-3** — a figure that appears in the capture only
in the linked NVIDIA post's title/URL, not in Fowler's own prose, which names the benchmark without a
score — having first used the same setup for GPU kernel optimization, where *"the agent ran for seven
days."* The two mechanisms, quoted from NVIDIA:

> "AVO is designed to **preserve progress beyond a single model context**. Two mechanisms are particularly
> important: **persistent memory and supervision**. Persistent memory carries forward prior
> implementations, evaluation results, compiler and profiler outputs, and accumulated reasoning, allowing
> the agent to **resume from the current state rather than repeatedly reconstructing the search**. The
> supervisor monitors the broader trajectory for **stagnation or repeated unproductive cycles** and can
> redirect the main agent toward alternative strategies when needed."

And the division of labour during the seven-day run: *"the main agent remained responsible for deciding
what to inspect, change, test, and evaluate, while the supervisor helped maintain forward progress when
the search plateaued."* NVIDIA's own reading is that doing well on two different long-horizon task types
indicates a general-purpose tool.

**Markers: VENDOR SELF-REPORT** (NVIDIA's own blog about its own harness) **and secondhand** (Fowler
relaying; the NVIDIA post is not in `raw/`). Fowler adds no assessment.

Why it matters: read with [[willison-gpt6-astra]] — OpenAI's custom "Provider Adapter harness" scoring
**99.9% for $19K vs the default harness's 62.7% for $26K** on the *same* benchmark — this is **a second
lab, a different base model, and different harness mechanisms moving the same benchmark**. Two independent
vendor harnesses, same conclusion: **the harness, not the model, is where the remaining headroom on
ARC-AGI-3 sat.** Neither is independent evidence; together they are a convergence worth naming.

**2. Fowler on CI with agents — the counterpoint to [[miller-pondering-continuous-integration-ai-world-order]].**
Responding to the same Paul Stack post Miller responded to, Fowler quotes Stack's diagnosis (*"the agent is
still discovering that its change doesn't work only after it crosses the PR boundary. The feedback loop is
in the wrong place regardless of how fast CI runs"*) and rejects the premise that this is new:

> "This is where I get to be the grumpy old guy, and point out that was **always how Continuous
> Integration works**. When I'm done with a change, first I pull… I build and test locally, and if all is
> well I push and let the CI server do its thing. The only reason the CI server should fail is if there's
> some funky mismatch between my machine and the CI server. **Tests that take a while to run aren't part
> of this loop, instead they are run further down the deployment pipeline, downstream of CI.** Any failures
> there imply missing tests in CI."

He concedes the real question — *"Stack is right that we should question how the deployment pipelines
should work with agents in play"* — and supplies the sentence this KB should keep:

> "CI with humans relies on them being disciplined to run commit tests locally before pushing to the CI
> server — **and that we can (and should) automate that when using agents.**"

Plus the framing claim: *"Above all, Continuous Integration is a practice, not just the CI server. Yes, CI
does conflate two jobs: executing verification and coordinating merges. But that's the point: verification
is a necessary part of merging if we want to retain a healthy mainline."* He is self-aware about the
grumpiness (*"I'm being a bit unfair dumping on this article here"*).

**3. "MCP is SOAP for Zoomers"** — Fowler quotes Mickey Petersen's one-liner without comment. A dated
snapshot of protocol scepticism, nothing more; worth one sentence on [[model-context-protocol]] as
recorded scepticism, not as an argument.

**4. Human detection of AI prose is near chance.** Fowler links Willison's LLM cliché highlighter and,
via Wikipedia's "Signs of AI writing," relays: *"a 2025 study has shown that human ability to distinguish
LLM text from human is no better than random chance,"* and a 2025 German-theses study with a *"recognition
rate of 57% for AI texts and 64% for human-generated texts."* He then turns it on himself — *"Not just do
I find myself repelled by prose with an LLM-voice, I also wonder how accurate my reaction is."* **These
figures are relayed through Wikipedia; neither study is named or captured. Do not cite them as studies from
this page.** They do bear directly on [[highsmith-practitioner-voice]]'s "LLM Voice" claim, which assumes
the reader can tell.

**5. Off-thread:** Claus Wilke's rebuttal of AI-bioweapon fears (*"Computational design of biological
systems is unfathomably difficult"*), and an arXiv **preprint** (2606.02184) showing LLMs generate
**correlated ensembles** of fictional expert names ("Elena Vasquez and Marcus Chen") whose *"co-occurrence
rates far exceed chance and are consistent across independent generations."* **PREPRINT, not peer
reviewed.** Mildly interesting for hallucination-shape work; not on any KB thread.

## Limits

- **A link roundup.** Nothing here is Fowler's own research, and only the CI fragment is his own argument.
  Every factual claim is secondhand and no primary is captured (NVIDIA AVO, the Stack post, the two
  detection studies, the ghost-names preprint).
- **AVO's numbers are unverified and self-reported**, with no methodology, cost, attempt count, or
  independent replication in the capture. "100% on ARC-AGI-3" and "ran for seven days" are NVIDIA's.
- **The format resists citation**: fragments are separated only by a snowflake rule, so anything cited
  from here should name which fragment.

## Connections / contrast

- **[[willison-gpt6-astra]]** — the pairing described above. Together, the strongest harness-leverage
  evidence in the KB, and both vendor self-reports.
- **[[miller-pondering-continuous-integration-ai-world-order]]** — the same Stack post, the opposite
  reading of what is new. Fowler: the practice always said verify locally first. Miller: doing so now feels
  like reverting to 2007. Both land on the same remedy. Hold the disagreement open.
- **[[long-running-agents]] and [[agent-harness]]**: AVO's *persistent memory + supervisor* is a direct
  instance of the initializer-executor / progress-file family, and the supervisor watching for
  **stagnation and repeated unproductive cycles** is a stop-condition mechanism — feedback in
  [[feedforward-and-feedback-controls]] terms, and an answer to the "how does a loop know it is stuck"
  question in [[loop-engineering]]. Compare Miller's Bobcat test-run supervisor
  ([[miller-pondering-continuous-integration-ai-world-order]]) and the trust-ledger termination rules on
  [[loop-engineering]]: three independent supervisors, three different things being supervised.
- A **seven-day single-task agent run** is the longest horizon recorded anywhere in this KB and belongs on
  [[long-running-agents]] as a marker of what vendors are claiming, with its caveat attached.
- [[highsmith-practitioner-voice]] and fragment 4 disagree about whether LLM Voice is detectable.

## Related

[[martin-fowler]] · [[agent-harness]] · [[harness-engineering]] · [[long-running-agents]] ·
[[loop-engineering]] · [[willison-gpt6-astra]] ·
[[miller-pondering-continuous-integration-ai-world-order]] · [[model-context-protocol]] ·
[[feedforward-and-feedback-controls]] · [[highsmith-practitioner-voice]] · [[unattended-coding-agents]]
