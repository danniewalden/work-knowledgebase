---
title: NVIDIA
type: entity
created: 2026-09-04
updated: 2026-09-04
sources: [fowler-fragments-2026-09-01]
tags: [org, agent-harness, vendor, thin-page]
---

# NVIDIA

> **Read the next paragraph before citing this page.** The KB holds **no primary capture about NVIDIA**.
> Everything below reaches it through **one secondhand paragraph** in a [[martin-fowler]] link roundup.
> This page exists to give that claim's marker a home attached to NVIDIA's name — not because the KB has
> coverage of the company. Batch F's own recommendation was to defer this page until the NVIDIA post is
> captured; it is created thin, and deliberately so.

The only thing the KB knows about NVIDIA on its own threads is **AVO**, an agent harness, and one
result: **100% on ARC-AGI-3** with **Claude Opus 5** as the base model, using persistent memory plus a
supervisor, alongside a **seven-day** kernel-optimization run
([[fowler-fragments-2026-09-01]]).

**Markers, and they are the substance of this page.** The result is **VENDOR SELF-REPORT** — NVIDIA on
NVIDIA's own harness — **and secondhand**, since Fowler is relaying and the NVIDIA post is **not in
`raw/`**. There is **no methodology, no cost, no attempt count and no replication.** The result is
attributed to the **harness**, not to the model, which is what makes it interesting at all: paired with
OpenAI's ARC-AGI-3 harness result ([[willison-gpt6-astra]]), it supports only the narrow reading that
*on one benchmark, two vendors independently moved the score a long way by changing the harness, and
both reported it themselves.* Rendering the pair as "harnesses measurably beat models" is the costliest
available error here.

**Named capture gap:** the NVIDIA AVO blog post (developer.nvidia.com, ~2026-09). It is the
highest-value outstanding capture on this thread, and the precondition for this page becoming more than
a stub.

Nothing else about NVIDIA — products, chips, market position — is evidenced by the KB's captures, and
nothing is asserted here.

## Related

[[agent-harness]] · [[harness-engineering]] · [[anthropic]] · [[openai]] · [[martin-fowler]]

_Source pages: [[fowler-fragments-2026-09-01]] (a secondhand relay — the only source)._
