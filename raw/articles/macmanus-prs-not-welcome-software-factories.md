---
source_url: https://www.latent.space/p/pr-not-welcome
title: "PRs NOT Welcome: How Top AI Open Source Projects Are Managing Thousands of Contributors"
author: Richard MacManus
publication: Latent.Space
published: 2026-09-01
retrieved: 2026-09-03
type: article
---

# PRs NOT Welcome: How Top AI Open Source Projects Are Managing Thousands of Contributors

### Vercel's AI SDK, Astro, Flue and tldraw are replacing drive-by community PRs with software factories, where teams of agents apply fixes and features.

Richard MacManus — Sep 01, 2026

GitHub invented pull requests, and for 18 years they have been open by default. **But now some of the top AI-native open source projects are shutting PRs off**, because they've found a better way.

These projects, which include Flue and tldraw, **refuse to accept PRs from external contributors** — in part because they're usually AI-generated. Instead, the maintainers prefer to **use their own agents** to create and manage PRs.

Also, many projects have begun **using a "[software factory](https://www.latent.space/p/software-factories)" to manage community contributions.** Typically this involves a 'team' of agents triaging a PR, reproducing the issue (if it's a bug), implementing a fix or a new feature, reviewing it, and then handing it back to a human to merge it.

## Vercel's software factory for AI SDK

Vercel recently published a post entitled "[Building a software factory for AI SDK](https://vercel.com/blog/building-a-software-factory-for-ai-sdk)." It describes how the open source AI SDK project, which gets over 20 million npm downloads per week, **deployed agents to get control over its PR and issue backlog** — which had reached "over 1,000 open issues and almost 800 pull requests" by late June.

There are several types of agents in Vercel's system, **each of which focuses on a different task**. For example, there's an agent that reproduces a bug, another that applies a fix, and yet another that reviews the fix.

*[Diagram from Vercel; comments by Latent Space]*

One of the key reasons why Vercel set up this software factory is because **it trusts its own agents to do the work**, more so than agents run by community members.

"If we have a very specific agent with a very specific prompt that we optimized — and we know that, over history, it was very successful in fixing a certain category of bugs — then **we develop trust in that particular agent configuration,"** Vercel engineer **[Lars Grammel](https://x.com/lgrammel)** explained in [a YouTube video](https://www.youtube.com/watch?v=wnydmnIYo1Y).

"For open-source projects, it's worth considering having your own agents and your own setup, and **not necessarily trusting the community**, because it can actually cut down your time to review," he added.

*[Example of software factory workflow in AI SDK project.]*

Grammel also showed the **deployment architecture** for its system, noting that "there is a UI, there's a web app, there's an underlying API, there's an execution space, and there are sandboxes." It's then synchronized with GitHub, which automatically triggers other actions. The UI Grammel mentioned was custom-made.

*[Vercel's software factory deployment architecture; diagram by Lars Grammel.]*

Just four weeks after this software factory was implemented, [Vercel claims](https://vercel.com/blog/building-a-software-factory-for-ai-sdk) the factory now "**authors between 25 and 35% of PRs we merge** and **closes 70-80% of issues**."

## Astro's auto-triage system

The [Astro web framework](https://github.com/withastro/astro), which has 62,000 stars on GitHub, has also adopted what creator **[Fred Schott](https://x.com/FredKSchott)** calls "that software factory idea."

"For five years, we were in this place where **issues came in faster than we could handle them**," Schott told Latent Space.

But now, **with agents handling the triage work, they've reestablished control.**

"It's totally shifted in the last six months," he said. "We can now solve these issues with these automations — handling triage, reproduction, getting the user to actually verify the fix that the bot is suggesting **before we even look at it.**"

*[Example of an Astro factory bot in action]*

The result was not just a large decrease in open issues, but a complete change in how the Astro team deals with incoming community requests.

**"I've never seen that in my entire decade-plus experience with open source,"** Schott said. "Being able to essentially treat issues as a thing that every week, you prioritize — no matter what — versus a backlog that you're constantly trimming."

Furthermore, the Astro "auto-triage" system directly led to Schott creating [a brand new agent framework, called Flue](https://www.latent.space/p/flue-2).

## Flue doesn't accept your PRs, but is open for discussion

With Flue, Schott is trying an even more radical approach to PRs. [Flue's contributor guide](https://github.com/withastro/flue?tab=contributing-ov-file) states that "we're going to try to reimagine things" — partly to prevent what it calls **"Drive-by AI slop PRs."**

Basically, Schott explained, **every external pull request in the Flue project is automatically closed and converted into an issue or discussion.** Bug reports and fix proposals get turned into issues, feature requests become discussions.

*[Agents can do most PR tasks now, according to Flue's contributor guide.]*

"If you submit a PR, no hard feelings, we're just going to go and represent it for you as issues and discussions. And from there, trying to figure out the right way to bring people on."

It's kind of like **treating incoming requests as** ***leads***, rather than as a piece of work a maintainer feels obliged to review. The contributor guide explains that it uses the team's own expertise combined with **"the best available SOTA [State-of-the-Art] LLMs that we have access to"** in order to help them decide what to work on next.

Once a decision is made in the issue or discussion, agents are then deployed for "research, design, implementation, and initial review."

## If our agents write the code, your external PRs are worthless

Like Flue, the "source available" React drawing tool [tldraw](https://github.com/tldraw/tldraw) (50,000 stars) **automatically closes external PRs**.

Project creator Steve Ruiz announced this policy [in January](https://github.com/tldraw/tldraw/issues/7695) and five months later [reiterated it](https://github.com/tldraw/tldraw/issues/9422), noting that it was "an opinionated decision made in response to changes in how we're coding (more discussion, more agents), the social practices around public contribution, and the changing landscape around code security."

> Steve Ruiz @steveruizok: "absurdity in my issues rn" — 4:04 PM · Jun 6, 2026

HashiCorp co-founder and Ghostty creator Mitchell Hashimoto, now a [co-founder of Superlogical](https://mitchellh.com/writing/superlogical), takes it even further. [He thinks](https://x.com/mitchellh/status/2064361174196682789) "the future is that **large open source projects will close contributions completely."**

[Ruiz responded](https://x.com/steveruizok/status/2064381300572672450), "It just makes less sense to have people contributing code if the issue is decently well-specified and the code can be written by agents."

## But…what happens to the community?

Traditionally in open source, pull requests have been reviewed by maintainers not only for the code, **but to teach contributors and assess them as future maintainers.** If projects like AI SDK and Astro are using their agents to do much of the code review and implementation, where does that leave community members who want to be more actively involved?

Schott recognizes this as a risk.

"It still leaves this open hole of, well, if you just keep narrowing the project, at a certain point, you and I go on vacation — what happens? It doesn't really solve every problem."

However, the fact that both Flue and tldraw don't accept PRs **but do accept new issues and discussions** perhaps points to a solution. Which is that by talking to each other more, community members better get to know — and trust — one another, which is both a way to **learn from peers** and potentially **prove yourself worthy of being a maintainer**.

*[Example of a tldraw issue being turned into a PR]*

As for the code, if it's easier for maintainers to use AI themselves than to accept external code contributions, then as tldraw founder [Steve Ruiz put it](https://tldraw.dev/blog/stay-away-from-my-trash), **"it's better to limit community contribution to the places it still matters: reporting, discussion, perspective, and care."**

---

*Capture notes (not the author's words): (1) The "25–35% of merged PRs / 70–80% of issues closed" figures are **Vercel's own claim about its own project**, reported second-hand by Latent.Space — vendor self-report, unaudited. (2) Fred Schott's "totally shifted in the last six months" and "never seen that in my decade-plus" are **practitioner impressions, not measurements**. (3) Latent.Space is a paywalled Substack; this post rendered in full to an unauthenticated fetch on 2026-09-03. The linked "Software Factories" and "Flue 2" Latent.Space pieces are not yet in `raw/`.*
