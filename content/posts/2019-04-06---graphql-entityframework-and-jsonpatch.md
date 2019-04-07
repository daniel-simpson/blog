---
title: GraphQL, Entity Framework Core and JSON Patch
date: "2019-04-06"
template: "post"
draft: false
slug: "/posts/2019/graphql-entityframework-and-jsonpatch/"
category: "Technology"
tags:
- "development"
- "csharp"
- ".net"
- "graphql"
description: "Implementing an abstracted method of CRUD operations with GraphQL, Entity Framework Core and JSON Patch"
---
For our business – [Take Off Go](https://www.takeoffgo.com/) – I have built a backend system for handling everything from our client relationship management, to finance, to trip management.

We are small, we don't have a lot of requirements and not many people to answer to, so I am comfortable using a custom built system for these purposes rather than using an off-the-shelf solution.

It also gives me a testbed to play with new technology.  This means that I have re-written the same functionality numerous times, some would say needlessly, but it's how I learn.

It started out not long after .NET Core was first released, which means it - the system - and I have grown along with the framework.

At its core, there is a [.NET Core Web API](https://dotnet.microsoft.com/) handling all the logic, a [Hangfire](https://www.hangfire.io/) scheduled task runner, a React interface, and recently a [gRPC](https://grpc.io/) endpoint for exposing APIs to external services.

Initially, I started with a standard Entity Framework setup, with ASP.NET Controllers for all my entities, talking to services in my business-logic layer, reading from the Entity Framework repository in the data layer.

Over time, this grew unwieldy.  There were a large number of controllers that all did basically the same thing - CRUD.  I want to add properties that our guests can travel to, well that's the model, business-logic service, the controller with at least four actions.

I saw this pattern repeated throughout the project and knew there had to be a better approach.

Enter GraphQL - and more specifically [graphql-dotnet](https://graphql-dotnet.github.io/).

I had previously heard of GraphQL and played with it a little, but never really understood, let alone harnessed its potential.  It seemed a bit fad-ish - why would I use that when I can just use Entity Framework and write out my controllers.

As I said in the beginning, I like to use our internal systems as a bit of a playground; so I started with a few basic entities that in terms of the system didn't require much more beyond simple CRUD operations - i.e., there was no special logic that needed to happen when entities were created or updated.

It quickly became apparent to me that there was some great potential here.  I gradually rolled out GraphQL across the board for all my entities.

I wrote a couple of helper methods to avoid the repetition that sparked this endeavour.  Which meant that I could simply add new entities with a few lines of code, such as -

```csharp
RegisterSingleType<CountryType, Country>("country");
RegisterListType<CountryType, Country>("countries", new ListFilter[]
{
    new ListFilter<Country, string>("filter")
    {
        ArgumentType = typeof(StringGraphType),
        Func = (ent, value) => ent.Name.Contains(value, StringComparison.InvariantCultureIgnoreCase)
            || ent.Iso2.Equals(value, StringComparison.InvariantCultureIgnoreCase)
            || ent.Iso3.Equals(value, StringComparison.InvariantCultureIgnoreCase)
    }
});
```

You can see this in context as a [gist here](https://gist.github.com/brendanmckenzie/2b964194229fd36bbe28c5c946d9da80#file-myquery-cs).

This was great, it gave me a great interface for querying data as I needed it on the frontend.

The next step was creating and updating data.

As I was adopting "new" technology, I saw potential in [JSON Patch](http://jsonpatch.com/).  I didn't like the idea of constantly sending entire objects back and forth over the wire and JSON Patch solved this.  I only had to send the delta and apply those changes.

The more I thought about it, in terms of Entity Framework - prior to actually attempting an implementation, that is - the more it made sense.  JSON Patch would apply operations to objects queried and tracked by Entity Framework the same way I would if I were manually updating those objects.

For simple entities - like my Country class above - this was perfect.  I would just query the entity from my data context, apply the patch, save the changes.  It seemed too good to be true.

And it was, for complex types.  What if I have a Customer class, and they can have a number of Quotes associated with them.

I want to query the customer, and their quotes, display them on my web interface, allow the user to make changes to them, then patch in those changes - to the customer, and to their quotes.

When I first thought through this problem (again, prior to attempting an implementation) I thought that Entity Framework would "just work."  And Entity Framework _would_ just work - Entity Framework Core, on the other hand, would not.  The reason being how both frameworks handle the lazy-loading of linked entities.

In Entity Framework, adding the `virtual` modifier to my `Quotes` collection should have done the trick.  Entity Framework Core doesn't work that way.

In hindsight, I was glad it didn't just work like that as I would have eventually shot myself in the foot.  What I didn't realise to be relevant was that the order of items in those collections matters.  If I modified the 2nd quote in the list, JSON Patch would identify it as being the "2nd item in the list", it wouldn't use any database identifiers.  Both Entity Framework and Entity Framework Core do not support sorting of the child collection.

What this meant was that when I queried my data from GraphQL and presented it to the user had to be the same way that I would query my data when patching.

This wasn't overly complex, it just meant that I had to add a bit more logic to the code querying my data context.

There was one final hurdle to overcome.  What would happen if I wanted to assign a User to a Quote?  If, on my web interface, I were to have a `<select />` drop down on my Quote form where I could choose from a list of users who the quote was assigned to, the JSON Patch it would generate would try to "replace" (update) all the fields on the linked user, which would cause a bit of pain when applied to the entity tracked by the data context.

Handling this on the front-end where the patch was generated was a bit dangerous, I didn't want to interfere with the JSON Patch libraries too much, so I took to handling this on the API itself.

The ASP.NET Core JsonPatch library works nicely with Newtonsoft's `JObject` implementation, so with a bit of trivial code, I was able to manipulate the inbound list of patch operations to work as required.  It's also easily extensible, like the GraphQL query, to add support for new entity types.

The resulting code - that I will admit is dangerously missing documentation - can be found in [this gist](https://gist.github.com/brendanmckenzie/a50f4eb7d5913372d01fef8e73c5dc9b).

Why is this in its own controller and not a GraphQL mutation, I hear you ask.  Initially, I went down this path.  I thought I could have a nice mutation that accepted a list of patch operations and that would be it.  The problem here is that the `value` field on a patch operation can be of _any_ type, a string, an int, a boolean, or a full-blown JSON object.  I was trying to force a square through a circular hole.

And with that, I have three out of the four CRUD operations implemented.  The final - D - is fairly trivial and doesn't quite deserve discussion.

What this post does not touch on is the frontend interface.  For the most part I use [Apollo](https://www.apollographql.com/docs/react/) and `fetch()`.  One issue that still plagues me is updating the Apollo cache after performing create and update actions.  Either I struggle to comprehend their documentation, or there's no straightforward way of updating the client-side caches after modifying data.  But that... is a problem for another time.