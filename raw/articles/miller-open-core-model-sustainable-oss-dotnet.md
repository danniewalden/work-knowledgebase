---
source_url: https://jeremydmiller.com/2026/08/28/the-open-core-model-for-sustainable-oss-development-in-net/
title: The "Open Core" Model for Sustainable OSS Development in .NET
author: Jeremy D. Miller
publication: The Shade Tree Developer (jeremydmiller.com)
published: 2026-08-28
retrieved: 2026-08-29
type: article
---

# The "Open Core" Model for Sustainable OSS Development in .NET

It's apparently time to play another game of .NET developers feeling consternation because of an OSS project's attempt to be more sustainable. [JasperFx Software](https://jasperfx.net), the company I founded around the "Critter Stack" tools is committed to an ["Open Core" model](https://en.wikipedia.org/wiki/Open-core_model). What that means for us is that:

1. The main libraries and tools like **[Marten](https://martendb.io) and [Wolverine](https://wolverinefx.io) will remain MIT licensed, i.e. free and open**
2. JasperFx will offer services like straight up consulting or [ongoing support agreements](https://jasperfx.net/support-plans/) (which are also de facto consulting time as well) for any tool in the [JasperFx GitHub organization](https://github.com/jasperfx).
3. JasperFx also has its commercial [AI Skills offerings for the Critter Stack](https://jasperfx.net/our-products/#ai-skills) and now our [commercial CritterWatch tool](https://critterwatch.jasperfx.net). With another set of commercial tools related to AI assisted development and Event Modeling coming soon (those will be part of the same license as CritterWatch)

At this point I think that JasperFx Software has already established that we have a viable business model and that we're going to be able to sustain our "Open Core" model going forward.

We still get occasional friction from potential clients and users that we'll do the same OSS "rug pull" that some other projects did by adopting a commercial license on their newer versions even though I've said "Open Core" in public a half a thousand times. I do not particularly enjoy that level of cynicism about OSS that frequently crops up in the ,NET community.

What I would say to folks out there is that tools like Marten and Wolverine are just not viable as side projects. A huge amount of our functionality in Marten for scalability only existed after I founded JasperFx and started working directly with clients every day. Wolverine's leadership election which undergirds a lot of our advanced blue/green deployment support and scalability would not have been possible to build and constantly curate without me being full time on the Critter Stack. I would ask our users to have some awareness for how much time it takes to evolve and maintain their OSS tools.

Yes, the existence of AI tools makes it tempting to think you can just vibe code replacements for your 3rd party dependencies over a rainy weekend, but you have to also understand how much hardening widely used OSS tools get from being beaten up by users and having to adapt to a world of technical irregularities like database outages, Rabbit MQ quietly dropping connections, database overloading, network hiccups, database administrators unexpectedly sending a kill signal to a PostgreSQL database that turns out to create gaps in sequences (and wasn't that one fun), and not to mention all the crazy edge cases we've had to face from Kubernetes doing Kubernetes things.

To sum this all up, you can't just vibe code replacements for quite a bit of this, these kinds of tools achieve deep quality through a lot of usage, feedback, and adaptation over time — and all of that takes a lot of time and a long attention span.

Hell, I've personally had to make several improvements to code subsystems in Marten and Wolverine in the last month that I thought were "done" and as stable as they could possibly be because new users in new circumstances proved otherwise

And just because I might get asked about this, my friend [Ian Cooper wrote about this too](https://www.linkedin.com/feed/update/urn:li:activity:7499006926417039360/), but maybe coming from a different perspective as an OSS maintainer. I partially agree with some of that and I'll respectfully disagree with other parts and just leave it at that.

## The JasperFx Stance on Polly and OSMF

The "[Open Source Maintenance Fee](https://opensourcemaintenancefee.org/)" is a new attempt to make OSS projects by getting some kind of funding to the maintainers, and about six weeks ago the very widely used [Polly project announced that they were adopting the new OSMF license](https://thepollyproject.org/2026/07/14/polly-osmf-announcement.html).

I'm obviously sympathetic to the Polly maintainers, and based on this exchange with one of the creators of the OSMF, my initial inclination is to pay the OSMF fee from JasperFx Software because of our commercialization of [Marten](https://martendb.io), [Polecat](https://polecat.jasperfx.net), and [Fisher](https://fisher.jasperfx.net) **through support plans** (those projects are still MIT licensed folks!) and the transitive dependency that CritterWatch has on Polly through those other libraries:

> [Comment by u/danielkzu from discussion in r/moderndotnet, "Another project jumps on the OSMF bandwagon"]

Like I said, I'm sympathetic to the Polly maintainers, and we'll try to be above board with them here. But, if there's even the slightest bit of hesitation from our current or potential customers about the Polly license, we'll replace our relatively small usage of Polly with something new in our foundational JasperFx library and remove Polly entirely. I'm not enthusiastic about doing that because the Polly.Core dependency is in our public API and pulling that out would require us to either do a major version release or cheat on SemVer rules — which we really hate to do without very good reason.

*I after all have a fiduciary responsibility to my "shareholders" to make JasperFx a sustainable financial success.*

Wolverine has its own resiliency features, so Polly isn't a concern there at least. Our document database and event store applications do use Polly for resiliency against transient errors though, and that's what would need to change. I'd guess that most of our users don't even realize that's there, so maybe the switchover won't be that big a deal if we decide to go that way.

---

*Capture note (watch, 2026-08-29): filed under the people watch (`people_scope: anything-substantive`). Mostly OSS-sustainability/licensing and off the KB's threads, kept for two on-thread data points. (1) A dated confirmation that JasperFx has **"another set of commercial tools related to AI assisted development and Event Modeling coming soon"** — the follow-up to [[miller-jasperfx-critterstack-ai-event-modeling-strategy]] and [[miller-jasperfx-ai-skills-agent-skills]]; his same-week Wolverine 6.30 release note (2026-08-25, surfaced but not filed) adds that they "smuggled in some support for our soon forthcoming 'Event Modeling' visualization support across the Critter Stack and more for CritterWatch visualization." (2) An anti-"vibe code your dependencies" argument that is the durability counterweight to [[dudycz-fork-can-you-own-it]]'s "LLM as a fork": LLMs change the cost of producing code, not the cost of the years of production beatings that hardened it — "these kinds of tools achieve deep quality through a lot of usage, feedback, and adaptation over time."*
