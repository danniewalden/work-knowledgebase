---
source_url: https://www.linkedin.com/pulse/your-workflow-should-live-inside-giant-process-manager-miuwc
title: Your Workflow Should Not Live Inside a Giant Process Manager
author: Adaptech Group (Adam Dymitruk's consultancy; article published on the Adaptech Group LinkedIn page and reposted by Adam Dymitruk)
publication: LinkedIn (Adaptech Group / LinkedIn Pulse)
published: 2026-07-28
retrieved: 2026-07-29
type: article
---

A long-running business process often begins as a simple sequence.

Check inventory. Confirm payment. Arrange shipping. Notify the customer.

The first version may fit inside one class or service. Then real operating conditions arrive. An external system stops responding. A payment succeeds but the confirmation is delayed. A retry creates the risk of doing the same work twice. A deployment restarts the application halfway through the process.

The workflow grows until one large saga or process manager contains every step, exception, retry, and compensation rule.

At that point, the problem is larger than code complexity. The organization can no longer see the current state of the business process without understanding the coordinator's internal logic.

That lack of visibility creates delivery risk.

## Hidden workflow state becomes an operational problem

When a process is buried inside procedural code, several basic questions become difficult to answer:

What has already finished?

Which external result is still missing?

Did the payment fail, or did the response simply arrive late?

Can the process continue safely after a restart?

Would another attempt repeat an action that already succeeded?

Support teams need these answers when customers call. Operations teams need them when work stops moving. Developers need them before changing the workflow. Leaders need them when evaluating delays, reliability, and modernization risk.

A large coordinator may contain the answers, but they are expressed as branches, internal state, and implementation details.

The workflow exists, but the business cannot easily inspect it.

## Represent progress as information

A more practical design is to model workflow progress as visible information.

For each active process, create a projected to-do list that records what the system knows, what has been completed, what remains unfinished, and whether enough information is available to continue.

Consider a stock purchase.

The system receives a request to buy shares, but it cannot submit the order until it has a current market price. A projected row could show:

The requested stock and quantity
Whether a price has been received
When that price arrived
Whether the order was submitted
The result of the submission
Whether another attempt is allowed

That row does not replace the event history. Events remain the record of what happened. The projection turns that history into a view that people and automated processors can use.

The process becomes easier to understand because the current state is visible.

## Give each processor one responsibility

Once workflow progress is represented clearly, one large coordinator is no longer necessary.

A small processor can retrieve the market price.

Another can submit the purchase once a valid price is available.

A separate processor can manage retries or check an uncertain result.

Several processors can observe the same projected to-do list. Each responds only to the fields and statuses related to its job.

This creates a useful separation of responsibility. The price processor does not need to understand every possible outcome of the purchase. The submission processor does not need to know how the market price was obtained. Each component can remain focused, testable, and replaceable.

The workflow still coordinates correctly because the projection shows which information is present and which step is ready.

## External calls are business states

One reason long-running workflows become difficult is that external calls are treated as lines inside a procedure.

Call the payment provider, receive the result, then continue.

In production, that interaction contains several meaningful states. The request may not have been sent. It may be waiting for a response. The response may have arrived too late. The external system may have completed the work even though the local system never received confirmation.

Those states matter to the business.

A stock price has a timestamp because the organization must decide how old the information can be before it is unsuitable for a purchase. A payment attempt needs a stable identifier because the system must avoid charging the customer twice. A shipment request may require verification before another request is sent.

When these conditions appear as events and projected statuses, they can be discussed, measured, and improved. When they remain inside a long procedure, they are harder to observe and easier to misunderstand.

## Recovery should be visible before a failure occurs

A useful test for any business workflow is to ask what happens if the application stops at each step.

If a server restarts after payment succeeds but before the application records the result, what does the system know?

If the answer depends on an in-memory position or a hidden flag inside one process manager, recovery will be difficult.

An event history and projected to-do list provide durable evidence.

The system can see that the payment was requested. It can see whether a confirmation event arrived. If the result is uncertain, a processor can verify the payment status instead of charging the customer again.

Recovery becomes part of the normal design rather than a collection of special cases added after failures occur.

That difference matters during modernization. Legacy systems often contain workflows that function under normal conditions but are difficult to resume, inspect, or change. Replacing one large coordinator with visible states and focused processors can reduce the number of assumptions held inside the code.

## Visibility improves more than architecture

The same projection that coordinates processors can also support operational tools.

A dashboard can show which orders are waiting for payment, which purchases are waiting for market data, or which requests have exceeded an expected service level.

Support staff can see why a customer's process stopped.

Product teams can measure how long each step takes.

Developers can identify whether delays come from an internal decision or an external dependency.

The technical design begins to reflect the language the business already uses.

A status such as PaymentAcceptedAwaitingShipment communicates more than a workflow instance marked at step seven. It describes the condition in terms that people across the organization can discuss.

## Event Modeling exposes the workflow before implementation

Event Modeling helps teams identify this structure early.

The model shows the business process as a timeline of commands, events, projections, and automations. Instead of drawing one box labeled "Saga," the team can see the decisions and facts that move the workflow forward.

A purchase request produces an event.

A projection shows purchases waiting for a price.

A processor obtains the price.

Another event records what was received.

The projection updates, and a different processor submits the order.

That sequence allows business leaders, architects, developers, and testers to examine the same process before it becomes distributed across services and infrastructure.

At Adaptech Group, this is one reason Event Modeling is treated as a foundation for Event Sourcing work. It gives the team a shared picture of the information flow and reveals where a large procedural coordinator can be replaced with smaller, clearer responsibilities.

## Start with one existing saga

A full architectural transformation is not required to test this approach.

Choose one process manager, orchestration service, or long-running workflow that causes operational confusion or slows delivery.

List every piece of information it needs. Include external results, timestamps, attempt counts, approvals, failure reasons, and completion states.

Then ask which missing item prevents the next decision.

That question often reveals the processors the workflow actually needs.

Turn those requirements into a projected to-do list. Use focused processors to complete each unfinished responsibility. Record the results as events.

The finished design should make the process easier to inspect than the code it replaces.

When the system can show what happened, what it knows, and what must happen next, workflow complexity becomes something the organization can manage rather than something a few developers must remember.
