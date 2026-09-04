---
title: "Willison — Just a rumour of a bug is enough to find a security exploit these days"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [willison-just-a-rumour-of-a-bug]
raw_file: [raw/articles/willison-just-a-rumour-of-a-bug.md]
tags: [agent-safety, security, coding-agents, autonomy, open-source, focus]
---

# Willison — Just a rumour of a bug is enough to find a security exploit these days

Blogmark by **[[simon-willison]]**, 2026-08-28, relaying **Anil Madhavapeddy** (professor at Cambridge,
core OCaml compiler maintainer). Raw capture: `raw/articles/willison-just-a-rumour-of-a-bug.md`.
**Secondhand** — the primary at anil.recoil.org was not fetched.

## The observation

Security issues in OCaml projects are drawing attempted exploits **within minutes** of a patch being
shared for discussion:

> "This normally takes a few days and a release within a week or two is reasonable. Within about ten
> minutes (!) this website was fielding probes for percent-encoded traversal sequences, indicating that
> automated watchers are keeping an eye on public repositories."

Willison's summary of the mechanism: *"Modern coding agents have become so effective at finding flaws
that the slightest hint at a new bug can be enough information for them to find it"* — Madhavapeddy
demonstrated it with his own agents, **switching to DeepSeek V4 Pro when Claude Fable refused the task**.
That detail is worth keeping: refusal is a per-model property, not a property of the capability, so a
safety posture that depends on one vendor declining is not a control.

## Independent corroboration, with numbers

Nick Craig-Wood, rclone maintainer, in the HN thread:

> "In the first 10 years of the rclone project we received about 20 security disclosures through GitHub.
> We had to deal with over 40 in the last month!… The hit rate for those security disclosures is pretty
> good - about 75% of them have a nugget of something which needs looking at."

Roughly a **240× increase in disclosure rate** against a 75% signal rate — so this is not simply noise.
The second-order effect is process collapse elsewhere: GitHub CVE assignment has gone from 2–3 days to
3–4 weeks, forcing point releases to ship with `CVE-PENDING` in the changelog.

## Why it matters here

- **It is the *capability* bound** on unattended operation — the third of the KB's three independent
  limits alongside *exposure* ([[willison-breaking-claude-code-auto-mode]]) and *degradation*
  ([[token-budget-quality-cliff]]). Its shape is different from the other two: those bound what your own
  agent can safely do, this one bounds what *other people's* agents do to you. See
  [[unattended-coding-agents]].
- **It breaks a process, not a system.** Madhavapeddy's point is that the discovery rate "appears
  incompatible with existing open source embargo practices" — a coordination norm built for
  human-timescale disclosure. Nothing else in this KB addresses the organisational consequences of agent
  capability at this end.
- It is a rare case in this KB of a **capability improvement being straightforwardly bad news** for the
  people affected, which is a useful counterweight to the harness/loop threads' framing of capability as
  the thing to maximise.

## Caveats

- **Secondhand twice over**: Willison relaying Madhavapeddy, plus an HN comment. The primary is
  uncaptured.
- Two projects (OCaml, rclone), both open-source infrastructure with public patch discussion — the most
  exposed possible setting. Generalisation to private codebases is not established.
- The 240× figure is my arithmetic on Craig-Wood's numbers (≈20 in 10 years vs 40 in one month), not his.

## Related

[[unattended-coding-agents]] · [[willison-breaking-claude-code-auto-mode]] ·
[[token-budget-quality-cliff]] · [[agent-governance]] · [[simon-willison]] · [[prompt-injection]] ·
[[agentic-coding]]
