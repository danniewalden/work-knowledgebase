---
title: "Source: Willison — Claude Fable 5.1 made me a really nice animated pelican (the reasoning-effort cost cliff)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [willison-claude-fable-5-1-animated-pelican]
raw_file: [raw/articles/willison-claude-fable-5-1-animated-pelican.md]
tags: [token-budget-quality-cliff, loop-engineering, reasoning-effort, cost, anthropic, off-thread, short]
---

# Source: Willison — Claude Fable 5.1 made me a really nice animated pelican

Post by **[[simon-willison]]**, 2026-09-01, on Claude Fable/Mythos 5.1 launch day. Raw capture:
`raw/articles/willison-claude-fable-5-1-animated-pelican.md`. **Deliberately short page: this is a model
review and mostly off-thread. It was captured for exactly one thing — the reasoning-effort cost cliff on a
single fixed prompt — which is a loop-budget datum.**

## Summary

Willison ran one unchanged prompt ("Generate an SVG of a pelican riding a bicycle") across all five of
Fable 5.1's reasoning-effort levels (low, medium, high, xhigh, max — *"no option to turn off reasoning
entirely"*), recording tokens, wall time and cost at each. The spread is the content.

## Key points

**The cost cliff, exactly as the capture reports it** — same model, same prompt, effort dial only:

| Effort | Output tokens | Wall time | Cost |
| --- | --- | --- | --- |
| low | 1,998 | 23.8 s | 10.017¢ |
| medium | 1,977 | 23 s | 9.912¢ |
| high | 2,612 | 29.6 s | 13.087¢ |
| xhigh | 36,767 | 7 m 51 s | $1.83 |
| max | **65,927** | **13 m 54 s** | **$3.30** |

(Anthropic's output-token count includes reasoning tokens. A follow-up "animate this" turn at `high` cost
$1.37 on 6,121 in / 26,201 out.)

Two things worth carrying:

1. **The dial is not a gradient, it is a step function.** low→high is ~1.3× cost; high→max is **~25×
   cost and ~28× wall time** (≈33× cost from low to max). A budget model that treats reasoning effort as
   linear will be wrong by an order of magnitude, and in an unattended loop the difference between a 24-second
   step and a **14-minute** step is a scheduling property, not a quality knob.
2. **The bottom of the dial is non-monotonic.** At both `low` and `medium` the model *"appeared to skip
   reasoning entirely"* — no summarized reasoning tokens — and **medium used 21 fewer output tokens than
   low**. So the low end of the dial did not do what it says on this prompt. Willison calls it *"a bit of a
   mystery"* and does not explain it.

Willison's own read on quality: `max` gave *"the best pelican I've seen from any of Anthropic's models"*
(a basket with a fish, a blue hat); `xhigh` and `max` reasoning traces show genuine design deliberation
(*"I'll accept the slight thickness as charming rather than overengineering it"*). Quality judgement here
is **IMPRESSION NOT MEASUREMENT** — it is one person's aesthetic read of one drawing.

## Limits

- **n=1 prompt, one run per level, one model, and the task is drawing an SVG.** Nothing generalizes to
  coding or agentic work from this; the *shape* of the cost curve is the transferable part, not the ratios.
- **Willison himself distrusts the benchmark**: since July he has been *"losing faith in the pelican
  benchmark—its connection to how good the models were at other tasks didn't seem to hold as strongly as
  it did back in 2025."* (The claim is comparative — weaker correlation than in 2025, not none.) He keeps
  it only for within-family and across-effort-level comparisons, which is precisely and only how this page
  uses it.
- The launch-day figures he relays (Terminal-Bench-Science 0.1: Fable 5.1 **52.6%** vs Fable 5 24.7%,
  Opus 5 29.0%, GPT-5.6 Sol 22.4%) are **[[anthropic]]'s own announcement numbers on a benchmark first
  announced five days earlier** — **VENDOR SELF-REPORT**, and not something this page relies on.
- The cost figures are from a third-party calculator (llm-prices.com) at 2026-09-01 pricing.

## Connections / contrast

- **[[token-budget-quality-cliff]]** is about quality degrading as budget is *consumed*; this is the
  complementary axis — what buying more budget costs and buys, on a fixed prompt. Both say the same
  practical thing: **budget is a first-class design variable in a loop, not a setting**.
- **Against [[willison-gpt6-astra]]**, from the same week: there, a harness change *raised* the score and
  *lowered* the cost ($19K/99.9% vs $26K/62.7%). Here, more spend on the same harness bought a modestly
  better drawing at 33× the price. Those are the two ends of where leverage lives — a point
  [[harness-engineering]] makes and this capture accidentally illustrates.
- Relevant to [[loop-engineering]]'s budget discussion and to any [[unattended-coding-agents]] cost model.

## Related

[[token-budget-quality-cliff]] · [[loop-engineering]] · [[harness-engineering]] ·
[[willison-gpt6-astra]] · [[simon-willison]] · [[anthropic]] · [[unattended-coding-agents]]
