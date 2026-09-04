---
source_url: https://www.awongcm.io/blog/2026/08/23/loop-engineering-teaching-ai-agents-how-to-think/
title: "Loop Engineering: Teaching AI Agents How to Think"
author: Andy Wong
publication: Power of Eloquence (awongcm.io)
published: 2026-08-23
retrieved: 2026-09-02
type: article
---

# Loop Engineering: Teaching AI Agents How to Think

Sun Aug 23 2026 12:00 PM

> **TL;DR**: *You've learned to shape what goes into the model. You've learned to build the harness that lets it act safely. Now comes the layer that decides when the agent is actually done — and who's really driving between now and then.*

*[Image: AI-generated header illustration — "Generated AI image by Google Gemini Nano Banana"]*

## Introduction

In my last [article](https://www.awongcm.io/blog/2026/07/05/harness-engineering-the-next-layer-every-developer-should-master-after-context-engineering/), I wrote about harness engineering — the runtime scaffolding that turns a model into an agent: tool calling, guardrails, state tracking, evaluation. If you've built one of those, you already have an agent that can act safely inside a single task.

But there's a question harness engineering doesn't answer: **who decides what the agent tries next, and when it stops trying?**

For most of 2025 and early 2026, the honest answer was "you do." You typed the next instruction, read the output, decided if it was good enough, and typed again. That's fine for a five-minute task. It falls apart the moment you want an agent to run for three hours, overnight, or on a schedule while you're asleep.

That's the layer this post is about: **loop engineering** — designing the system that prompts, verifies, retries, and stops an agent, so you're no longer the one doing it turn by turn.

---

## What Is Loop Engineering?

Loop engineering is the discipline of designing the outer cycle that runs an agent to completion — instead of you sitting in the loop, steering every step.

The framing crystallised in June 2026, when Boris Cherny, who leads Claude Code at Anthropic, put it bluntly: "I don't prompt Claude anymore. I have loops running that prompt Claude." Around the same time, Addy Osmani and Peter Steinberger were converging on the same observation from different corners of the AI-coding world — that the real bottleneck had quietly shifted from writing a good prompt to designing the system that decides what to prompt next.

Here's the mental model I've found most useful: **a loop is a task plus a check.** A task without a check is just hope. If you ask an agent to fix a bug once and eyeball the diff, that's prompting. If you wrap that same request in a system that runs the fix, runs the tests, feeds any failure back in as fresh context, and repeats until the suite is green or a limit is hit — that's a loop.

The intelligence still lives in the model. The reliability now lives in the loop.

---

## Where This Sits Next to Context and Harness Engineering

It's worth being precise about the boundary, because the three disciplines are easy to blur together.

- **Context engineering** answers: *what do I put in front of the model right now?*
- **Harness engineering** answers: *how does the model act on that — which tools it can call, how a single step is validated and executed?*
- **Loop engineering** answers: *what happens after that step — do we go again, and if so, with what, and for how long?*

A harness governs one step. A loop governs the campaign. You can have an excellent harness — clean tool validation, solid guardrails, good logging — wrapped in a terrible loop that has no real stopping condition, and the agent will still spin uselessly for hours or quietly declare victory on the wrong thing.

---

## The Four Components Every Loop Needs

Every agent loop, no matter the framework, decomposes into four parts. Miss one and the loop either never starts, never stops, or stops without knowing whether it actually succeeded.

### 1. Trigger — what starts the cycle

A schedule, an event (a PR opens, a test fails, a ticket lands), or a plain instruction from a person. The trigger is what lets a loop run without you sitting there to press go.

### 2. Goal — a verifiable end state, not a vibe

"Make the code better" is not a goal a machine can check. "All tests pass," "P95 latency under 300ms," "zero open Sev-1 issues" — those are goals. If you can't write a check for it, the loop can't know when it's done.

### 3. Verifier — how the loop knows it's done

This is the part worth being paranoid about. Prefer a deterministic check — a test suite exit code, a schema validator, a linter — over asking the same model to grade its own output. A model marking its own homework is the one failure mode that quietly poisons every other safeguard you build. When you do need a model as verifier, use a separate agent with different instructions, so the one that wrote the code isn't also the one that approves it.

### 4. Stop rules — multiple independent exits

At minimum: a success exit when the verifier confirms the goal, a hard iteration cap so a stuck loop can't run forever, and a budget cap so a runaway loop can't burn your token spend overnight. Skipping the iteration and budget caps is how people wake up to a five-figure API bill and an agent that looped for nine hundred rounds on a problem it was never going to solve.

```
from dataclasses import dataclass
from enum import Enum

class StopReason(Enum):
    SUCCESS = "success"
    MAX_ITERATIONS = "max_iterations"
    BUDGET_EXCEEDED = "budget_exceeded"
    NOT_DONE = "not_done"

@dataclass
class LoopConfig:
    goal_check: callable          # deterministic verifier, e.g. run_tests() -> bool
    max_iterations: int = 8
    max_cost_usd: float = 5.00

class LoopController:
    def __init__(self, config: LoopConfig):
        self.config = config
        self.iteration = 0
        self.spend = 0.0

    def should_stop(self, goal_met: bool) -> StopReason | None:
        if goal_met:
            return StopReason.SUCCESS
        if self.iteration >= self.config.max_iterations:
            return StopReason.MAX_ITERATIONS
        if self.spend >= self.config.max_cost_usd:
            return StopReason.BUDGET_EXCEEDED
        return None
```

Notice this is deliberately small. It doesn't decide *what* the agent does next — that's still the harness's job. It only decides whether to let the harness run again.

---

## A Minimal Loop Wrapped Around a Harness

If you built something like the `AgentHarness` from the harness engineering post — the piece that validates a tool call, executes it, and tracks state for one step — the loop is the layer that sits one level up and decides whether to call that harness again.

```
async def run_loop(task_input: str, context: RequestContext,
                    harness: AgentHarness, controller: LoopController) -> LoopResult:
    last_result = None

    while True:
        # 1. Act: run one harness pass (gather, act, one tool call, update state)
        last_result = await harness.run(task_input, context)

        # 2. Verify: deterministic check, not the model grading itself
        goal_met = controller.config.goal_check(last_result)

        # 3. Decide: should this loop go again?
        reason = controller.should_stop(goal_met)
        if reason is not None:
            return LoopResult(final=last_result, reason=reason,
                               iterations=controller.iteration)

        # 4. Feed the failure back in as fresh context for the next pass
        task_input = last_result.build_feedback_prompt()
        controller.iteration += 1
```

The shape is intentionally boring: act, verify, decide, feed back. Everything sophisticated in a mature agent system — worktrees for parallel attempts, sub-agents that verify instead of the writer grading itself, persistent state that survives a restart — is a variation on this same skeleton, not a replacement for it.

---

## Where Loops Go Wrong

Most broken loops trace back to a missing or weak version of one of the four components above:

| Symptom                                             | Usually caused by                                                                                                                                      |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Agent declares victory too early                    | Goal is vague, not a real check                                                                                                                        |
| Agent runs forever, making no progress              | No iteration cap, or the verifier never returns true or false cleanly                                                                                  |
| Agent "fixes" the same thing repeatedly             | No feedback path — the failure isn't being fed back into the next attempt                                                                              |
| Surprise five-figure bill                           | No budget cap, or the cap wasn't wired to actually halt execution                                                                                      |
| Agent's own output convinces itself the job is done | Verifier reaches for a second LLM call before exhausting the deterministic check sitting right there — a test suite, a schema, a linter, a status code |

The deepest failure, though, is subtler than any single row: reaching for a five-agent orchestration with a planner and a vector memory before you've proven that one act-verify cycle works at all. A loop amplifies whatever is inside it — a weak verifier doesn't make the loop safer, it just makes the agent's mistakes more expensive to repeat. Start with the simplest loop that could possibly work, usually one act, one deterministic check, and only add machinery when a real failure forces it.

---

## They Nest, They Don't Compete

A harness without a loop is an agent that can act once, safely, and then stop — useful, but you're still the one deciding whether to run it again. A loop without a harness has nothing trustworthy to call on each cycle; it's just retrying blind. You need both, and the boundary between them is exactly the line between *one step* and *the whole task*: the harness's own loop guard stops a single step from spinning, while the loop's stop rules stop the entire campaign.

---

## What to Build Next

If you have an agent doing real work today, or you're about to:

**Short term (this sprint):**

- [ ] Write your goal as an executable check, not a sentence — before writing any loop code
- [ ] Add a hard iteration cap and a budget cap to any agent that currently runs unattended
- [ ] Confirm your verifier is deterministic; if it's a second model call, make it a genuinely separate agent from the one doing the work

**Medium term (next month):**

- [ ] Build the feedback path — feed the exact failure back into the next iteration, not just "try again"
- [ ] Instrument iteration count, stop reason, and cost per run so a stuck loop shows up in a dashboard, not a surprise invoice
- [ ] Separate "the loop's persistent state" from the model's conversation history, so a restarted loop doesn't start amnesiac

**Longer term:**

- [ ] Build a small library of reusable loops for your team's recurring tasks, the way you'd build a shared tool registry
- [ ] Push toward parallel, isolated attempts (separate worktrees or sandboxes) once a single loop is proven trustworthy
- [ ] Track which verifier caught which class of failure, so you know where to tighten the check rather than add another agent

---

## Closing Thought

Context engineering is about crafting the right input. Harness engineering is about building the system that governs what the model is allowed to do with it, one step at a time. Loop engineering is about deciding, without you in the room, whether that step actually moved the task forward — and when to call it done.

The agents that run unattended and don't embarrass you in production won't be the ones built on the cleverest single prompt. They'll be the ones sitting inside a loop with a real goal, a verifier that isn't grading its own homework, and stop rules that actually fire.

That loop is the layer that finally lets you stop being the one pressing "go" every single time.

Till next time, Happy Coding!

---

## References

1. Boris Cherny, quoted in Satvik Paramkusam, ["Loop Engineering: Complete Guide for AI Agents (2026),"](https://www.buildfastwithai.com/blogs/loop-engineering-ai-agents-guide) Build Fast with AI, July 14, 2026.
2. Addy Osmani, ["Loop Engineering,"](https://addyosmani.com/blog/loop-engineering/) addyosmani.com, June 2026.
3. Valentina Alto, ["Introducing Loop Engineering,"](https://valentinaalto.medium.com/introducing-loop-engineering-ac7a6098bb10) Medium, July 2026.
4. Divy Yadav, ["Loop Engineering Explained: 4 AI Agent Loops Every AI Developer Must Know in 2026,"](https://medium.com/ai-engineering-simplified/loop-engineering-explained-4-ai-agent-loops-every-ai-developer-must-know-in-2026-7e1852392cc2) AI Engineering Simplified, Medium, June 2026.
5. explainx.ai, ["What Is Loop Engineering? Beyond Prompt Engineering in 2026,"](https://explainx.ai/blog/what-is-loop-engineering-ai-agents-2026) explainx.ai Blog, July 18, 2026.
6. Anthropic, ["Building Effective Agents,"](https://www.anthropic.com/engineering/building-effective-agents) Anthropic Engineering.
7. Anthropic, ["Claude Agent SDK Overview,"](https://docs.claude.com/en/api/agent-sdk/overview) Claude Docs.

Posted by Andy Wong Sun Aug 23 2026 — tags: ai-engineering, large-language-models, loop-engineering, harness-engineering, ai-agents, agentic-ai, claude, developer-tools
