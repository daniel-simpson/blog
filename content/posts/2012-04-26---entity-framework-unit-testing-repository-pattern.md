---
title: Entity Framework, Unit Testing and the Repository Pattern
date: "2012-04-26"
template: "post"
draft: false
slug: "/posts/2012/entity-framework-unit-testing-repository-pattern/"

tags:
- ".net"
- "entity-framework"
- "sql"
- "development"
- "testing"
description: "I gave myself a problem.  I started reading about test-driven development (TDD), and it had me intrigued.  The way I generally developed websites was having the presentation layer of my applications (mainly MVC websites) somewhat tightly coupled with the data source.  Controllers would be access the database via L2S or EF and pass the returned model to the view.  This works, sometimes (small projects, etc...), but it isn't exactly great when projects start to expand and testing becomes useful."
---
I gave myself a problem.  I started reading about test-driven development (TDD), and it had me intrigued.  The way I generally developed websites was having the presentation layer of my applications (mainly MVC websites) somewhat tightly coupled with the data source.  Controllers would be access the database via L2S or EF and pass the returned model to the view.  This works, sometimes (small projects, etc...), but it isn't exactly great when projects start to expand and testing becomes useful.

What I wanted to achieve was a solid solution structure that would suit my needs that were.

* Absolute persistence ignorance
* Testability via in-memory mock data stores
* Generalisation far enough so development time wouldn't explode

I have four projects (relating to data access, actual application code has nothing to do with what I am discussing so will be excluded from all figures):

* `Sln.DataAccess`
 * explained below
* `Sln.DataAccess.Sql`
 * Contains the implementation for accessing the entities from a SQL database (in my case, via Entity Framework, so could alternatively be named Sln.DataAccess.EF)
* `Sln.DataAccess.Memory`
 * Like above but reads and writes from in-memory System.Collection.Generic.List<>s
* `Sln.Testing`
 * Interacts with the data access classes and makes sure I don't break anything while playing

Under `Sln.DataAccess` I had _Repositories_ and _Entities_.

* _Entities_ contained classes defining the data structures; and
* _Repositories_ contained interfaces defining the method of access to these entities.

Once I started implementing the Sql/Memory repositories I realised there was an issue.  To make this work smoothly with Entity Framework I had to add attributes (or data annotations) to the Entity classes.  This was undesired, the target was to have the `Sln.DataAccess` having absolutely no reference to any `System.Data` namespaced classes, attributes, interfaces, etc...
 
The solution was to replace the classes under Entities with interfaces.  The only downside I could see to this was if I wanted to have global logic on these entities, but with C# 3.0 and extension methods this really is a non-issue.
 
So now I have my solution, I've put together the skeleton of it on github under a public repository; [check it out here](https://github.com/bmckenzie/projects). (n.b. this project was created in VS11 so you may have trouble opening it in previous versions, however none of the code is specific to .NET 4.5 so it is relevant back to when .NET introduced LINQ)