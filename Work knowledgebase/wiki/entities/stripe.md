---
title: Stripe
type: entity
created: 2026-06-11
updated: 2026-06-11
sources: [stripe-minions-one-shot-coding-agents]
tags: [organization, fintech, harness-engineering, coding-agents]
---

# Stripe

Financial-infrastructure company; its payments code moves well over $1T/year in production. In the
KB, Stripe is the source of a flagship production [[harness-engineering]] case study
([[stripe-minions-one-shot-coding-agents]], by Alistair Gray of the internal "Leverage" team).

Stripe's **minions** are fully [[unattended-coding-agents|unattended, one-shot coding agents]]
producing **1,000+ merged PRs/week** (human-reviewed, no human-written code). Built on a fork of
Block's **goose** agent, they interleave the agent loop with deterministic git/lint/test steps, run
in pre-warmed isolated "devboxes," gather context over [[model-context-protocol|MCP]] via a 400+-tool
internal server ("Toolshed"), and lean hard on **shift-left feedback** — heuristic <5s pre-push lints
plus selective CI over 3M+ tests with autofixes ([[feedforward-and-feedback-controls]]). Guiding
principle: "if it's good for humans, it's good for LLMs, too." Sits alongside [[openai]] and
[[anthropic]] as a builder-side voice; a Part 2 on implementation is a candidate for a future ingest.

_Source: [[stripe-minions-one-shot-coding-agents]]._
