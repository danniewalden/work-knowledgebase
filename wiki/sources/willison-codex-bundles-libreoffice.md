---
title: "Source: Willison — Codex bundles LibreOffice"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [willison-codex-bundles-libreoffice]
raw_file: [raw/articles/willison-codex-bundles-libreoffice.md]
tags: [agent-harness, harness-engineering, openai, short]
---

# Source: Willison — Codex bundles LibreOffice

Short observation post by **[[simon-willison]]**, 2026-09-01. Raw capture:
`raw/articles/willison-codex-bundles-libreoffice.md`. **Deliberately short page — the capture is one
finding long, and the finding is good.**

## Summary

Poking around `~/.cache` with a disk-usage tool, Willison found the OpenAI Codex desktop app (since
rebranded to ChatGPT) carrying **1.7GB in `codex-primary-runtime`**: a full Python install (440.6MB), a
full Node.js install (446.4MB), and native binaries totalling 771MB — **headless LibreOffice (429.7MB)**,
Poppler (187.9MB), git (148.1MB), libheif, jxrlib. And the part that makes it a KB datum:

> "The `~/.cache/codex-runtimes/codex-primary-runtime/plugins/openai-primary-runtime/plugins/documents`
> folder includes **skills which tell Codex how to find and use those binaries**."

## Key points

- **The only durable claim: a commercial harness ships an operating environment, and pairs each capability
  with a skill that teaches the agent to use it.** Binaries alone are inert; the skill is what makes the
  binary reachable. This is [[agent-harness]]'s "bundled infrastructure" primitive made concrete at 1.7GB,
  and it is the same tool↔skill pairing discipline that [[miller-ai-assisted-production-support-with-critterwatch]]
  states as an explicit internal rule ("a tool with no skill coverage is an under-leveraged tool") — one
  vendor doing it for a general runtime, another for a .NET library stack.
- **Corollary for anyone building their own harness:** document-format capability (docx/xlsx/pdf) is
  delivered by shipping LibreOffice and Poppler and telling the agent about them, not by model ability.
  Capability attribution defaults to the model far too easily; this is a case where it is plainly the
  environment.

## Limits

- **One user, one `~/.cache` listing, no vendor statement.** Directory sizes and names are all the
  evidence; the skills' contents were not read or quoted.
- **Nothing is measured** — no claim about whether the bundled binaries improve outcomes.
- Snapshot of one app build on macOS at 2026-09-01.

## Connections / contrast

The disk-side view of [[willison-understanding-chatgpt-work]] (the same product family, seen from its tool
and skill inventory two days earlier, 2026-08-30). Read together they say a rented harness is *an environment plus a skill
catalogue*, mostly undocumented. Also a footnote to [[harness-engineering]]'s "give the model a computer"
principle: OpenAI ships the computer.

## Related

[[agent-harness]] · [[harness-engineering]] · [[willison-understanding-chatgpt-work]] · [[openai]] ·
[[simon-willison]] · [[miller-ai-assisted-production-support-with-critterwatch]]
