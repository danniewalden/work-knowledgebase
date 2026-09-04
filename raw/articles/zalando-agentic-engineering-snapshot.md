---
source_url: https://engineering.zalando.com/posts/2026/08/agentic-engineering-at-zalando-a-snapshot.html
title: "Agentic Engineering at Zalando: a snapshot"
author: Bartosz Ocytko (Executive Principal Engineer, Zalando SE)
publication: Zalando Engineering Blog
published: 2026-08-14
retrieved: 2026-08-29
type: article
---

# Agentic Engineering at Zalando: a snapshot

*We look back at our journey of agentic engineering at Zalando, sharing our learnings and approaches that worked well for us in the past 2.5 years.*

Tags: Artificial Intelligence, Culture, LLM, Open Source, Machine Learning

While the landscape and environment rapidly changes every day, the whole industry is figuring out how to approach Agentic Engineering. With more than 250 engineering teams innovating across our business lines, we're observing value and impact of LLMs in different forms and at different paces. We shared some early wins on using LLMs for [product data enrichments](https://engineering.zalando.com/posts/2024/09/content-creation-copilot-ai-assited-product-onboarding.html), LLM as a judge for [improving search quality](https://engineering.zalando.com/posts/2026/03/search-quality-assurance-with-llm-judge.html), [relevance assessment in product search](https://engineering.zalando.com/posts/2024/11/llm-as-a-judge-relevance-assessment-paper-announcement.html), or [frontend migrations](https://engineering.zalando.com/posts/2025/02/llm-migration-ui-component-libraries.html).

Recently, we have been looking back at our progress in the past 2.5 years and we'd like to share a few approaches that worked well for us.

## LLM proxy for API-based LLM access from day 1

We've been a GitHub Copilot user from the early days when it offered autocomplete in the IDE. To complement this offering and provide API-based access to LLMs, our ML platform team deployed in January 2024 a [LiteLLM](http://docs.litellm.ai/) based API proxy with access to models from different providers (now: OpenAI, AWS Bedrock, and Google Vertex). This way, it became easy for our engineers to experiment with different tools and models. The platform team got a single point to measure adoption via: MAU, WAU, model, User-Agent.

We like LiteLLM for its extensibility. We use post-call hooks for anonymized cost tracking and [pre-call hooks](https://docs.litellm.ai/docs/proxy/call_hooks) for enforcing client version upgrades by restricting access to the proxy based on the User-Agent header. For self-managed client installations, unfortunately blocking access is the only effective measure. Same goes for retiring models. There is always a long-tail group of users who do not adjust their local configurations and who do not follow new model releases. We also enabled [auto-injection](https://docs.litellm.ai/docs/tutorials/prompt_caching) of prompt caching checkpoints, which reduced costs for custom agents while their authors still learn about prompt caching. To mitigate stability and memory leak issues of LiteLLM, we enforce restarts after 20k requests using `--max_requests_before_restart`. This enables us to run the proxy for 2k MAU with just six small (2 CPU cores, 4 GB memory) pods. We look forward to the Rust rewrite that's expected to improve performance and stability.

### Beyond the API: Chat UI and CLI

The API offering is complemented with a simple chat UI (fork of a now unmaintained OSS codebase) and a CLI tool (custom-built using pydantic-ai). To our surprise, the Chat UI still has a high adoption rate even though IDE plugins and CLIs are ubiquitous these days and users have many more capable alternatives to choose from. The CLI was incepted in a hackathon (Aug 2024) in times where coding agents did not exist yet. Initially, we used it in maintenance scripts for model access in the terminal. Over time, the repository attracted a small community of maintainers who extended it with additional tools helping us scale adoption of LLMs for coding tasks:

- generating images with simple file format conversion
- an interactive mode for multi-turn chats, supported by simple commands to load and save files for context management
- agent mode with MCP support and automatic Bearer token injection for internally hosted MCP servers
- http to stdio MCP proxy to make internally built MCP servers easy to access in any other tool
- built-in MCP server configuration, enabling first-time MCP users to experiment easily without much friction
- coding agent configuration command which installs safe configurations for claude code, opencode, pi along with custom plugins for model autodiscovery

The token injection and MCP proxy helped us to promote safe configuration of MCP servers where no secrets need to be hardcoded in configuration files. It allowed to spread the use of internally-deployed MCP servers without needing to deal with any auth concerns. This is especially important as the user base of the LLM access expands beyond engineering, with varying intuition for security. Deployed MCP servers, hosted by teams, are automatically protected by our default ingress oauth filter.

### Challenges with LLM-enabled tooling

Two classic problems are consistent across different tools. Too often, tools use a generic User-Agent header, making it difficult to identify the tools used as clients of the proxy. For our own LLM applications, such as custom code review agents, we ensure to include a name and originating repository and version as part of the User-Agent header. For other tools, we request changes upstream (or contribute).

Second, tools lack support for custom auth commands for auth token generation, supporting only static credentials or defaulting to support subscription offerings. Reliance on environment variables causes user frustration as tokens expire and need to be refreshed manually which involves restarting the applications. To bridge this gap, we have a local proxy that injects auth headers and write plugins for coding agents that handle model access and model discovery along with their parameters. The proxy evolved to include features helping live debug LLM tools of our own making. It ships with a TUI that displays current costs per model, highlights gaps in usage of cached tokens, and displays the per request metadata (User-Agent, model, costs, token statistics incl. cache write/read). Future adjustments include adding tips for better usage of prompt caching (inspired by pi's `showCacheMissNotices`) through analysis of outgoing requests.

## Vendor independence

Vendor independence is key in a fast-moving environment. Our proxy provides us with ability to onboard additional LLM providers and our users pick a tool that vibes best with them. We have never centrally mandated the use of a single tool. Users make choices for tools, based on available models and their own preferences (IDE vs. CLI). Natural progression from chat-based interactions to agentic loops orchestrated through CLIs or Desktop UIs further drives tool switches.

For some users, [opencode](https://opencode.ai/) and [pi](https://pi.dev/) offer a sweet-spot as they allow mixing models between Github Copilot subscription and our API-based access. This move to open tools is likely to progress further as moving off closed-weight models requires switching to open tools. However, we see users becoming too attached to the coding agent they had been using for a while. Model preference also makes a difference with users preferring the style of answers from model provider X over Y. The hesitance to switch tools on psychological level exists despite the rather low switching costs between the tools as capabilities of the tools are largely similar to one another.

We maintain reference configurations for the different coding agents and plugins for model providers. While we explore Device Management for developer tooling (we never had the need for it before), configuration for tools can be applied with a special command in our CLI tool which reads the latest configuration state from a git repository.

## Identifying the impact of AI coding

### PRs and code reviews

We see impact of AI coding in our PR data since two years. In addition to a consistent increase in PR sizes of \([100,500)\) we also see growth in the higher buckets since Sonnet 4 release in Q2/2025, esp. \([500,1k)\) and \([1k,2k)\).

*[Figure: PR size distribution (quarterly)]*

Teams who found large PRs to be a problem, have reached internal agreements that they will limit PR sizes to a fixed size. Hard enforcement through pre-commit hooks is less popular. Other teams are used to larger PRs and instead of relying on meticulously crafted commit sequences, now rely on goodies provided by tooling we use, such as semantic grouping of changes in Github PRs or Linear Reviews.

### Impact on code complexity

We also see impact of AI coding in the codebases themselves, with good and bad practices being amplified. Looking at commit-level evolution of code quality metrics in Java and Golang codebases, we mapped each commit to a few metrics and plotted their evolution over time. We used four codebases:

| Codebase           | Language | Age  | Agent Adoption    | Notes                                                  |
| ------------------ | -------- | ---- | ----------------- | ------------------------------------------------------ |
| `go-agentic-only`  | Go       | New  | Full from start   | Built with spec-driven development from day0           |
| `go-reference`     | Go       | 10y+ | From commit >3000 | OSS codebase                                           |
| `java-with-agents` | Java     | 4y   | From commit >1600 | Gradual adoption of coding agents                      |
| `java-reference`   | Java     | 12y+ | None              | Macroservice with code extracted to other repositories |

Looking at the total cyclomatic complexity evolution on a per commit level, we can pinpoint inflection points in code complexity at a time when coding agents come into the picture. Some codebases carry markers (Co-authored-by) that confirm these inflection points; others (esp. OSS) have less consistency in these as not all authors disclose usage of coding agents.

For codebases that started with full use of agentic coding, we see complexity to build up very quickly with growth fading out. If code complexity is expected to plateau for a well-scoped microservice, one would hope this means that the time to build has been drastically reduced. Time will show whether this is the case. You can also see complexity dropping in the graph, following a refactoring in one of the codebases.

*[Figure: Total CCN (Cyclomatic Complexity Number) across codebases]*

Notably, even commit messages carry the footprint of coding agents, typically around the 5k character mark. In one extreme case, we found a commit message to include a full log of unit test execution. If easy to get unnoticed in code reviews, this is a good constraint to add in pre-commit hooks.

*[Figure: Commit message size distribution across codebases]*

## Risk-based PR approval

In the pursuit of protecting lead time to merge for PRs, we built a risk-based PR approval tool, triggered at PR creation stage. Each PR is evaluated for its rollout risk: low, medium, high. 33% of our PRs are low-risk and are auto-approved by the bot. The author of the PR can thus choose to merge the PR, which in our case reduced PR lead time by 20-40% (when compared with all PRs). It also greatly accelerated individuals building prototypes or taking care of internal tooling who would have otherwise needed to interrupt one of their colleagues to rubberstamp their changes.

The rule set for the approval bot is built based on analysis of our production incidents and the typical drivers for outages. The rules are highly specific to our tech stack, deployment manifests, configuration files, etc. Typos that break configuration are assessed as high risk (would have saved us from the [metadpata incident](https://engineering.zalando.com/posts/2024/01/tale-of-metadpata-the-revenge-of-the-supertools.html)). Breaking backwards-compatibility is medium risk and requires judgement from another human to double-check the business rationale. Documentation only changes are low risk.

Anecdotal evidence shows that the bot affects behavior of engineers to increase the probability of a low-risk PR. For example, PRs start to be broken down into those that can be shipped quickly (low risk) with backwards compatible-changes and less important medium-risk PRs dropping unused fields that require another approval. In the past, we observed such changes to be mixed together, increasing time to market and rollout risk.

## Learning from session data

Looking at session data from coding agents is highly educational. Aside from spotting non-essential traffic (e.g. generating plan names, terminal window titles, or recaps for idle sessions) that costs tokens, users can learn more about their own prompting patterns. We found [agentsview](https://www.agentsview.io/) useful to inspect session data across multiple tools and [codeburn](https://github.com/getagentseal/codeburn) to provide means to understand usage across projects / task types.

One insight from session data was a user with very low cache hit ratio for opencode (<30% vs. 80%+ expected). To help pinpoint the session with low cache hit ratio, we wrote a simple parser calculating cache hit ratio across sessions. Fortunately, it turned out not to be a systematic bug across our user base.

## Agent skills

We have a centralized agent skill collection grouped into plugins. These skills address common tasks or concerns across the organization across disciplines (e.g. data, engineering, frontend, sre) or programming languages. A widely popular type of skills are migration skills that guide teams in adopting new platform tools or infrastructure practices (e.g. multi-arch builds). The skill collection is distributed via managed configuration settings or cli command installing the needed symlinks (e.g. opencode does not support plugin marketplaces).

By encouraging broad contribution of skills that teams found useful, we got an opportunity to discover and disseminate best practices across the organization, related to validation of plugin syntax in CI/CD pipelines, separation of concerns between skills and scripts (e.g. where OAuth token generation belongs).

Teams building their own skills use the collection as a reference and inspiration for their own skills, for example copying the use of [agent-skills-eval](https://github.com/darkrishabh/agent-skills-eval).

## Governance

With >200 teams innovating and broadly exploring the ecosystem, the question arises whether and when to converge. We believe it's way too early for this. While agentic engineering practices are still in their early stages, our key objective is transparency and exchange across teams. We resort to structured knowledge sharing (more on that below) and proven governance methods to create transparency and promote cross-team sharing.

One such mechanism is our [Tech Radar](https://opensource.zalando.com/tech-radar/). Internally, we added an AI section, focused on providing overviews and entry points to key documentation on our offering, policies, and guidelines. In the past 10 years, library choices have been offloaded to our language communities of practice and out of scope for the Tech Radar. However, the cambrian explosion of AI tools and the rapid expansion of the ecosystem increased the need for clearer guidance on practices that are proven and those that are still early stage. We therefore see value in tracking practices, tools, and libraries for AI use cases. To increase transparency, the AI section of the radar has a separate entry point in our Backstage-based developer portal, called [Sunrise](https://engineering.zalando.com/posts/2023/08/sunrise-zalandos-developer-platform-based-on-backstage.html).

For early-stage projects we provide entry points for legal assessments on a per use-case basis to ensure compliance. Further, we auto-detect AI model usage through scanning of deployed Docker images. The system is auto-registered in our developer portal and the owners are asked to provide needed documentation or undergo an additional legal review.

## Knowledge sharing

Knowledge sharing needs to account for the pace at which things change in the ecosystem. When state of the art changes daily, early adopters have different needs for exchange than those early in the game. The closer we are to emerging best practices, a more standardized and scalable training format works best. We introduce the formats that worked for us for knowledge exchange and training in this section.

One thing to point out is the importance of finding balance. There are things happening in engineering besides AI that deserve attention. During our annual Software Engineering Community Conference, we ran the Agentic Engineering track on day 1 and to balance it out an Engineering Fundamentals track on day 2. Similarly, we plan to add a training on engineering excellence to teach about the hard lessons learned about operating systems at our scale and promote engineering best practices.

### LLM guild

Since 2024 we have a chat channel where we share and discuss industry news, announcements related to our LLM offering, and team up for experiments. We run 1h knowledge-sharing sessions weekly with 20-min slots for presentations or demos. Sessions are recorded.

The sessions have a moderator curating the agenda, encouraging individuals from their network to present, or issuing open calls for presentations in the chat. The format is great for early adopters who seek the most recent knowledge and experiment results from their peers across the company. The presentations are a great source of talent for hands-on support in projects, exploration of new approaches, and to expand our pool of internal trainers.

We also experiment with different formats for the weekly meetings. For example, we ran a session on agent skills where we promoted our company-wide agent skill marketplace by mapping the skills against our developer journey steps (idea, design, code, test, monitor, operate, maintain). First, we asked attendees to add examples of any team-level skills they had created which could complement our global collection. Next, we ran breakout rooms for each of the journey steps where the groups compiled opportunity statements for skills that do not exist yet.

### Guided Experimentation

Following the spirit of guided innovation, we had success with hackathons with ca. 10 topics chosen upfront by the organizing team. The topics include a defined goal, hints on what to consider, what's out of scope, and what potential synergies exist with other groups.

The topics are tackled in a 2-3 day hackathon (with open sign-ups) where groups of 4-6 people attempt to meet the stated objectives, respecting the set constraints. Scope and constraints can be negotiated with the facilitators during the event.

In the early days, such an approach allowed us to explore parallel paths and choose what tools to invest in. One of the topics explored in such format was building MCP servers following a template which seeded the initial set of community-maintained MCP servers at Zalando. Another group was explicitly asked not to look at MCP, but rather explore a generic approach for APIs: perform a search against our API definition catalogue and generate API calls based on the user prompt. This effort was successful and built up on our internal API catalogue, now also exposed as an MCP tool itself. It also highlighted gaps in API spec quality, for example missing hostnames making it impossible to generate working API calls.

We do also run business-unit scoped hackathons where teams form around business goals with aim for rapid prototyping, build out of agentic engineering skills, etc.

### From Labs to Trainings

We use a format we called *GenAI Labs* to share knowledge across the organization. Labs are on-site sessions for ca. 20 people, hosted by 1-2 trainers with a duration of 1-4 hours. After a short briefing session introducing the topic, attendees go through a set of exercises in pairs. In longer sessions, there is a break at half time for group sharing. For the very first session for a topic, we pre-assign attendees by their past experience with agentic engineering techniques, using a short sign-up form. This allows for time-efficient exploration: over the course of 3 days we can run 6 sessions with ca. 120-150 participants across multiple locations.

Lab sessions which we intend to host more often are converted into monthly trainings. The trainer pool is recruited from attendees of prior Lab sessions. Trainers improve content based on feedback from attendees. Our Tech Academy team responsible for internal trainings helps with the facilitation, looking after the attendee and trainer experience.

We run two sessions monthly: using MCP servers and building agents with pydantic-ai. The first helps onboard everyone to the concept of MCP and promotes our internal set of MCP servers. The second explains basic concepts about tool calling and agent loops, providing attendees with foundational understanding on how agents that they use day to day work under the hood. We're looking to extend the agents training with teaching prompt caching and add new sessions on: using coding agents, agent skills, and building agentic loops. We tried out the three sessions as workshops alongside our [annual engineering conference](https://engineering.zalando.com/posts/2024/06/hosting-an-internal-engineering-conference.html) where we tested the demand for the sessions.

One important guidance for training sessions is to state explicitly when manual coding is expected from attendees, given that the training is aimed at building new skills. We have observed that the temptation of participants to use coding agents as a shortcut to achieve results is high. Yet, using coding agents usually inhibits learning.

## Getting to the next level

Across industry, many AI wins and increases in PR throughput are reported for monorepos where the leverage is high. While we have a few monorepos, we largely use separate repositories for our microservices. We will be implementing a scanner to assess the AI readiness of each repository, allowing for correlations between delivery posture and codebase health. The nice side-effect of readiness assessment is an increase in the overall quality of code and promotion of engineering best practices that otherwise would not be applied due to missing ROI (Return on Investment).

To manage the fleet of microservices we have a tool where we define transformations to be run across a set of repositories. These transformations now include AI-based adjustments with a coding agent CLI being run against the codebases. We expect to see a significant increase in the use of this feature when improving and standardizing our codebases.

## What's next?

Like anyone in the industry we observe how AI amplifies the good and bad practices across our organization. Teams that get carried away with agentic engineering end up with large PRs that discourage reviewers and slow down delivery until a team adjusts their practices.

We do see our investments into platforms pay off as well. Our Zalando web monorepo sets up a deployment for each PR, which is wired to live data. This mechanism enables now not only agents, but also non-engineers who can prompt changes and easily review the results before asking engineers to take over. Other frontend teams find themselves implementing similar mechanisms. Our internal documentation hosting is used to safely host applications and prototypes in form of static websites. Enabled by coding agents, engineers ship dashboards, demos, data visualization tools, applications with client-side logic, etc. To ease the setup of prototypes, we will make the process more accessible to non-engineers who today are asked to start with a repository. Their need is typically to share a prototype that's running on localhost with their peers. We're inspired by [Shopify's Quick](https://shopify.engineering/quick) here.

Like every other tech company, we are building an agent platform. It aims to allow teams to easily define and deploy agents, without the need to take care of sandboxing themselves. We are composing the platform from OSS components, such as [kagent](https://kagent.dev/) that handles runtime aspects of agents on Kubernetes. We are also building an Identity Broker component that captures delegation chains for on-behalf-of flows, brokering between different OAuth2 infrastructures, and implementing a token vault. It is designed to be used by an infrastructure gateway in the call path between an agent and an MCP server or between agents. Our goal is to simplify both agent and MCP server development and solve the hard authentication and authorization problems in agentic systems in one place. Our colleagues will be sharing more about the Identity Broker at the AGNTCon + MCPCon Europe on September 18th, 2026 in Amsterdam.

We still have a long list of problems to solve, such as: managing tooling and configuration on users' devices (or moving local environments completely to the cloud), local sandboxing, and auto-routing across models, incl. open-weight ones (users rarely switch models unless nudged by hitting a limit or error). If you're a non-vendor engineering team tackling similar problems and the experience shared in the post sounds familiar to you, feel free to get in touch.

---

*Capture note (watch, 2026-08-29): surfaced via Martin Fowler's [Fragments: August 24](https://martinfowler.com/fragments/2026-08-24.html), which flagged it as "detailed and thoughtful". Published 2026-08-14 — one day outside the strict 14-day lookback window, filed anyway because it has never appeared in this KB and is a rare NON-VENDOR, non-consultancy production account of agentic engineering at scale (>250 teams, 2.5 years), the same class of independent evidence as [[stripe-minions-one-shot-coding-agents]] and [[martinfowler-prince-building-reliable-agentic-ai-systems]]. Images/figures noted inline rather than embedded.*
