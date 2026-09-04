---
source_url: https://jeremydmiller.com/2026/09/02/new-stuff-in-critter-stack-ai-skills-1-10/
title: New stuff in Critter Stack AI Skills 1.10
author: Jeremy Miller
publication: The Shade Tree Developer
published: 2026-09-02
retrieved: 2026-09-03
type: article
---

# New stuff in Critter Stack AI Skills 1.10

We shipped [Critter Stack AI Skills 1.10.0](https://ai-skills.jasperfx.net/whats-new) today. Eleven new skills, which brings the catalog (so far) to **102** across all the Critter Stack tools and trying to cover every use case and common troubleshooting need we can think of.

If you haven't run across these yet, the short version is that AI Skills are structured documentation written for the coding agent rather than for you. Not API reference — the agent can already read that — but the accumulated *"here's what this actually means, here's the trap, here's what to check next"* that otherwise only exists in the heads of the people who built the thing. I wrote up [a whole session of an agent using them against a real codebase](https://jeremydmiller.com/news/ai-skills-and-the-critter-stack-cli) a couple of days ago if you want to see them working.

Our AI Skills will also get your AI agents to use Wolverine, Marten, Alba, and all the other tools in the most idiomatic way possible that should lead to more terse code and in many cases, more performant code. They'll also help your AI agents write more testable code and the automated tests that go with that using all the Critter Stack test utilities we've built over the years. And lastly, the AI Skills help your agents to understand test failures and to utilize all the observability capabilities of the Critter Stack with some help from CritterWatch's MCP support as well as all the command line diagnostics that come along with the Critter Stack.

In short, we're throwing every possible bit of AI spaghetti up against the wall and the AI Skills are kind of the glue of all our AI related tools and approaches.

Here's what's new.

## Sagas, from both directions

[Wolverine Sagas](https://ai-skills.jasperfx.net/skills/wolverine-handlers-sagas) was a big hole in the AI Skills before this release, and now we've got AI Skills coverage on the valid usages of Saga handler signatures and for using [Sagas from HTTP endpoints](https://ai-skills.jasperfx.net/skills/wolverine-http-sagas) covers the part that trips up almost everybody who tries it. In `Wolverine.HTTP`, the *first* return value of an endpoint method is the response body. Which means if you return a `Saga`, congratulations — you've just serialized your saga state to the caller. The `Saga` has to be a later tuple member, and there's an `[EmptyResponse]` shape for when you don't want a body at all. That one fact reshapes the whole topic, and it's exactly the kind of thing that is obvious in retrospect and expensive in the moment.

## Troubleshooting Projections

There are two new projection troubleshooting skills today.

[Troubleshooting a projection](https://ai-skills.jasperfx.net/skills/critterstack-projection-troubleshooting) is the general one: your projection is behind, stalled, or producing a document that's just plain wrong, and you need to figure out which. [The CritterWatch one](https://ai-skills.jasperfx.net/skills/wolverine-integrations-critterwatch-projection-troubleshooting) is the fleet version of running applications in production — `diagnose_projection` to rank shards worst-first, then `run_projection_stepper` to replay your *actual production projection code* over a slice of real events and read the before/after state at every single step.

For development time, we added a new command line tool called `projection-run` to JasperFx.Events and shipped it in Marten and Polecat. Then we added a skill that knows how to use the new "projection stepper" CLI tool and tested it by pointing an agent at a projection I'd deliberately broken and watching where it got stuck.

## Marten: versioning, archiving, and search

We filled in some important gaps for Marten usage in the AI Skills this time around:

[Event versioning and upcasting](https://ai-skills.jasperfx.net/skills/marten-event-versioning-and-upcasting) — renaming an event type, moving a namespace, adding a field, and the three flavors of upcaster for when the change isn't additive.

[Archiving and stream compaction](https://ai-skills.jasperfx.net/skills/marten-archiving-and-stream-compaction) has the fact I most want people to internalize: **archiving alone doesn't shrink anything.** `ArchiveStream` sets a flag. It's `UseArchivedStreamPartitioning` that moves archived events onto separate physical storage and actually buys you the query performance — and it quietly weakens a stream-identity guarantee on the way, which you should know about before you turn it on.

Plus [full-text and NGram search](https://ai-skills.jasperfx.net/skills/marten-full-text-search) — four different query functions and real guidance on which one you want — and [AI features with `Marten.PgVector`](https://ai-skills.jasperfx.net/skills/critterstack-ai-features-with-marten-pgvector) for embeddings, vector search, and event-sourced `VectorProjection`.

## Integrations

[gRPC with Wolverine](https://ai-skills.jasperfx.net/skills/wolverine-integrations-grpc), covering the service-shim-to-bus-to-handler flow, streaming and its cancellation contract, and RPC deduplication.

[MCP servers for your own app](https://ai-skills.jasperfx.net/skills/critterstack-mcp-servers-for-your-app) — twenty shipped tools across `Marten.Mcp`, `Polecat.Mcp` and `WolverineFx.Mcp` that expose *your* application to an agent: query event streams, fetch aggregate state, read daemon status and routing diagnostics, scaffold a vertical slice.

And [CritterWatch alerts](https://ai-skills.jasperfx.net/skills/wolverine-integrations-critterwatch-alerts) — how to acknowledge, snooze, or clear an alert with the right audit attribution, and how metrics alerts are actually decided underneath.

## Getting them

The AI Skills are available standalone or bundled with CritterWatch:

- **[Solo — $250](https://portal.jasperfx.net/buy?sku=ai-skills-solo)**, for individual developers
- **[Team — $1,000](https://portal.jasperfx.net/buy?sku=ai-skills-team)**, for teams under 10 developers
- **[Team (Large) — $2,000](https://portal.jasperfx.net/buy?sku=ai-skills-team-large)**, for teams of 10 or more

All the plans are on the [products page](https://jasperfx.net/our-products/#ai-skills), the full catalog is browsable at [ai-skills.jasperfx.net](https://ai-skills.jasperfx.net/), and they're included with [CritterWatch Professional and Enterprise](https://jasperfx.net/our-products/#critterwatch-plans). Existing subscribers just take the update — the skills ship as the `JasperFx.AiSkills` package, and [the install guide](https://ai-skills.jasperfx.net/install) covers wiring them into Claude Code or whatever agent you're driving.

If there's a corner of the Critter Stack you keep having to re-explain to your agent, [tell us](https://jasperfx.net/contact/). That's genuinely how most of these get picked.

jeremydmiller — Uncategorized — September 2, 2026 — 4 Minutes

---

*Capture note (not the author's words): **VENDOR SELF-REPORT.** This is a JasperFx product-release post by the vendor's founder; the "102 skills", the pricing, and the claims about idiomatic/terser/more-performant agent output are JasperFx's own. The post also links a companion piece, "AI Skills and the Critter Stack CLI" (https://jeremydmiller.com/news/ai-skills-and-the-critter-stack-cli), which is NOT yet in `raw/`.*
