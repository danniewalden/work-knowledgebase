---
title: "Source: Miller — The \"Open Core\" Model for Sustainable OSS Development in .NET"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [miller-open-core-model-sustainable-oss-dotnet]
raw_file: [raw/articles/miller-open-core-model-sustainable-oss-dotnet.md]
tags: [critter-stack, oss-business-model, off-thread, vendor-self-report, short]
---

# Source: Miller — The "Open Core" Model for Sustainable OSS Development in .NET

Post by **[[jeremy-miller]]**, 2026-08-28. Raw capture:
`raw/articles/miller-open-core-model-sustainable-oss-dotnet.md`. **Deliberately short page: this is
mostly an OSS licensing and business-model post, which is off-thread for this KB.** It is kept for two
on-thread data points, exactly as its capture note says. **VENDOR SELF-REPORT** throughout — the founder
of JasperFx on JasperFx's commercial strategy.

## Summary

Miller restates JasperFx's **open-core** commitment: Marten and Wolverine stay MIT-licensed; revenue comes
from consulting and support plans plus commercial products (AI Skills, CritterWatch). He pushes back on
"rug pull" suspicion in the .NET community, and works through his stance on Polly's adoption of the Open
Source Maintenance Fee licence (inclined to pay it; would replace Polly rather than expose customers to
licence doubt, at the cost of a major version or a SemVer violation).

## Key points — the two things worth carrying

**1. A dated confirmation of unshipped roadmap.** *"With another set of commercial tools related to AI
assisted development and Event Modeling coming soon (those will be part of the same license as
CritterWatch)."* This is the 2026-08-28 follow-up to the strategy announced in
[[miller-jasperfx-critterstack-ai-event-modeling-strategy]] — still **announced, not shipped**, which is
the useful fact. (The capture note adds that his same-week Wolverine 6.30 release note mentions
*"smuggled in some support for our soon forthcoming 'Event Modeling' visualization support across the
Critter Stack"* — that release note is **not** in `raw/`.)

**2. The durability argument against "vibe code your dependencies."** The substantive claim, and the only
one with reach beyond .NET:

> "Yes, the existence of AI tools makes it tempting to think you can just vibe code replacements for your
> 3rd party dependencies over a rainy weekend, but you have to also understand how much hardening widely
> used OSS tools get from being beaten up by users and having to adapt to a world of technical
> irregularities like database outages, Rabbit MQ quietly dropping connections, database overloading,
> network hiccups, database administrators unexpectedly sending a kill signal to a PostgreSQL database
> that turns out to create gaps in sequences… **these kinds of tools achieve deep quality through a lot of
> usage, feedback, and adaptation over time — and all of that takes a lot of time and a long attention
> span.**"

The mechanism is the point: **LLMs change the cost of producing code, not the cost of accumulating the
production beatings that hardened it.** He offers a live example — *"I've personally had to make several
improvements to code subsystems in Marten and Wolverine in the last month that I thought were 'done' and
as stable as they could possibly be because new users in new circumstances proved otherwise."*

## Limits

- **Maximally interested.** He sells the commercial tools, maintains the libraries in question, and states
  his own financial stake outright (*"I after all have a fiduciary responsibility to my 'shareholders'"*).
  The durability argument is also an argument for buying his support plans.
- **No measurement of any kind.** The hardening claim is a maintainer's account of his own project; the
  "several improvements in the last month" is unquantified and unspecified.
- Most of the post (Polly/OSMF, community cynicism, licence mechanics) is off-thread and is deliberately
  not summarized further here.

## Connections / contrast

- **The counterweight to [[dudycz-fork-can-you-own-it]]'s "LLM as a fork."** If an LLM can reproduce a
  dependency's *code*, Miller's answer is that the code was never the asset — the accumulated adaptation to
  production irregularity was. The two make a genuine pair on the same question and should be read
  together; neither is measured.
- Context for the [[critter-stack]] page on **why the stack ships what it ships**: the AI Skills and
  CritterWatch exist as the commercial half of an open-core model, which is why the KB's other Critter
  Stack captures are product posts. That is the whole of this capture's value to the wiki's threads.
- Tangentially relevant to [[comprehension-debt]]: a dependency you generated is a dependency nobody has
  been beaten up by yet.

## Related

[[jeremy-miller]] · [[critter-stack]] · [[dudycz-fork-can-you-own-it]] ·
[[miller-jasperfx-critterstack-ai-event-modeling-strategy]] · [[comprehension-debt]] ·
[[agentic-coding]]
