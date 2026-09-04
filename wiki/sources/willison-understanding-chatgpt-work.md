---
title: "Source: Willison — Understanding ChatGPT Work"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [willison-understanding-chatgpt-work]
raw_file: [raw/articles/willison-understanding-chatgpt-work.md]
tags: [agent-harness, harness-engineering, prompt-injection, agent-legibility, openai, focus]
---

# Source: Willison — Understanding ChatGPT Work

Post by **[[simon-willison]]**, 2026-08-30. Raw capture:
`raw/articles/willison-understanding-chatgpt-work.md`. A reverse-engineering write-up of [[openai]]'s
**ChatGPT Work** (announced 2026-07-09), which he calls *"an extraordinarily confusing and very powerful
product."* First-hand: he used it extensively and built artifacts with it.

## Summary

The interesting content is not the product tour, it is what the tour is *made of*. Willison enumerates
ChatGPT Work's harness — models and reasoning levels, code execution with **open internet access**, a full
headless Chrome, a **persistent filesystem shared across sessions**, subagents, deployable sites,
scheduled prompts — and then, because OpenAI documents Work *"in terms of what it's for, not what it
actually does,"* has to get the agent to inventory **its own tools and skills** to find out what it can
do. The result is simultaneously the KB's most detailed picture of a commercial general-purpose harness
and a clean demonstration of how little of a rented harness is documented.

## Key points

**Two products under one name.** *Work Cloud* (browser/mobile, cloud-executed) and *Work Local* (the
desktop app formerly called Codex, running against local files) — *"regular Codex re-skinned to be less
intimidating to non-software-developers."* The post covers Work Cloud only. Paid tiers only ($20/month+).

**The harness inventory** — read this against [[agent-harness]]'s primitives list; it maps almost
one-to-one:

- **Code execution with internet access**, which he calls the most exciting feature: *"The code execution
  environment can now talk to the rest of the internet!"* Configurable domain allowlist, but *"the default
  appears to be open to all."* He contrasts Claude's container, which has had restricted access since
  Sept 2025 but where *"the allowlist of domains is very short"* (PyPI, npm, GitHub clones). **A harness capability difference,
  not a model difference.**
- **A full headless Chrome**: load pages, fill forms, screenshot, and run JavaScript against the DOM via
  Playwright. Sign-in is handed to the human — *"the browser can prompt you to take over and enter both
  passwords and 2FA codes, without round-tripping those credentials through the model itself"* — a
  credible credential-isolation pattern worth naming on its own.
- **A persistent filesystem shared between sessions**: per-session scratch folders under `/workspace`
  that survive and are visible across concurrently running sessions (*"I have 171 folders in
  /workspace/scratch right now!"*), though not a shared process space. This is the filesystem primitive
  that [[agent-harness]] calls the most foundational, in its cross-session form.
- **Subagents** (Sol/Luna/Terra), with `Ultra` described as *"a special mode that more eagerly delegates
  to sub-agents"* — his understanding from Codex, not documentation.
- **ChatGPT Sites**: build *and deploy* stateful sites on Cloudflare Workers (D1/R2), private by default.
- **Scheduled prompt automations**, which he twice notes also work in plain Chat.

**The legibility finding, and the number to handle carefully.** Unable to get a tool list from the docs,
he prompted a Work session to build a site cataloguing its own tools, then its own skills. Result:
**223 registered tools** (6 of them his own MCPs via `datasette-mcp`) and **44 skills** — including
`control-browser`, `documents` (.docx), `imagegen`, `pdf`, `spreadsheets`, `sites-sites-building`,
`openai-docs`, `data-analytics:build-dashboard`. **These counts are a MODEL SELF-REPORT, not
documentation** — the agent describing its own context and tool registry, at Willison's prompting, with no
vendor confirmation. Cite them as "the agent reported 223 tools and 44 skills," never as an OpenAI figure.
The same caveat applies to the `control-browser` skill text he extracted.

His diagnosis is explicit and is the durable claim:

> "1. OpenAI explain Work in terms of what it's for, not what it actually does. 2. OpenAI still insist on
> hiding their system prompts and tools descriptions. **If the ChatGPT Work documentation included the
> exact system prompt and tool descriptions used by the agent I wouldn't have needed to write this post.**"

**The safety point — his own [[willison-lethal-trifecta|lethal trifecta]], fully assembled.** Private data
+ exposure to untrusted content + an exfiltration channel: *"ChatGPT Work combines all three!"* He has no
answer on mitigation and asks for one, guessing it is the same auto-review mechanism as Codex. Note the
compounding factors: an internet-open execution sandbox, a real browser that visits arbitrary sites, and a
filesystem **shared across concurrently running sessions** — so a [[prompt-injection]] in one session has a
persistent, cross-session write surface. The capture states the trifecta; the cross-session amplification
is a reading of what he describes, and it is the sharpest open risk in this batch.

## Limits

- **A practitioner's reconstruction, not documentation.** Its central factual content is what one user
  inferred and what the agent said about itself; he flags several points as guesses (*"I'm assuming
  Sol?"*, *"my current understanding"*, *"as far as I can tell"*, *"I believe"*).
- **Product state is date-stamped and moving** — *"furiously iterating,"* with two mid-post updates
  correcting his own claims. Everything here is a 2026-08-30 snapshot.
- **No performance or efficacy claim is made or tested.** This is a capability inventory, not evidence
  that any of it works well.
- The tool/skill counts are self-reported by the agent (above) and were not cross-checked.

## Connections / contrast

- **Pairs with [[willison-claudes-new-system-prompt]]** into the batch's second durable structural claim:
  **the harness layer you rent is not disclosed, and interrogating the agent is the only available
  instrument.** Anthropic publishes a core consumer prompt but not the per-feature blocks and not Claude
  Code's; OpenAI publishes neither. Same finding, both vendors, one week apart.
- **Pairs with [[willison-codex-bundles-libreoffice]]**, which is the same harness seen from the disk:
  1.7GB of bundled Python, Node, Poppler, git and headless LibreOffice, with skills that tell the agent
  where they are. Together: **a commercial harness is an environment plus a skill catalogue**, and most of
  it is undocumented.
- **Against [[openai-harness-engineering-codex]]**, OpenAI's own harness-engineering case study: there the
  harness was legible repo artifacts the team owned; here it is a rented, hidden runtime. The KB's
  [[harness-engineering]] guidance implicitly assumes the former.
- Extends [[willison-lethal-trifecta]] with the first KB example of a mainstream consumer product shipping
  all three legs by default, and is directly relevant to [[agent-governance]] (what you can even audit)
  and [[unattended-coding-agents]] (scheduled prompts + subagents + open network).
- The 44 skills are a large-scale instance of the **Skills primitive** tracked on
  [[harness-engineering]] and in [[miller-jasperfx-ai-skills-agent-skills]] — one vendor shipping skills
  for its own runtime, another for its own libraries.

## Related

[[agent-harness]] · [[harness-engineering]] · [[prompt-injection]] · [[willison-lethal-trifecta]] ·
[[agent-legibility]] · [[openai]] · [[simon-willison]] · [[willison-claudes-new-system-prompt]] ·
[[willison-codex-bundles-libreoffice]] · [[agent-governance]] · [[model-context-protocol]] ·
[[unattended-coding-agents]] · [[long-running-agents]]
