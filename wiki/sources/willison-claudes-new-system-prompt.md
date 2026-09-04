---
title: "Source: Willison — Claude's new system prompt (and the layers that aren't published)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [willison-claudes-new-system-prompt]
raw_file: [raw/articles/willison-claudes-new-system-prompt.md]
tags: [agent-harness, agent-legibility, harness-engineering, system-prompts, anthropic, focus]
---

# Source: Willison — Claude's new system prompt (and the layers that aren't published)

Post by **[[simon-willison]]**, 2026-09-02. Raw capture:
`raw/articles/willison-claudes-new-system-prompt.md`. Ostensibly a diff-read of the Claude Fable 5.1
consumer system prompt against Fable 5's; the on-thread finding is **structural, and it is not about the
model**.

## Summary

[[anthropic]] publishes system prompts for its consumer apps (claude.ai and mobile) — *"sadly not for
Claude Cowork or Claude Code"* — with historic revisions, now re-arranged into an index plus a page per
model, each fetchable as Markdown by appending `.md`. Willison built
[`simonw/claude-system-prompts`](https://github.com/simonw/claude-system-prompts): each model family gets
one file with a **synthesized, back-dated commit history**, so prompt revisions are diffable in the GitHub
UI, with a daily GitHub Actions job and LLM-written change summaries. The content changes he finds are
mostly copyright and tone policy. The durable point is the last one he reaches: **a published "system
prompt" is only one layer of the real harness.**

## Key points

**The structural finding.** The `end_conversation` tool disappeared from the published prompt, but the
model still described detailed rules for it. Asked where they came from, Fable 5.1 answered:

> "The end_conversation section comes from a different layer. In my actual context, the core prompt is
> followed by a series of **feature- and tool-specific blocks** that get added depending on what's enabled
> for the session: the end_conversation rules, memory system notes, past-chats tools, web search and
> citation guidelines, artifact and file-creation instructions, and so on. **Those blocks aren't part of
> the published core prompt**, which is why you can't find them on that page."

Willison's conclusion: *"So, once again, there are crucial portions of the system prompt that have not been
published."*

**Carry this claim with its provenance: it is a MODEL SELF-REPORT, NOT DOCUMENTATION.** The evidence that
unpublished per-feature blocks exist is *a model describing its own context window* — exactly the class of
claim the KB elsewhere refuses to treat as measurement. It is plausible, it is consistent with the
published prompt's gaps, and Willison presents it as the model's account. It is not an Anthropic
statement, and no page should render it as one. (Compare the same shape in
[[willison-understanding-chatgpt-work]], where a ChatGPT Work session enumerated its own 223 tools and 44
skills — same method, same epistemic status, different vendor.)

**Why it matters for [[agent-harness]] and [[agent-legibility]].** If a vendor's *published* prompt is the
core layer only, then:

- **"Read the system prompt" is not a route to knowing the harness.** The composition — which blocks load
  under which enabled features — is the thing that determines behaviour, and it is unpublished and
  session-dependent.
- **Prompt archaeology has a floor.** Willison's diff pipeline is the most careful public instrument for
  tracking these artifacts, and it can only see the layer that is published. The observable surface is a
  vendor choice, not a property of the system.
- **It is a legibility asymmetry the KB should state plainly:** harnesses are engineered in layers, and
  the layer visible from outside is chosen by the vendor.

**Secondary observations worth keeping** (content, not structure): the new prompt refuses song lyrics,
poems and book passages "in whole or in part," and keeps refusing reworded requests for the rest of the
conversation, with a pre-1929 exception judged on the model's own knowledge of the work's date — added,
Willison notes, *"within days of the news breaking that Sony Music Publishing and Warner Chappell are
suing Anthropic."* A parallel block forbids drawing copyrighted characters "at all," judged by *"what the
finished picture would add up to, not by what it names,"* with a worked axolotl example. Style tweaks
instruct brevity and ban the words "genuinely", "honestly", "straightforward". The `end_conversation`
escalation was replaced with "accountability without self-abasement." And the prompt now carries the
model's **reliable knowledge cutoff (end of June 2026)** together with the only `{{currentDateTime}}`
macro, placed near the end — *"which makes sense from a caching perspective."*

**One methodological detail worth borrowing.** Willison had GPT-5.6 Luna, not Claude, summarize the Claude
prompt diffs: *"mainly because I don't trust Claude to summarize its own system prompts when there's a
risk that material from its system prompt might impact its opinions."* A deliberate
**check-external-to-the-thing-checked** choice, and the same principle as
[[bockeler-tdd-inside-the-agent-loop]]'s finding that a self-confirmed red test proves nothing.

## Limits

- **The load-bearing claim is the model's, not the vendor's** (see above). No independent confirmation of
  the unpublished blocks exists in this capture.
- Everything here concerns **consumer chat apps**, not the coding harnesses the KB mostly cares about —
  and Willison notes Claude Code and Cowork prompts are *not* published at all, so the agentic surface is
  less legible than the consumer one.
- Content-change readings (lawsuit timing, "maybe Fable is good enough at SVGs now") are Willison's
  speculation, and he says so.
- The whole tracking system was **built by Fable 5.1** (*"wrote every line of automation code and almost
  all of the documentation"*), which is a datum for [[agentic-coding]] but also means the instrument is
  itself agent-authored.

## Connections / contrast

- **Pairs with [[willison-understanding-chatgpt-work]] into one claim the KB can state as a pattern:**
  neither major vendor publishes the full harness, and the only route in is to interrogate the agent about
  itself. Willison says it directly of OpenAI — *"OpenAI still insist on hiding their system prompts and
  tools descriptions"* — and finds it true of Anthropic's agentic products too.
- **Contrast with [[openai-harness-engineering-codex]] and [[hashimoto-my-ai-adoption-journey]]**, where
  the harness is the practitioner's *own* repo artifacts (AGENTS.md, linters, scripts) and therefore fully
  legible. The lesson: harness legibility is high for the layer you build and low for the layer you rent.
- Relevant to [[claude-agent-sdk]] and [[context-engineering]]: what loads into context per session is
  the mechanism, and here it is not disclosed.

## Related

[[agent-harness]] · [[agent-legibility]] · [[harness-engineering]] · [[anthropic]] ·
[[simon-willison]] · [[willison-understanding-chatgpt-work]] · [[context-engineering]] ·
[[claude-agent-sdk]] · [[bockeler-tdd-inside-the-agent-loop]] · [[agent-explainability]]
