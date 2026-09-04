---
title: "Source: Willison — GPT-6 Astra (the ARC-AGI-3 harness result)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [willison-gpt6-astra]
raw_file: [raw/articles/willison-gpt6-astra.md]
tags: [agent-harness, harness-engineering, benchmarks, frontier-models, openai, vendor-self-report, focus]
---

# Source: Willison — GPT-6 Astra (the ARC-AGI-3 harness result)

Blogmark by **[[simon-willison]]**, 2026-09-03, linking [[openai]]'s GPT-6 Astra launch page (via Hacker
News). Raw capture: `raw/articles/willison-gpt6-astra.md`. Willison is explicit that he **had not tried
the model** — *"I've not tried it yet myself, so I don't have a great deal to say about it yet"* — so this
is a **relay of launch material with one third-party cross-check**, not a review. Almost everything
quantitative in it is **VENDOR SELF-REPORT** ([[openai]]'s own numbers about its own model).

## Summary

The capture matters to this KB for one reason, and it is not the model. Buried in the benchmark round-up
is a **harness-not-model result on a single benchmark, with cost attached**, and it is the cleanest such
datum the KB holds. The rest of the page — pricing parity with Claude Fable 5/5.1 at **$10/million input
and $50/million output**, security-benchmark sweeps, long-context scores, the API label `gpt-6-astra` — is
launch-day context.

## Key points

**The harness datum (the reason this page exists).** On [ARC-AGI-3](https://arcprize.org/arc-agi/3)
(released March 2026), as the capture states it:

> "Astra scores 99.9% on the recent (released in March) ARC-AGI 3 benchmark — though notably Fable 5 does
> not yet have a published result, and the ARC-AGI blog notes that the 99.9% score was achieved for **$19K
> using OpenAI's custom 'Provider Adapter harness'**, while the **default ARC-AGI harness scored 62.7% for
> $26K**."

And the mechanism, quoted in the capture from the ARC-AGI blog:

> "The Provider Adapter harness preserves opaque reasoning state between requests and uses compaction for
> longer conversations, allowing the model to reuse prior work."

Three things to hold separately, because they carry different weight:

1. **A 37.2-point spread on the same benchmark with the same model, attributable to the harness alone** —
   and the higher score cost **less** ($19K vs $26K). Capability and cost moved the same direction, which
   is the opposite of the usual reasoning-effort trade (contrast
   [[willison-claude-fable-5-1-animated-pelican]], where 33× the spend bought a better drawing).
2. **The two named mechanisms are specific and small**: retained (opaque) reasoning state across requests,
   plus compaction. Both are ordinary [[agent-harness]] primitives, not model changes.
3. **Attribution is mixed, and the distinction matters.** The 99.9% figure sits in OpenAI's own launch
   material — **VENDOR SELF-REPORT**. The *harness attribution and the dollar figures* are reported by
   the **ARC Prize blog**, i.e. the benchmark maintainer, which is a materially better provenance than the
   rest of the page — but ARC Prize is the party whose benchmark is being saturated, so it is **NOT
   INDEPENDENT** of the benchmark's standing either. Neither party is disinterested; they are interested
   in different things.

**Other OpenAI-reported figures — all VENDOR SELF-REPORT, none replicated:**

- Security: **100% on ExploitBench** (GPT-5.6 Sol 78.5%), **42.4% on ExploitGym** (Sol 30.3%), **99.2%
  within four attempts** on SRE-Bench binary reverse engineering (Sol 68.7%). Willison reads the emphasis
  as a response to "the recent Hugging Face incident."
- Long context, on **OpenAI's own eight-needle benchmark**: 100% at 256K–512K tokens, 96.3% at 512K–1M.
  Willison's gloss — *"OpenAI may have vanquished one of the ongoing challenges with long context
  processing"* — is his speculation on a vendor's own needle test, and should not be carried as a finding
  about [[context-rot]].

**The one third-party cross-check, and it cuts the other way.** Artificial Analysis (independent of both
labs) puts Astra at **61 on their Intelligence Index — equal to GPT-5.6 Sol, five points below Claude
Fable 5.1 (max with fallback)**, and behind Meta's Muse Spark 1.3 (max). It does lead their **Coding Agent
Index cost-efficiency frontier**: at max effort about the same cost as Sol (max) for two more points, and
*"per task… less than half the cost of Claude Fable 5, for the same score."* So the honest one-line summary
of launch day is **cost-efficiency leader, not capability leader** — which is not how the launch material
reads.

## Limits

- **Willison had not used the model.** No independent observation of any kind is in this capture.
- **The 99.9% is not a model-vs-model comparison.** Fable 5 has no published ARC-AGI-3 result, as the
  capture says plainly. Any page that renders this as "Astra beats Fable on ARC-AGI-3" is inventing a
  comparison the source refuses to make.
- **Benchmark saturation is not general capability.** A 99.9% on one reasoning benchmark, achieved with a
  bespoke harness built by the model's own vendor, is a statement about that pairing on that benchmark.
- **No methodology for the $19K/$26K split** is in the capture — what the money bought (attempts?
  parallelism? retries?) is unstated, so the cost figures are directional only.

## Connections / contrast

**This is the corroboration [[mcateer-evolution-of-the-agent-harness]] was missing.** McAteer (2026-08-22)
carried, secondhand and unlinked, that *"GPT-5.6 Sol's ARC-AGI-3 score tripled from 13.3% to 38.3%"* by
"adding only retained reasoning and compaction" — flagged there as an unverifiable OpenAI self-report.
This capture names **the same two mechanisms** (retained reasoning state + compaction), on the same
benchmark, one model generation later, with a **named harness, a linked benchmark-maintainer post, and
cost figures**. The claim is now traceable rather than folkloric. It remains a vendor's harness on a
vendor's model, so it does not become independent — it becomes *citable*.

**And it is not the only ARC-AGI-3 harness result in this batch.** [[fowler-fragments-2026-09-01]] relays
NVIDIA's report of **100% on ARC-AGI-3 using Claude Opus 5 plus their AVO harness** (persistent memory +
a supervisor watching for stagnation) — a *different lab, different base model, different harness
mechanisms, same benchmark*. Two labs independently moved the same benchmark by changing the harness. That
convergence is worth more than either number: it is the strongest evidence in the KB for
[[agent-harness]]'s core claim (**agent = model + harness**) and for [[harness-engineering]] as a
discipline with measurable leverage. Both remain vendor self-reports about their own harnesses.

**Against [[token-budget-quality-cliff]]:** compaction appearing as a *score-raising* mechanism is a live
data point for that page's open question "does compaction help or hurt?" — here, on this benchmark, it
helped. One benchmark, one vendor.

**The weaker sibling.** [[swyx-gpt6-astra-automated-ai-engineer]] covers the same launch from an
early-access seat and is much softer evidence; read that page's caveats before letting its claims lean on
this one.

## Related

[[agent-harness]] · [[harness-engineering]] · [[mcateer-evolution-of-the-agent-harness]] ·
[[fowler-fragments-2026-09-01]] · [[swyx-gpt6-astra-automated-ai-engineer]] · [[openai]] ·
[[simon-willison]] · [[context-rot]] · [[token-budget-quality-cliff]] · [[long-running-agents]]
