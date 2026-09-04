---
source_url: https://jeremydmiller.com/2026/07/10/your-ai-agent-just-got-a-lot-better-at-the-critter-stack-ai-skills-1-6-0/
title: "Your AI Agent Just Got a Lot Better at the Critter Stack: AI Skills 1.6.0"
author: Jeremy D. Miller
publication: The Shade Tree Developer (jeremydmiller.com)
published: 2026-07-10
retrieved: 2026-07-13
type: article
---

# Your AI Agent Just Got a Lot Better at the Critter Stack: AI Skills 1.6.0

*(Jeremy D. Miller, The Shade Tree Developer, 2026-07-10. Verbatim capture. The AGENTIC-ANGLE keeper the watch-config flags Miller for: vendor-authored, source-verified agent skills as the fix for stale-training-data drift on the event-sourcing substrate. Ties to [[critter-stack]] (AI skill files), [[miller-codebase-is-the-prompt-vertical-slices-ai]] (skills encode the conventions), [[harness-engineering]]/[[agent-legibility]], and the skills-as-harness-primitive theme in [[addyosmani-loop-engineering]].)*

JasperFx Software and the greater "Critter Stack" community is advancing our tools pretty rapidly and we have (at least for now) a release cadence that's far more rapid than our competitors in the .NET space. It's perfectly possible to be an experienced Critter Stack user and not be aware of the latest, greatest features, fixes, and improvements.

That's the problem JasperFx AI Skills exists to solve. It's a curated library of agent skills — now 81 of them — covering Wolverine, Marten, Polecat, and CritterWatch, written and maintained by the people who build these tools. Install them once and your agent stops guessing from stale training data and starts working from documentation that's verified against the actual source code, current as of this month, and organized the way agents actually consume knowledge: task-shaped, example-heavy, and honest about the sharp edges.

Release 1.6.0 is out today, and it's a big one. Here's what's inside.

## Ready for the Critter Stack 2026 release

Marten 9 and Wolverine 6 changed the code-generation and deployment story in ways that make most existing internet advice actively wrong. Marten 9 eliminated runtime code generation entirely — no more codegen write step for Marten, no more GeneratedCodeMode knobs, no more Internal/Generated/ folders. Wolverine 6 kept its codegen but moved the Roslyn compiler into the opt-in WolverineFx.RuntimeCompilation package, which means your production image can now run in Static mode with zero Roslyn on disk — roughly 100 MB lighter and Native-AOT-ready.

Every skill in the library that touches code generation was re-audited for this release. The canonical codegen skill now teaches the full Roslyn-free production shape: pre-generate in your Docker build stage, run Static with AssertAllPreGeneratedTypesExist, keep the runtime compiler out of Release builds. And it's precise about the mixed-host nuance that trips people up: a host running both Marten 9 and Wolverine 6 still needs codegen write — but only for the Wolverine half. Your agent will now get that distinction right instead of cargo-culting a Dockerfile step "for the Critter Stack."

## A new troubleshooting line — with the real error messages

Two new skills anchor a troubleshooting category: message routing and service location & code generation. The second one is my favorite thing in this release. When your Wolverine 6 upgrade throws InvalidServiceLocationException at startup (and it will, because the ServiceLocationPolicy default flipped), the skill has the exact exception text, every reason string the codegen can emit — "opaque lambda factory," "concrete type is not public," "directly using IServiceProvider" — and the specific registration fix for each one. Every error message was verified verbatim against the Wolverine and JasperFx source, because an agent pattern-matching on error text needs the real text, not a paraphrase.

It also documents a CI trick that deserves to be better known: dotnet run -- codegen test generates and compiles every handler and endpoint in memory and fails the build on any codegen error — so the opaque registration someone adds on Tuesday fails Tuesday's PR, not Friday's deploy.

## .NET Aspire, done properly

A new consolidated Wolverine with .NET Aspire skill covers the one pattern that repeats across every resource — AddX → WithReference → WaitFor → read the injected connection string — plus a per-provider matrix for SQL Server, MySQL, Oracle, PostgreSQL, RavenDB, and Cosmos DB persistence, and the transport-side stories for RabbitMQ, Kafka, NATS, and Azure Service Bus (including which ones have UsingNamedConnection helpers and which ones don't — we checked the source, there are exactly two). The per-transport skills each gained their own Aspire sections, and the skill is refreshingly blunt about AWS SQS/SNS: there is no first-party Aspire integration, so here's the LocalStack pattern instead.

## CritterWatch operations

The skills aren't just for writing code — they work with CritterWatch, our monitoring and operations console for the Critter Stack, too. Three new skills cover operating a fleet: service actions (like evicting a stale service registration), the embedded CLI (cw-* read commands), and lifecycle diagnostics — on top of the existing setup and routing-diagnostics skills. If you're running CritterWatch, your agent can now help you install it, wire it into Aspire, and operate it day to day.

## Self-contained by design

A principle we hardened this release: if a skill shows you a helper method, the skill carries the complete source. The TrackedHttpCall helper that makes Alba + Wolverine integration testing so pleasant? It's never shipped in a NuGet — it's a pattern from Wolverine's own test suite, and every testing skill now embeds the full method and says so explicitly. Same for the Azure Service Bus emulator helper. No more agents (or humans) hunting for a package reference that doesn't exist. Where we found the upstream docs implying otherwise, we filed the issues too.

## And the steady sharpening

Beyond the headlines: clarified exactly when Marten's IncludeType<T>() is needed (only when Marten can't infer event types — explicit Evolve overrides or base-type Apply methods), covered Wolverine 6.17's HTTP QUERY verb support, [AsParameters] binding patterns, Polecat's typed streaming result types for HTTP endpoints, migration-guide fixes driven directly by user feedback, and more. Twenty-four merged PRs since 1.5.0, every open issue in the tracker closed.

## Getting it

AI Skills is available for purchase at jasperfx.net/our-products. Once you're licensed, it ships as the JasperFx.AiSkills package on the JasperFx feed:

    agentskills-cli add JasperFx.AiSkills

Browse the full catalog and per-release changelog at the AI Skills documentation site to see exactly what your agent would be working from. And if your agent still gets something wrong — file an issue. Half of this release started life as user feedback, and the loop from "the skill told me something stale" to "fixed, verified against source, released" is exactly the point of maintaining these ourselves.
