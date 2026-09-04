---
title: "Dilger — Markdown is a suggestion dressed up as a spec"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [dilger-markdown-is-a-suggestion-dressed-as-a-spec]
raw_file: [raw/notes/dilger-markdown-is-a-suggestion-dressed-as-a-spec.md]
tags: [event-modeling, spec-driven-development, agentic-coding, controversy, focus]
---

# Dilger — Markdown is a suggestion dressed up as a spec

LinkedIn post by **[[martin-dilger]]**, 2026-08-25. Raw capture:
`raw/notes/dilger-markdown-is-a-suggestion-dressed-as-a-spec.md` (297 words), collected 2026-08-26 in a
logged-in browser session. Ends with a promotion for his September "agentic engineer program."

The **Model-as-Language** pole of [[model-as-code-vs-model-as-language]], and the sharpest statement of
it the KB holds.

## The argument

Four moves, in order:

1. **The observation.** "I keep watching engineers explain, in great detail, how something should work.
   Most of the time it's close to begging. Paragraph after paragraph of markdown, trying to get an agent
   to do what it's told."
2. **The economy-of-description test.** *"Pages of prose to produce a handful of lines. If the
   explanation outweighs the thing it's explaining, the tool doing the explaining is wrong - always
   was."* This is the load-bearing argument, and it is a **ratio** argument rather than a correctness
   one: prose fails not because it can't say the thing, but because saying it costs more than the thing.
3. **Code is a formal language — and that's not the objection.** "We have a formal language - it's
   called Code. Now everybody is shying away from it, nothing gets written by hand anymore." Worth
   noting carefully, because it is often misread: Dilger does *not* dismiss code as insufficiently
   formal. He opens by saying hand-writing code is "so 2024" while simultaneously defending code's status
   as a formal language.
4. **The conclusion.** *"The Markdown we use is a suggestion dressed up as a spec. There is only one
   thing worse than written specifications - spoken ones. Both fail the spec-test if the used language is
   wrong. Spec-Driven Development requires suitable language. Event Modeling is the one that works for
   me. A precise specification of behavior."*

Closing exhortation: "Stop writing prose, use a suitable language. Back to engineering please."

## What is actually being claimed

The implicit premise — never stated outright in the post, and worth making explicit because it is where
the disagreement with [[jeremy-miller]] actually lives — is that **code specifies *implementation* while
the thing needing specification is *behavior over time***, which is what [[event-modeling]]'s timeline
supplies. So his objection to code-as-spec is not about formality but about *what* code is formal about.

*(This post does not make the business-reviewability argument that usually accompanies his position
elsewhere — it is a reading of the gap between "code is a formal language" and "Event Modeling is a
precise specification of behavior," not something he says here.)*

Note also the phrase "the one that works **for me**." The post is assertive in tone but the claim is
hedged to personal practice, and no comparison against alternatives is offered.

## Where it sits

This is the quote that anchors the Model-as-Language side of
[[model-as-code-vs-model-as-language]], written four days after Miller staked the opposite ground
([[miller-jasperfx-critterstack-ai-event-modeling-strategy]]), neither naming the other. It is also the
most compact statement of the position behind the tooling ladder in
[[agent-readable-model-artifacts]] and the critique in [[spec-driven-development]] — and it converges
with [[ng-spec-driven-development-is-waterfall-in-markdown]] from a third direction: both reject
Markdown-as-specification, though Ng's objection is that the *provenance* is wrong (nobody agreed it)
where Dilger's is that the *language* is wrong.

The evidence he can point to is not in this post but in the self-training loop two days later
([[dilger-one-million-tokens-self-training-modeling-agent]]): a formal model can be **structurally
diffed** against known-good models, which is a property Markdown does not have. That, rather than the
rhetoric here, is the strongest form of his argument.

## Caveats

- **Marketing.** The post ends by selling the last seat in a paid program, and Dilger sells the platform
  the position implies ([[eventmodelers-ai]]).
- **Assertion, not evidence.** No comparison, no worked example, no measurement — the KB's standing
  caveat on Dilger's LinkedIn output.
- Links in the original were `lnkd.in` shortlinks, unresolved at capture.

## Related

[[martin-dilger]] · [[model-as-code-vs-model-as-language]] · [[spec-driven-development]] ·
[[event-modeling]] · [[agent-readable-model-artifacts]] · [[eventmodelers-ai]] ·
[[miller-jasperfx-critterstack-ai-event-modeling-strategy]] ·
[[ng-spec-driven-development-is-waterfall-in-markdown]]
