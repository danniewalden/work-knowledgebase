---
source_url: https://www.eventmodelers.ai/docs/blog/event-modeling-ui-only-interactions-filtering/
title: "How to Model UI-Only Interactions - A Filtering Example"
author: Martin Dilger
publication: eventmodelers.ai (nebulit | Event Modeling Toolkit) — Blog
published: 2026-07-31
retrieved: 2026-08-17
type: article
---

# How to Model UI-Only Interactions - A Filtering Example

Not every screen interaction needs a Command and an Event. Here's how to model filtering as a pure UI-only interaction using Multi-Screen Views.

July 31, 2026 · 6 min read · Event Modeling & Process

*[Image: Event Modeling UI Only Interactions Example: Filtering — https://www.eventmodelers.ai/assets/images/blog/event-modeling-ui-only-interactions-filtering.png]*

This question came up today, and of course I've answered it dozens of times already. But I realized I never really wrote it down formally. Let's fix that.

*[Image: Slack question: "How would you model filtering? As in, you have a table of data of books and you want to filter it by genre." — .../event-modeling-ui-only-interactions-filtering-1.png]*

"How would you model filtering? As in, you have a table of data of books and you want to filter it by genre. From a technical point of view, this could be just on the client side, but it could also be an API call to refetch the data."

That's the question. And it's a good one, because the honest answer is: it depends - and most of the time, filtering doesn't need a Command or an Event at all.

## Start With a Chapter

You find all my articles and videos on [eventmodelers.ai](https://www.eventmodelers.ai). If you want to follow along, go to [app.eventmodelers.ai](https://app.eventmodelers.ai) - that's the easiest way to start modeling.

You can also do this all using AI by connecting your agent with the new CLI to the platform. It takes only 15 seconds:

```
npx @eventmodelers/cli init-modeling
```

Everything starts with a Chapter. Think of a Chapter as a timeline of things that happen - a small, self-contained slice of the world you're modeling.

*[Image: Book Filtering chapter with three columns across Actor, Interaction, Swimlane and Spec Lane rows — .../event-modeling-ui-only-interactions-filtering-2.png]*

The next thing you'd typically want to do is create the relevant Event(s), Command(s), and Read Model(s). For our books example, that's exactly what happens on the left: a user submits a Command, and a `Book registered` Event lands on the swimlane.

*[Image: A Command flowing into a Book registered event on the swimlane — .../event-modeling-ui-only-interactions-filtering-3.png]*

## Now Define the View for Filtering

Now define the View for filtering. Give the new HTML View a try - you can write your Views with plain HTML, or even better, just generate them very cheaply with your connected agent.

*[Image: Edit HTML dialog showing Page 1 with a plain book list and Page 2 with a filter input field — .../event-modeling-ui-only-interactions-filtering-4.png]*

This is where the actual answer to "how do you model filtering" lives. Page 1 shows the unfiltered list of books. Page 2 shows the same Read Model, but with a filter field on top of it - typed in, applied, done. No round trip to a Command, no new Event.

The Multi-Screen support is what makes this possible: it lets you easily navigate between the unfiltered- and the filtered View, both backed by the exact same `Books[]` Read Model.

Now we already know how it should look. But we still want to describe how it behaves, using Scenarios and Given/When/Then syntax. Here the built-in Query-Support comes in very handy.

*[Image: Scenario 1: Given two Book registered events, When Query by title, Then Books read model returns the matching title — .../event-modeling-ui-only-interactions-filtering-5.png]*

Given two `Book registered` events - one for Harry Potter, one for Lord of the Rings - When you query by title with the key "Harry Potter", Then the `Books` Read Model returns just that one match. Nothing about this Scenario depends on the UI plumbing. It's stated purely in terms of the data.

## Enough to Implement It

This is enough to implement it. Using the UI mockup - which is also accessible for a connected agent building from the model - it's quite clear what needs to be done.

*[Image: Full slice showing the Actor, Command, Book registered event, and the Books read model rendered as an HTML mockup on the right — .../event-modeling-ui-only-interactions-filtering-6.png]*

## Conclusion

What is important to understand: UI-only interaction typically does not involve Commands or Events. Using the Multi-View support, you can show in one slice how the system should behave without inventing state changes that don't exist in the domain.

Filtering, sorting, expanding a row, switching a tab - these are all views on data you already have. Model them as Views, not as Commands looking for an Event to justify them.

My new program "Agentic Engineer" starts on Sep. 7 - teaching you in 3 weeks how to become the Agentic Engineer, working with the Triplet Architecture of Event Modeling, Event Sourcing, and Vertical Slices. There are only 7 seats left.

### Join the Agentic Engineer Program

Apply Spec-Driven Development Hands-On - Event Modeling, Event Sourcing, and AI Engineering with autonomous agents.

## Related Articles

- The Triplet Architecture — Event Modeling, Vertical Slices, and Event Sourcing only pay off when you use all three together. (Event Modeling & Architecture • July 2026)
- How to model branches in Event Modeling — Linearize your conditional flows using Given/When/Then and maintain clear, readable models. (Event Modeling & Patterns • November 2025)
- 7 Insights I Learned Building Event Models Since 2021 — Practical tricks to help you build better Event Models. (Event Modeling & Best Practices • November 2024)

---

*Capture note (not part of the source): article body captured verbatim from the eventmodelers.ai blog page; site navigation, promo banner, and footer stripped. Nine inline screenshots are noted in place with their alt text and asset paths rather than reproduced.*
