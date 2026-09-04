---
source_url: https://jeremydmiller.com/2026/08/31/pondering-continuous-integration-in-our-new-ai-world-order/
title: Pondering Continuous Integration in our new AI World Order
author: Jeremy D. Miller
publication: The Shade Tree Developer (jeremydmiller.com)
published: 2026-08-31
retrieved: 2026-09-02
type: article
---

# Pondering Continuous Integration in our new AI World Order

*[Image: https://jeremydmiller.com/wp-content/uploads/2026/06/image-3.png]*

I read a post from Paul Stack last week I thought was interesting titled [AI Broke the Assumptions Behind CI](https://stack72.dev/ai-broke-the-assumptions-behind-ci/). I was maybe much more influenced by Extreme Programming (XP) back in the day, so I’d disagree a little bit with his characterization of CI being something tied to the pull request workflow in GitHub et al, but let’s talk more about this.

The original point of CI was really just to be constantly getting feedback on your code by building and running tests against it as you change code and adjust as needed if CI found problems. With the radically different part of XP at the time being that you actually wrote tests!

The general idea behind XP was to be able to work faster and more adaptively by providing your team with effective feedback loops to guide and correct the adaptation as you worked. I’d say after all these years that CI is still very important — but it’s time for a serious rethink in our new AI powered world order.

Back to what Paul was getting at in his post, here’s the CI process I admittedly use for Marten, Wolverine, or other Critter Stack tool development:

1. Write code locally and be constantly running the tests most closely related to whatever I’m changing
2. Create pull requests — which we do in no small part just for traceability more so that as a code review tool (GitHub release notes generation is tied to pull requests and that’s just very helpful)
3. Lazily allow GitHub Actions execute all kinds of test suites and smoke test harnesses against the pull request while I go off and worry about something else
4. Merge pull requests when CI goes green or fix broken tests

And that’s mostly worked out until just recently. However, with the extreme load that’s come from all of us yahoos using AI agents to code so much faster, GitHub Actions are very noticeably slower or flat out unreliable on the worst days. And of course, to make things worse, we’ve added a lot more tests and CI actions than we ever tried to do before.

Granted, the Critter Stack work I do is especially problematic in this regard because so much of what we do involves slow running tests that execute against databases and message brokers. We’re also having to constantly build up and tear down .NET applications in memory. Especially for us, but maybe for you too since so many of us depend on now overloaded CI servers, there’s a very real problem that depending on CI builds running on a remote box has become a sometimes unacceptable bottleneck.

To balance a “good enough” safety net and for getting things done, I’ll mirror Paul Stack’s post and say that in some cases I’m:

- Doing trunk based development like it’s 2007 and Subversion is the latest hotness!
- Strictly using local testing with a lighter weight set of suites for commits, and trying to be very selective of what subset of tests are executing based on the changes in flight.
- Using the full blown “HeavyGate” of test suites to do pushes to the remote `main`

In public projects where there’s value in using pull requests just for tracking, I think we’re going to have to get more creative about test run filtering to avoid running test suites that aren’t relevant to the changes in flight to get pull requests in without hours of delays.

On a side note, with CI builds being so slow, that’s forced us to be much more aggressive about stomping out flaky or otherwise unreliable tests so CI is far more consistent for us. I’ve also added a new critter named “[Bobcat](https://github.com/)” (the project is actually old enough that I started it before we adopted the current Critter Stack naming scheme) that among other things, uses the [Microsoft Testing Platform](https://learn.microsoft.com/en-us/dotnet/core/testing/microsoft-testing-platform-intro) to supervise test runs and selectively do test retries, process restarts, and even hard Docker resets based on known test flakes. That’s been hugely helpful both locally where heavy development can break down when Docker containers have run too long in tests and also for CI where retrying a CI failure just in case it’s just a test flake is just too damn slow now.

Anyway, AI assisted development continues to take up more of my gray matter than I wished it did and I don’t think the adaptation is going to change any time soon.

## Capture note (not part of the source)

Captured from the jeremydmiller.com author archive page, which renders the full post inline.
