---
source_url: https://simonwillison.net/2026/Sep/2/rick-brewster/
title: A quote from Rick Brewster (Paint.NET's clean-room Direct2D rewrite)
author: Simon Willison (quoting Rick Brewster)
publication: Simon Willison's Weblog
published: 2026-09-02
retrieved: 2026-09-03
type: article
---

# Quotation post — Simon Willison's Weblog, Wednesday 2nd September 2026

> Direct2D has always been the biggest hurdle for Paint.NET on WINE, and it's clear that it will never be completed enough for Paint.NET's use. And I can't just "disable" the use of Direct2D. So, instead, **Paint.NET now has an internal, from-scratch, clean-room reverse-engineered rewrite of Direct2D that it uses on WINE** (triggered by using **/wine**). It lives in **PaintDotNet.Windows.Direct2D1.Managed.dll**. This was written by our good friend [Claude](https://claude.ai/), without whom this would NOT have been possible and would NEVER have happened. [...]
>
> Most of this code is, as they say, "vibe coded." By that I mean that it has not been thoroughly reviewed, it's more "trust me bro" style. I cannot possibly review 180,000 lines of code, it's just way way *way* too much. For reference, the rest of Paint.NET is about 700,000 lines of code and I've been working on it for over 20 years. [...]
>
> At times, Claude was working with the fury of 10 freshly unshackled Einstein genius-level 10x coders. And other times ... well, not so much. I had to babysit Claude quite a bit to make sure it did resource management correctly (for awhile it just wasn't doing the COM equivalent of AddRef() for reference counted objects, oops). I had to slap it a few times when I found some really bad design or architecture decisions. And I was also impressed at some rather clever and tireless reverse engineering work it did to figure out all the formulas needed for implementing Direct2D's built-in effects library.

— [Rick Brewster](https://forums.paint.net/topic/134563-extremely-experimental-winelinux-support-how-to-get-started/), author of Paint.NET

Posted 5:50 am, 2nd September 2026 / tags: dotnet, linux, reverse-engineering, ai, generative-ai, llms, claude, vibe-coding, coding-agents

---

*Capture notes (not the author's words): (1) This is a **quotation post** — Willison's contribution is the selection and framing; the words quoted are Rick Brewster's, from a Paint.NET forum thread. (2) Brewster's account is a **practitioner self-report on his own project**, not a measurement: the line counts are his, and "it has not been thoroughly reviewed" is stated by the author of the unreviewed code. (3) Captured because it is an unusually blunt primary datum on the verification-burden / comprehension-debt strand — a maintainer of a 20-year, 700k-line codebase stating plainly that 180k agent-written lines are past the point where review is possible at all. Also in the same day's archive but NOT captured: Willison's 2,270-word entry "Claude's new system prompt really doesn't want to reproduce song lyrics" (https://simonwillison.net/2026/Sep/2/claudes-new-system-prompt/), judged off-thread (content policy, not harness/agent design).*
