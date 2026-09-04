---
title: "DORA — ROI of AI-Assisted Software Development report (2026.01)"
type: source
created: 2026-08-03
updated: 2026-08-03
sources: [dora-roi-ai-assisted-software-development-2026]
raw_file: [raw/articles/dora-roi-ai-assisted-software-development-2026.md]
tags: [dora, agentic-ai, ai-roi, market, governance, business-capabilities, harness-engineering, focus]
---

# DORA — ROI of AI-Assisted Software Development report (2026.01)

The **2026 DORA ROI report** (v2026.01, [[dora|DORA]] / Google Cloud, last updated 2026-04-22) — a
practical framework for calculating the financial return on AI investment in software development, and a
follow-up to the 2025 *State of AI-Assisted Software Development* report. Raw capture:
`raw/articles/dora-roi-ai-assisted-software-development-2026.md`.

**Provenance caveat (read first):** the DORA **primary is a gated Google Cloud lead-gen download** and
the `dora.dev/ai/roi/` pages are content-free landing pages, so this page is compiled from **InfoQ's
report-writeup** (Matt Saunders, 2026-05-11), which quotes the primary directly. Treat the figures as
DORA's own *illustrative* numbers relayed through a reputable secondary; supersede this page if the gated
PDF is ever obtained. This closes the KB's standing **[[dora]] future-marker** and is the primary behind
[[skelton-team-topologies-foundation-ai-roi|Skelton's "Team Topologies as the foundation for AI ROI"]].

## The core thesis — AI is an amplifier

> "The greatest returns on AI investment come not from the tools themselves but from a strategic focus on
> the underlying organizational system: the quality of the internal platform, the clarity of workflows,
> and the alignment of teams." — Nathen Harvey, DORA team lead

Without that foundation, "AI creates localized pockets of productivity that are often lost in downstream
chaos." This restates the 2025 DORA finding that AI **magnifies** the strengths of high-performing orgs
and the dysfunctions of struggling ones — the same environment-over-tooling through-line the KB tracks in
[[tornhill-why-human-level-ai-wont-be-enough|Tornhill]] and [[dilger-harness-is-20-percent-requirements-are-80|Dilger's
"harness is 20%"]].

## The J-Curve of value realisation

Most organizations hit a **temporary productivity dip before long-term gains** — "the tuition cost of
transformation." Three causes:

1. **Learning curve** — teams adapting their workflows to AI.
2. **Verification tax** — the cost of reviewing AI-generated code for trust/security/standards.
3. **Downstream adaptation** — testing and change-approval processes must be reworked to handle larger
   code volumes.

The warning to leaders: don't misread the dip as failure and pull funding before the return arrives. The
report says the J-Curve "consistently" recurs across prior technical disciplines (continuous delivery,
platform engineering).

## The ROI model

Value **flows through a chain**: AI adoption → **seven capabilities** (incl. a quality internal
platform, version-control practices, AI-accessible internal data) → improved **DORA delivery metrics** →
non-financial outcomes (developer experience, user experience) → **financial outcomes** (cost savings,
revenue growth). ROI = (value − investment) / investment.

Illustrative figures (a 500-person eng org, $176k fully-loaded salary/head): **~$11.6M return vs $8.4M
investment = 39% first-year ROI, ~8-month payback** — explicitly flagged "a high-uncertainty estimate
meant to spark a conversation, rather than a rigid mathematical formula." An interactive **calculator**
accompanies it; the authors recommend running conservative / realistic / optimistic scenarios. Because
inference cost fell ~280× (Nov 2022 → Oct 2024, Stanford AI Index), the true burden has **shifted from
compute to governance** — managing the verification tax, adjusting workflows, upskilling staff.

> "We don't measure AI by the code it writes but by the bottlenecks it clears." — DORA team

## The instability tax

AI raises individual effectiveness and code quality but is associated with **rising delivery
instability**: more code moving faster overwhelms pipelines and manual review gates. The sample
calculator shows a **negative downtime impact of $344k** as the assumed change-failure rate rises 5% →
6% post-adoption — presented not as a reason to delay but as a reason to invest in **automated testing,
CI, and small batches**. Corroborating context: Stanford's SE-Productivity work found AI yields **35–40%
gains on greenfield tasks but ≤10% on complex legacy code** — decisive for the many orgs on existing
systems.

## The agentic-era reframing

The report describes the shift from reactive AI tools to **autonomous multi-step agents** and
**discourages headcount reduction** (retaining/training staff is more cost-effective and preserves
institutional knowledge):

> "Return on investment is no longer a measure of how many developers an organization can replace. It is
> a measure of how much latent human creativity can be unlocked by offloading systemic toil to these
> autonomous agents." — DORA team

Long-term, they cite Google Cloud data of an average **727% ROI over three years** (~8-month payback),
framing year one as foundation-building with compounding gains in years two–three as teams move from
coding assistants to agentic workflows at scale.

## Why it matters here

- **Closes the [[dora]] future-marker** and supplies the primary grounding for
  [[skelton-team-topologies-foundation-ai-roi]] — Skelton's whole argument is a reading of *this* report.
- **Independent-ish empirical weight** on the KB's **environment-over-model** through-line: the
  "verification tax" is the ROI-accounting name for the maker≠checker cost the [[loop-engineering]] /
  [[harness-engineering]] thread keeps flagging, and "AI is an amplifier" is the market-research
  counterpart to [[borg-tornhill-code-for-machines-not-just-humans|Borg/Tornhill's]] measured code-health
  effect and Dilger's 80/20.
- **The seven-capabilities → outcomes chain** ties AI ROI to [[business-capabilities]] and to
  [[agent-governance]] (the report explicitly relocates the cost centre to governance).
- Caveat: **vendor (Google Cloud) framing**, **captured via a secondary** (primary is gated), and the
  headline figures are self-labelled illustrative — evidence of *framing and direction*, not audited ROI.

## Links

Entities: [[dora]], [[matthew-skelton]]. Concepts: [[agentic-ai]], [[agent-governance]],
[[business-capabilities]], [[harness-engineering]], [[loop-engineering]], [[agentic-coding]],
[[team-topologies]], [[autonomy-ladder]].
Related sources: [[skelton-team-topologies-foundation-ai-roi]],
[[devadoss-cead-capability-aligned-agent-design]], [[deloitte-ai-agents-scaling-faster-than-guardrails]],
[[langchain-state-of-agent-engineering-2026]], [[tornhill-why-human-level-ai-wont-be-enough]].

_Raw source: `raw/articles/dora-roi-ai-assisted-software-development-2026.md`._
