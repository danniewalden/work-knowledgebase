---
source_url: https://www.linkedin.com/posts/goeleven_this-is-the-third-post-in-a-mini-series-that-activity-7126176217610768385-HKVo
title: "Translate an event model into code (3): the Event Sourced Projection"
author: Yves Goeleven
publication: LinkedIn
published: 2023-11-06
retrieved: 2026-06-14
type: article
---

# Translating an event model into code — part 3: the Event Sourced Projection

**Yves Goeleven** — *LinkedIn post (2023), third in his mini-series on translating an event model into
code. Captured via logged-in Chrome.*

---

This is the third post in a mini-series that explains how I translate an event model into code. This
time I'll cover the pattern I use to turn a history of events into a state representation that is
consumable by people. More specifically the scenario where the consuming person is the same person
that invoked a command a bit earlier in the process, and now they want to see the result of their
effort.

Note that the event history is representing the state changes of the business process leading up to
the entity, and not the lifecycle of the entity itself.

My pattern of choice for this scenario is the Event Sourced Projection. A projection converts a stream
of events into one or more state objects. The code for such a projection typically looks like this:

```csharp
public class ProjectToSalesOrderDetail:
    IProjection<SalesOrderDetail, BookingStarted>,
    IProjection<SalesOrderDetail, BookingConfirmed>
{
    public void Project(SalesOrderDetail order, BookingStarted msg)
    {
        order.PurchaseOrderReference = msg.PurchaseOrderId;
        order.SellerReference = msg.SellerReference;
        order.BuyerReference = msg.BuyerReference;
        order.Status = "Pending";
        order.OrderLines = msg.OrderLines;
    }

    public void Project(SalesOrderDetail order, BookingConfirmed msg)
    {
        order.Status = "Confirmed";
    }
}
```

Projection code is usually very straight forward, copying over data from the stream of events, into a
single data model. When the caller is the same person that invoked a command just before, I will
typically execute this projection in process of the query handler (e.g. HTTP Get request) itself.
First I'll load all the events of the process where this entity originates from, pass all those events
into the projection code, and return the projected entity back to the caller.

The shape of the state object varies based on the needs of the caller: This single stream of events
can be turned into a purchase order, a notification for that purchase order, a sales order, a receipt
for the sales order, a confirmation message for the sales order, a list of sales orders, or whatever
other shapes the users have in mind, now.. and more importantly, in the future...

(A more detailed C# code example is linked from the post.)
