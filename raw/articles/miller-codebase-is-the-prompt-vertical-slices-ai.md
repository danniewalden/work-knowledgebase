---
source_url: https://jeremydmiller.com/2026/06/04/the-codebase-is-the-prompt-wolverine-vertical-slices-and-ai-assisted-development/
title: "The Codebase Is the Prompt: Wolverine, Vertical Slices, and AI-Assisted Development"
author: Jeremy D. Miller
publication: The Shade Tree Developer
published: 2026-06-04
retrieved: 2026-06-15
type: article
---

*I'm taking a little bit of time today to start writing up a "strategery" document on the JasperFx / Critter Stack approach to AI in the near future. One of the arguments I'm wanting to lean into quite heavily to call Wolverine AI-friendly is how it compresses code in its approach to "Vertical Slice Architecture" and how its focus on the "A-Frame Architecture" to testability has also made Wolverine AI friendly as well.*

Formal layered architecture approaches like the Clean Architecture or other Hexagonal Architecture flavors have dominated the .NET landscape as the accepted "best practices" approach for years. It was a well intentioned strategy to improve maintainability through enforcing some level of loose coupling. Today though, there's a new factor that's annoyingly dominating seemingly all software development discourse: the AI coding agent.

An agent doesn't get tired, but it does have a finite context window, and it pays — in tokens, in latency, and in accuracy — for every irrelevant file it has to load to understand one feature. The structure of your codebase is now, effectively, part of the prompt. And it turns out that the architecture that's easiest for an agent to reason about is a vertical slice approach, which is conveniently enough, what I'd prefer to do anyway and something that Wolverine is very good at.

I want to make the case that the Critter Stack — and Wolverine specifically — is the best foundation and approach in .NET for vertical slice architecture in the age of coding agents, precisely because of how aggressively it compresses the code you have to write and read for each feature as well as the structural consistency you'll get by following our recommended idioms.

## Why layered architectures fight the agent

Picture the canonical "clean" layered solution: controllers in one project, application services in another, a pile of `IRequest`/`IRequestHandler` types, repository interfaces and their implementations, DTOs, mapping profiles, and a domain project underneath it all. To change one behavior — say, how a shipment gets created — an agent has to go find the controller, the request, the handler, the validator, the repository interface, the repository implementation, and probably a mapping profile or two. They live in six or seven directories, scattered among dozens of unrelated features that share those same folders.

Every one of those files has to be pulled into the agent's context before it can safely make a change. Most of what it loads is irrelevant to the task. The signal-to-noise ratio in the context window collapses, and that's exactly the condition under which agents start guessing — inventing abstractions you didn't ask for, "fixing" error cases that can't happen, and drifting away from the intent of the change. The architecture that was supposed to manage complexity ends up manufacturing context pollution.

This isn't a hypothetical. It's become the dominant theme in writing about AI-ready codebases over the last year, usually under the banner of *locality of reference*: keep everything a feature needs in one place, and the agent loads only what's relevant. The conclusion practitioners keep arriving at is that feature-organized, vertical-slice code is simply easier — and cheaper — for an agent to work in than layer-organized code.

## Vertical slices, and the ceremony problem

Vertical slice architecture, as Jimmy Bogard originally framed it, organizes code around features instead of technical layers. A slice owns its whole pathway: take the input, do the work, produce the output, all in one place. It's no accident that the .NET community tends to conflate VSA with MediatR — they share an originator, and MediatR's request-per-handler model nudges you naturally toward one self-contained unit per use case.

*For the record, FubuMVC (Wolverine's predecessor) also promoted what we now call "vertical slices," but as Jimmy told me, does it matter if nobody used the tool? (ouch).*

But here's the thing, the "just use MediatR" approach still carries a surprising amount of ceremony. For one feature you typically write a request record, the `IRequest<T>` marker, a handler class implementing `IRequestHandler<,>`, constructor injection for every dependency, an explicit `SaveChangesAsync`, a separate call through `IMediator`/`IPublisher` to raise follow-on events, a `Program.cs` registration, and a pipeline behavior to wire up validation. The slice is co-located, which is good. But it's not *small*. There's a lot of structural code surrounding the two or three lines that actually express the business decision — and the agent has to read all of it.

If fewer files and tighter context are what make vertical slices good for AI, then the natural question is: how few artifacts can a slice actually be reduced to?

## Wolverine takes the slice to its logical conclusion

This is where Wolverine earns its place in the conversation. Wolverine is, in effect, vertical slice architecture compressed about as far as the language allows. Consider a typical "create a shipment" slice the MediatR way:

```c#
public record CreateShipment(Guid OrderId, string Carrier) : IRequest<ShipmentCreated>;

public class CreateShipmentValidator : AbstractValidator<CreateShipment>
{
    public CreateShipmentValidator() => RuleFor(x => x.Carrier).NotEmpty();
}

public class CreateShipmentHandler : IRequestHandler<CreateShipment, ShipmentCreated>
{
    private readonly IDocumentSession _session;
    private readonly IPublisher _publisher;

    public CreateShipmentHandler(IDocumentSession session, IPublisher publisher)
    {
        _session = session;
        _publisher = publisher;
    }

    public async Task<ShipmentCreated> Handle(CreateShipment request, CancellationToken ct)
    {
        var shipment = new Shipment(request.OrderId, request.Carrier);
        _session.Store(shipment);
        await _session.SaveChangesAsync(ct);
        var @event = new ShipmentCreated(shipment.Id, request.OrderId);
        await _publisher.Publish(@event, ct);
        return @event;
    }
}
```

Plus the controller that calls it, plus the MediatR and validation-pipeline registration in `Program.cs`.

Here's the same slice in Wolverine:

```c#
public record CreateShipment(Guid OrderId, string Carrier);

public class CreateShipmentValidator : AbstractValidator<CreateShipment>
{
    public CreateShipmentValidator() => RuleFor(x => x.Carrier).NotEmpty();
}

public static class CreateShipmentHandler
{
    [Transactional]
    public static ShipmentCreated Handle(CreateShipment command, IDocumentSession session)
    {
        var shipment = new Shipment(command.OrderId, command.Carrier);
        session.Store(shipment);
        // The returned event is published by Wolverine as a cascading message.
        // No IMediator. No manual SaveChangesAsync. No pipeline wiring.
        return new ShipmentCreated(shipment.Id, command.OrderId);
    }
}
```

Look at what disappeared. No marker interfaces — Wolverine discovers handlers by convention, so the type carries no `IRequest`/`IRequestHandler` noise. No constructor and no fields — dependencies arrive by *method injection*, declared right where they're used. No manual transaction management — `[Transactional]` (or a global auto-transaction policy) lets Wolverine and Marten manage the unit of work and use the document session as a transactional outbox. No separate publish call — returning a value *is* publishing it, as a cascading message. The validator is still a plain FluentValidation validator, but it's discovered and run by Wolverine's middleware; there's no pipeline behavior to hand-wire.

*And also, the Wolverine version also integrates a transactional outbox capability for durable execution. Now that there is so much interest in modular monoliths right now as well, I think it's going to be important for folks to consider asynchronous workflows between modules within the same system. Conveniently enough, Wolverine has very strong support for that through its in process queueing, transactional outbox for durability, and built in Open Telemetry tracing for visibility into the asynchronous workflows. MediatR and all the tools it has inspired typically do not have any of that.*

What's left is almost entirely the business decision — and that's the whole point!

It compresses even further on the HTTP edge. With Wolverine.Http, the endpoint *is* the handler — there's no controller calling a mediator calling a handler:

```c#
public static class CreateShipmentEndpoint
{
    [WolverinePost("/shipments")]
    [Transactional]
    public static ShipmentCreated Post(CreateShipment command, IDocumentSession session)
    {
        var shipment = new Shipment(command.OrderId, command.Carrier);
        session.Store(shipment);
        return new ShipmentCreated(shipment.Id, command.OrderId);
    }
}
```

And if you're doing event sourcing with Marten, the aggregate handler workflow collapses the load-decide-append-save dance into a single method that receives the current aggregate state and returns the resulting events:

```c#
public static class ShipOrderHandler
{
    [AggregateHandler]
    public static OrderShipped Handle(ShipOrder command, Order order)
    {
        if (order.HasShipped)
            throw new InvalidOperationException("Order has already shipped");
        return new OrderShipped(command.OrderId, DateTimeOffset.UtcNow);
    }
}
```

Wolverine fetches and rehydrates the `Order` from its event stream, hands it to you, appends whatever events you return, and commits — transactionally — without you writing any of that plumbing. The slice is the decision and nothing else.

Mediator tools were valuable when you were using them within ASP.Net Core MVC architectures where MVC controllers organized around domain entities (think `InvoiceController`) had a tendency to get very bloated. MediatR absolutely provided value in those days for teams to mitigate and control the accidental complexity from that type of MVC controller approach. In my opinion though, using a "mediator" should be completely unnecessary with Wolverine.

*Wolverine can of course be used as just a "mediator" too, but I tend to recommend against that in most cases.*

## Why compression is the feature for AI

Tightly co-located slices are good for agents; *small* slices are better. Three reasons it compounds:

**The whole slice fits in context.** When a feature is one record, one validator, and one short static handler, the agent can load the entire unit of work and still have headroom for the task. It never has to reconstruct a flow from fragments strewn across layers, which is precisely the situation where agents hallucinate.

**There's far less surface to get wrong.** Boilerplate isn't free for an agent — it's more code to generate correctly, more interfaces to implement consistently, more registration to remember. Every artifact Wolverine removes is an artifact the agent can't fumble. Returning a cascading message can't drift the way a hand-written `IPublisher.Publish` call can be forgotten or mis-ordered.

**It's cheaper to operate.** This one is easy to overlook. Fewer tokens loaded per task is a direct, recurring cost reduction every single time an agent touches the code — whether that's a developer's Copilot session, a Claude Code run, or an automated diagnostic agent. In a world where you may be paying per token to run agents against your system, the most compressed codebase is also the cheapest one to keep an agent working in.

And by the way, our new curated AI Skills for the Critter Stack will help you settle into idiomatic vertical slice usage with Wolverine and Marten that will fit well into AI usage. And it so happens that you can purchase access to those AI Skills from the JasperFx website 🙂

## Compression alone isn't the whole story

I want to be honest about where "just write tiny handlers" stops being sufficient, because the failure mode is real. When every part is small and stateless, the burden of knowing *how the parts wire together* — what conventions discover a handler, what a cascading return actually does, what middleware runs around your method — doesn't vanish. It shifts somewhere. If it shifts into the agent's context as guesswork, you've traded one problem for another.

The answer is conventions plus documented context. Wolverine's behavior is convention-driven, which means it's *learnable* and, more importantly, *encodable*. This is exactly why we ship AI skill files for the Critter Stack: they give the agent the macrostructure that the compressed slice deliberately leaves implicit — handler discovery rules, the cascading-message model, when and how the transactional middleware applies, the idiomatic shape we actually want. The skills are the constitution; the slices are the code. Together they give an agent a codebase that is both minimal to read and unambiguous to extend. Compressed code without the conventions documented is just terse code. Compressed code *with* the conventions encoded is an architecture an agent can work in confidently.

Two practical notes in the same honest spirit. Wolverine generates the glue code around your handlers, and that generated code is a benefit for AI — the agent writes the small handler; the framework produces the plumbing it would otherwise have to read and reproduce — but your conventions should tell the agent plainly that generated code is not to be hand-edited, and explain the model so it doesn't fight the generator. And the classic VSA critique about duplication at scale still applies: resist the urge to grow a sprawling shared "services" layer the moment two slices rhyme. Wolverine's middleware and compound-handler patterns are the right place to absorb genuinely shared concerns without rebuilding the layered architecture you just escaped.

It's still in flight, but we've put work into our forthcoming CritterWatch tool to give you visualizations of how messages flow between systems or even between handlers within the same system. I'll be recording a video on that some time next week.

## The takeaway

The industry is converging on vertical slices as the AI-friendly way to organize code, and it's converging there for sound reasons: locality, focus, and a clean context window. Wolverine is the most thorough expression of that idea in .NET. It strips a slice down to the business decision, removes the ceremony that an agent would otherwise have to read and reproduce, and — paired with skill files that encode the conventions — gives a coding agent a codebase that is small, coherent, and cheap to reason about.

If your architecture is now part of the prompt, the move is to make that prompt as short and as clear as it can be. That's been the Wolverine philosophy from the start. It just happens to be exactly what the agents want too.

(Tagged: .Net, Marten, Wolverine)
