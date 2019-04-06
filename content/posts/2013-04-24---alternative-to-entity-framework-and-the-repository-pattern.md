---
title: Alternative to Entity Framework and the Repository pattern
date: "2013-04-24"
template: "post"
draft: false
slug: "/posts/2013/alternative-to-entity-framework-and-the-repository-pattern/"

tags:
- "entity-framework"
- "repository-pattern"
- "service-pattern"
description: "About a year ago I wrote a post suggesting how one could approach the Repository and Unit of Work patterns when using Entity Framework, at the time I was somewhat new to Entity Framework and it was a shiny new toy that could do everything.  Since then I've been involved in quite a few projects and though it is quite a nice framework, I've concluded that it's not the one tool to rule them all.  I also realised that the Repository pattern isn't always the best approach to take."
---
About a year ago I wrote [a post suggesting how one could approach the Repository and Unit of Work patterns when using Entity Framework](http://brendanmckenzie.com/blog/2012/08/entity-framework-executing-stored-procedures), at the time I was somewhat new to Entity Framework and it was a shiny new toy that could do **everything**.  Since then I've been involved in quite a few projects and though it is quite a nice framework, I've concluded that it's not the one tool to rule them all.  I also realised that the Repository pattern isn't *always* the best approach to take.

The idea behind the Repository pattern, well at least my idea behind it, was that for each entity (table) in the database you have a repository interface and its implementing class.  The associated business logic would access data through the repository by the way of a Unit of Work class.

Upon first glance it appears to be a fun problem to approach, but the more you look at it, the clearer it becomes that Entity Framework *is* a combination of the Repository *and* Unit of Work patterns.

This got me thinking about a better way to approach this.  The goal is to give a bit of separation from the application (say, an ASP.NET MVC website) and the underlying data (the database).

My first step was to implement Services, say I have a Member table, I would have a MemberService class with all actions to take on the Member table.  Though it quickly became apparent that these service classes would grow exponentially in size as the application grows, hurting maintainability.

This lead me to my final approach, which was to still use services, but instead of having one class per *entity*, have one class per *action*.  For example, a for member authentication I would have a class called `Authenticate` inside the `App.Services.Member` namespace.  Services would inherit from a `BaseService` that would simply provide a quick access to a `IDbConnection` and other necessities. Each service would have an `Execute` method however this would not be abstracted by means of the `BaseService` or an interface implementation as the `Execute` method could take any number of methods and provide any type of response.

Although this path provides for great flexibility and maintainability, for simple service calls it can be cumbersome to call a simple action.  This lead me to implement a Helper class that provides a quick means to call services.  The logic remains in the service class, the call is just made easier by the `Helper` class, keeping the `Helper` class smaller in code size.

As I mentioned previously, I found that Entity Framework isn't always the best tool for the job.  When it comes to complex schemas it's sometimes nice to be able to construct your own SQL calls, or use stored procedures (if that's what floats your boat, though in my opinion stored procedures should be used sparingly and for simple <abbr title="Create, Retreive, Update, Delete">CRUD</abbr> operations they are generally unnecessary), this lead me to discover [dapper-dot-net](https://code.google.com/p/dapper-dot-net/), a simple, efficient ORM that provides great flexibility.

The final (abridged) version of what I've been talking about can be [found here](https://github.com/bmckenzie/projects-services).

**Side note**: the discussion for stored procedures and against can be debated until the cows come home.  I've [said my piece on them before](http://brendanmckenzie.com/blog/2012/04/stored-procedures-debate), and I stand by it, at the end of the day, do whatever your comfortable with, you don't need my (or anyone's) blessing.  Use stored procedures, or don't, I'm not a cop.