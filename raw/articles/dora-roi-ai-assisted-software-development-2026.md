---
source_url: https://www.infoq.com/news/2026/05/dora-roi-ai-assisted-dev-report/
title: "New DORA Report Claims Strong Engineering Foundations Drive AI Return on Investment"
author: Matt Saunders
publication: InfoQ (C4Media)
published: 2026-05-11
retrieved: 2026-08-03
type: article
note: >
  Verbatim capture of InfoQ's report-writeup of DORA's "ROI of AI-Assisted Software
  Development" report (v2026.01, DORA/Google Cloud, last updated 2026-04-22). The DORA
  PRIMARY itself is a gated Google Cloud lead-gen download
  (cloud.google.com/resources/content/dora-roi-of-ai-assisted-software-development) and
  the dora.dev/ai/roi/report/ + /calculator/ pages are content-free landing pages, so
  this reputable secondary — which quotes the primary directly — is the most substantive
  fetchable record. This is the [[dora]] future-marker the KB flagged; it grounds
  [[skelton-team-topologies-foundation-ai-roi]]. If the gated PDF is ever obtained, this
  should be superseded/supplemented by the primary.
---

# New DORA Report Claims Strong Engineering Foundations Drive AI Return on Investment

*May 11, 2026 · by Matt Saunders · InfoQ (DevOps)*

Google Cloud's [DORA](https://dora.dev/) team has published an updated report, the ROI of
AI-Assisted Software Development (2026.01) offering a practical framework for calculating the
financial return on AI investment in software development. The report sets out a structured model
for translating engineering metrics into business value. It is a follow up to the 2025 DORA State
of AI-Assisted Software Development report and was authored by a team from Google Cloud's DORA
group and its delta innovation practice.

The report's central argument is that AI acts as an amplifier. "The greatest returns on AI
investment come not from the tools themselves but from a strategic focus on the underlying
organizational system: the quality of the internal platform, the clarity of workflows, and the
alignment of teams," writes Nathen Harvey, the DORA team lead at Google Cloud. "Without this
foundation, AI creates localized pockets of productivity that are often lost in downstream chaos."
This framing directly echoes the 2025 DORA research, which found that AI magnifies the strengths of
high-performing organisations and the dysfunctions of struggling ones.

[Figure: The J-Curve of AI value realisation (copyright DORA)]

A key idea in the report is the J-Curve of value realisation. The authors argue that most
organisations will experience a temporary productivity dip before achieving long-term gains from AI
adoption. This dip has three main causes: the learning curve as teams adapt their workflows, the
verification tax imposed by reviewing AI-generated code, and the need to adapt downstream processes
such as testing and change approval to handle increased code volumes. The report describes this
period as "the tuition cost of transformation" and argues that leaders who misread it as failure
risk pulling funding during the dip and losing the eventual return.

The report's methodology for computing ROI is built on a value model drawn from Google Cloud's
Value Realisation practice. Value flows from AI adoption through a set of seven capabilities;
including a quality internal platform, version control practices, and AI-accessible internal data.
This flows into improved DORA delivery metrics, then into non-financial outcomes such as developer
experience and user experience, and finally into financial outcomes: cost savings and revenue
growth. The ROI is calculated using the standard formula: value minus investment, divided by
investment. Using illustrative figures for a 500-person engineering organisation with a fully
loaded salary of $176,000 per head, the report models a first-year return of approximately $11.6
million against an investment of $8.4 million, yielding a 39% ROI and a payback period of around
eight months.

The report is careful not to overstate these figures. "Treat these calculations as a
high-uncertainty estimate meant to spark a conversation, rather than a rigid mathematical formula,"
the authors write. They note that inference costs for AI models have fallen dramatically; dropping
by a factor of 280 between November 2022 and October 2024 according to the Stanford Artificial
Intelligence Index. This means that the true financial burden of adoption has shifted to
governance: managing the verification tax, adjusting workflows, and upskilling staff.

> "We don't measure AI by the code it writes but by the bottlenecks it clears."
> — DORA team, Google Cloud, ROI of AI-Assisted Software Development report

The report also highlights the instability tax. Drawing on the 2025 DORA research, it notes that
while AI adoption is associated with increased individual effectiveness and code quality, it is
also associated with a rise in software delivery instability. More code moving faster can overwhelm
existing deployment pipelines and manual review gates. The model accounts for this as a cost, and
the sample calculator actually shows a negative downtime impact of $344,000 because the assumed
change failure rate rises from 5% to 6% after AI adoption. The authors present this not as a reason
to delay adoption, but as a reason to invest in automated testing, continuous integration, and
working in small batches.

InfoQ has previously covered the evolution of DORA's AI research. In September 2025, InfoQ reported
on the 2025 DORA State of AI-Assisted Software Development, which introduced the DORA AI
Capabilities Model and identified the seven distinct team archetypes ranging from high-achievers to
organisations stuck in a legacy bottleneck. A March 2026 InfoQ analysis of that report noted that
the research drew on surveys from nearly 5,000 technology professionals and over 100 hours of
qualitative interviews, and concluded that "AI will not fix broken engineering systems."

The new ROI report complements that earlier work by giving engineering leaders a concrete financial
toolkit. It includes an interactive calculator that organisations can use to adjust the assumptions
to their own context. The authors recommend running three scenarios: conservative, realistic, and
optimistic, to build a range of outcomes and set appropriate expectations with finance teams.

Community reactions to the report have been broadly supportive of its framing. Karol Wojtaszek
noted on LinkedIn that the report addresses the real question executives are asking about AI
spending. Andreas Wiesmueller wrote on LinkedIn that "AI without engineering excellence just scales
your problems," a view closely aligned with the report's emphasis on organisational foundations.
Writing in a LinkedIn article on why AI ROI requires process redesign, Ravi Kalakota, a technology
strategist based in New York and not affiliated with Google, argued that "real ROI doesn't come
from the Large Language Model; it comes from the Model Redesign," adding that "deploying AI without
operational redesign is just an expensive, high-speed way to stay the same."

This tension between tool adoption and organisational readiness is not new territory for DORA. The
same dynamic has appeared in prior DORA research on continuous delivery and platform engineering,
both of which showed initial productivity dips before long-term gains. The report draws an explicit
parallel, noting that the J-Curve "consistently" appears across these technical disciplines.
Research cited in the report from Stanford University's Software Engineering Productivity programme
found that while AI yields a 35 to 40% productivity gain on simple, greenfield tasks, its impact on
complex legacy code is often 10% or less; a finding that matters for the many organisations working
primarily on existing systems.

The report also addresses what it calls the "agentic era," describing a shift from reactive AI
tools to autonomous systems capable of executing multi-step workflows. In this context, the authors
reframe how ROI should be understood. The report strongly discourages headcount reduction as a
strategy, arguing that retaining and training existing staff is more cost-effective and preserves
institutional knowledge.

> "Return on investment is no longer a measure of how many developers an organization can replace.
> It is a measure of how much latent human creativity can be unlocked by offloading systemic toil
> to these autonomous agents."
> — DORA team, Google Cloud, ROI of AI-Assisted Software Development report

For the longer term, the authors point to Google Cloud data showing an average 727% return on
investment in Google Cloud AI over three years, and an average payback period of around eight
months. They frame the first year as primarily a period of foundation building and organisational
change, with compounding gains in years two and three as teams move from simple coding assistants
to agentic workflows at scale. The report is available at dora.dev/ai/roi/report.
