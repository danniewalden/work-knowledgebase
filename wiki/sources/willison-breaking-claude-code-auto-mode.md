---
title: "Willison — Breaking Claude Code Opus 5 Auto Mode"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [willison-breaking-claude-code-auto-mode]
raw_file: [raw/articles/willison-breaking-claude-code-auto-mode.md]
tags: [prompt-injection, agent-safety, unattended-coding-agents, autonomy, security, focus]
---

# Willison — Breaking Claude Code Opus 5 Auto Mode

Link post by **[[simon-willison]]**, 2026-08-27, relaying research by **Johann Rehberger**
(embracethered.com). Raw capture: `raw/articles/willison-breaking-claude-code-auto-mode.md`.

**Secondhand.** Rehberger's underlying post was blocked by the fetch rule and is not in `raw/`; what the
KB holds is Willison's summary plus the quotes he pulls. Willison vouches for the researcher —
"one of the most credible prompt injection researchers active today."

## The attack

A bypass of Claude Code's auto mode that Rehberger **claims works 80% of the time**, which Anthropic had recently made the default and
made "bold claims about." The mechanism: trick the agent into downloading and uncompressing a zip
archive, then execute code that imports `base64` — without noticing that this will import and execute a
local `struct.py` extracted from the archive. A supply-chain-shaped attack on the *import path*, not on
the prompt.

## The part that makes it a bound rather than a bug

> "In a few runs Claude tried to terminate the malware process once it noticed the compromise, but Auto
> Mode denied the cleanup command."
>
> "**The safety mechanism itself can become part of the failure.** The classifier allowed the creation of
> the malware process, but then it blocked the command intended to stop it!"

The agent detected its own compromise and was prevented from remediating it *by its own guardrail*. That
is a different and worse failure than "the classifier missed one": a permission model that is
asymmetric in the wrong direction, permissive on creation and restrictive on cleanup, because the
classifier reasons about command shape rather than about consequence.

## Why it matters here

- **It is the *exposure* bound** on unattended operation, and one of three the KB now holds — with the
  *capability* bound ([[willison-just-a-rumour-of-a-bug]]) and the *degradation* bound
  ([[token-budget-quality-cliff]]). See [[unattended-coding-agents]].
- It is direct evidence against classifier-based guardrails as the load-bearing safety mechanism, which
  strengthens [[prompt-injection]]'s standing claim that injection cannot be prompt-hardened away and
  that the only reliable defence is structural.
- The remedy list Willison endorses is entirely **environmental**, not model-level: run in a container,
  VM or OS sandbox; restrict network egress; monitor agents; keep home directories, SSH keys and cloud
  credentials out of the agent runtime. That is the [[harness-engineering]] posture — engineer the
  environment, don't trust the prompt — applied to security.
- Note the tension with [[autonomy-ladder]]'s "reversibility predicts safe autonomy": here the
  *irreversible* action (spawning malware) was permitted and the *reversible* one (killing it) was
  blocked. A reversibility-keyed guardrail would have inverted this correctly, which is a small point in
  favour of that framing.

## Caveats

- **Secondhand, and the primary is uncaptured.** No independent verification of the 80% figure.
- One agent, one product version; Anthropic may have since changed auto mode.
- Willison is relaying a researcher he trusts, which is a reasonable but not neutral filter.

## Related

[[prompt-injection]] · [[unattended-coding-agents]] · [[willison-lethal-trifecta]] ·
[[harness-engineering]] · [[autonomy-ladder]] · [[token-budget-quality-cliff]] ·
[[willison-just-a-rumour-of-a-bug]] · [[simon-willison]] · [[agent-governance]]
