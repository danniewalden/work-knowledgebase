---
source_url: https://www.latent.space/p/astra
title: "GPT-6 Astra: an automated AI Engineer you can hire for <$6 an hour"
author: swyx (Latent.Space)
publication: Latent.Space
published: 2026-09-03
retrieved: 2026-09-04
type: article
capture_note: >
  Full free post (not paywalled). The author states mid-post that the writeup is
  unfinished — "We are out of time for this writeup, will complete this later" —
  so the published text captured here is itself a partial draft that may be
  extended at the source. Screenshots of agent logs and benchmark UIs carried
  most of the evidence in the original; they are noted inline as [image: ...]
  since their content is not reproducible as text.
---

# GPT-6 Astra: an automated AI Engineer you can hire for <$6 an hour

### We spent 20B+ tokens of GPT-6 Astra to explore everything. Here's our learnings.

*Sep 03, 2026*

**GPT-6 Astra**, the first [Stargate](https://x.com/ZeffMax/status/2095582617035063375?s=20) and [lightly looped](https://x.com/rasbt/status/2095141254958858496) supermodel from OpenAI, [launched today](http://GPT-6 Astra's launch), cleanly beating [Fable 5.1](https://www.latent.space/p/ainews-claude-fablemythos-51-new) on many metrics including completely saturating the hardest versions of [FrontierMath](https://buttondown.com/ainews/archive/ainews-frontiermath-a-benchmark-for-evaluating/) (97.6%) and [ARC-AGI-3](https://openai.com/index/gpt-6-astra/#citation-top-1) (99.9%). Lots of demos will focus on typical talk tracks like the [computer use](https://x.com/OpenAI/status/2095595741528125780) to the [Pokemon playing](https://x.com/Clad3815/status/2095596013168050551) to [Blender](https://x.com/tomkrcha/status/2095598645190291775) to the [scientific](https://x.com/polynoamial/status/2095583211950833768) and [cybersafety](https://openai.com/index/gpt-6-astra/#citation-top-13) benchmarks ([system card](https://deploymentsafety.openai.com/gpt-6-astra)). Greg says [AGI is here](https://x.com/ZeffMax/status/2095582614648447179), and Jakub says it is [finally the Automated AI Research Intern](https://www.latent.space/p/ainews-openai-to-reach-agi-bar-by) he wanted.

We aren't qualified to talk about those, but we got early access and threw it at every practical, real-life task we could think of. After burning **over 20B tokens of Astra**, we can confirm the most surprising finding: **GPT-6 Astra** **is one of a new class of models**[1](#footnote-1) **that are fully capable AI Engineers in their own right**. They now help you **choose and train models**, **label data** (both helping you label and then using your labels for active learning, like [SAM](https://www.youtube.com/watch?v=sVo7SC62voA)), **keep pipelines saturated**, **instrument and read logs**, **deploy and debug entire systems** in one shot, fan out and **command and eval subagents** (including agents running other models), and keep coherence over **billions** of tokens of a single agent thread.

[image: post header graphic]

## Raising Your Ambitions

We've written before about [the high-return activity of raising your aspirations for LLMs](https://www.latent.space/p/ainews-the-high-return-activity-of?utm_source=publication-search). **Our experience has made us exponentially more ambitious than we have ever been**. Over the past month, we went from prompting humans for a fun "[Kill My SaaS](https://x.com/swyx/status/2085517544795079014)" competition[2](#footnote-2), to building a [dozen internal/personal tools](https://tools.aieconf.com/), including [4 previously paid SaaS tools](https://swyx.io/tools), fully [redesigned my personal site](https://swyx.io/), made an incomplete but functional [replacement of GitHub + Vercel](https://forge.smol.ai/), trained game AI for [a strategy board game with 10,000x more legal moves than Go](https://overgrid.swyx.io/#ai-rivals), saved tens of thousands of dollars in personal finance cleanups, [republished my old book](https://learninpublic.org/) with synced audiobook audio and printed physical editions, and even [more](https://aeo.latent.space/) [ambitious](https://news.latent.space/) projects we will launch soon.

The $6 an hour number might sound surprising, but that's exactly what we saw in [our testing](https://aeo.latent.space/#operations) - 33 tokens per second at a max $50 per million token rate. Given that Astra is more token efficient than Sol and Fable ([independently confirmed by Artificial Analysis](https://x.com/ArtificialAnlys/status/2095595494081024077)), it often means that Astra is simultaneously also the best fast-and-smart model you can buy (assuming our preview latency holds for GA), outside of [Spark 1.3](https://www.latent.space/p/ainews-muse-spark-13-matches-gpt).

[image: screenshot of the authors' token/cost logs, captioned "our logs" and linking to aeo.latent.space/#operations]

## Managing fleets of subagents (individually tweaked, bounded concurrency)

Now of course, if you just throw on Astra at Ultra you're gonna burn through a lot more than $6 per hour…. because it is so dang good at parallelizing.

[image: screenshot of a fleet of subagents running with bounded concurrency]

## Monitoring its own runs, starting and stopping waves

This is basically what i'd pay a junior AI Engineer to do. and I spent about $100 over 2 days to do this.

[image: screenshot of the agent monitoring its own runs, starting and stopping waves]

## Making model benchmarks, handling money, making estimates, scaling up runs, getting human ratings

Wild.

[image: screenshot of agent-produced benchmark planning / cost estimation]

[image: screenshot of a benchmark suite UI, captioned "example here" linking to swyxbench.sites.smol.ai/suites/aie-transcription/]

We are out of time for this writeup, will complete this later, so if you are reading this on email, check back at the end of the day.

However the overall conclusion you should have is that OpenAI have clearly trained a model that is capable of automating much of their own AI Engineering, and it is finally time that you learn to exploit Astra- and Fable-class models and be far, [far more unreasonable](https://www.youtube.com/watch?v=9fubhllmsBU&pp=0gcJCUAdAYcqIYzv).

[video embed: https://www.youtube-nocookie.com/embed/qqrk7CtkuIw]

[1](#footnote-anchor-1)

We are [running similar work](https://aeo.latent.space/) on Grok, Fable and other similar frontier models but OpenAI was most generous with trial limits so this gets the writeup - but the agentic coding patterns discussed here will likely apply to all such late 2026 frontier models.

[2](#footnote-anchor-2)

Many of you are waiting to hear results… sorry for the radio silence! we got… busy! We will announce winners and reimbursements and best attempts.
