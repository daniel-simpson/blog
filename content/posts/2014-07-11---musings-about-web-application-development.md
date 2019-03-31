---
title: Musings about Web Application Development
date: "2014-07-11"
template: "post"
draft: false
slug: "/posts/2014/musings-about-web-application-development/"

tags:
- "web"
- "technology"
- "cloud"
- "development"
- "security"
description: "*In the ideal world* is a great way to start any thought, then reality comes in and kills all your big ideas."
---
*In the ideal world* is a great way to start any thought, then reality comes in and kills all your big ideas.

If you were given a project that will start small and evolve into something bigger, how would you approach it?  Would you build something expecting the future, or focus on what's required immediatley and worry about the future later?  Personall I take the latter approach, but that's getting a little away from what I want to discuss.

I want to develop a website, it will run off a database, it will be load balanced between multiple servers, and it must be *fast* and *secure*.

There are a few things to take into consideration when approaching such a project.

 * What database will I use?
 * How will I structure the data?
 * How will I access the data?
 * What technology will I host the website on?
 * Will it run in the cloud or a dedicated server?
 * What will I code the website in?
 * How can I ensure the website will work properly when load balanced?
 * How can I keep the website secure?
 * How will I handle back-end processing tasks?

The first couple of points are a matter of personal preference.  Personally I would choose PostgreSQL and structure the data in the sanest way possible, and access data in the simplest most efficient way possible.

Hosting is a cross of personal preference and funding available.  Cloud seems like a good idea but can get expensive, though it does scale well.  Dedicated is more stable when it comes to pricing, but also has its downfalls, such as scaling and updates.

What technology to code the website in is closer to what I want to discuss.  I have come to the conclusion that my ideal website would be a single page application (SPA, probably heavily utilising [AngularJS](https://angularjs.org)), with all its resources - images, scripts, styles - hosted in a geographically load balanced CDN, accessing an API that's hosted on geographically load balanced cloud servers that read from the same database.

So then, what technology do you code the back-end API in?  The way I see it is that the API is a very light-weight way of accessing what's in the database.  There shouldn't be mountains of logic in the website's API.  It should be fast and responsive.  Frameworks such as ASP.NET add a huge overhead to handling web requests.  The API should only be concerned with what happens on the website and purely with that, the heavy-lifting should be done outside the scope of the website's API.  When a request comes from the website to do some heavy processing a request should be passed off to the complex side of the system and handled there.  Having clarified that, the website would probably best be written in pure C, D, Go or Rust.  I've found [vibe.d](http://vibed.org/) and would probably choose that because of a newfound interest in [D](http://dlang.org).

Now that I have the API sorted, what processes the heavy tasks?  How do I start those tasks?  How do I notify the API when those tasks fail/succeed?  I would probably use message queues ([redis](http://redis.io), [RabbitMQ](http://www.rabbitmq.com), [Amazon SQS](http://aws.amazon.com/sqs)) to pass messages between the services.  The consuming services could be written in anything, I would probably opt for either Python or C#.

How do I make sure the website will work in a load balanced environment?  The issue is that an initial request may be made to server `A`, if subsequent requests are made to server `B` or `C` or `D` etc... how do I ensure the user doesn't notice the server switching?  Ideally the services will all operate in a manner where context doesn't matter, to achieve this a cookie will be created to identify the user's session.  Utilising either the core or an external redis/memcached database a list of sessions will be stored and used for validation on every request made by the client.

How do I stop the user from hijacking someone elses account?  If you store the user access information in a cookie on the clients machine it leaves you vulnerable to attack, to avoid this you can use mechanisms such as HMAC-SHA1 to avoid this.  I would also store a list of user_session's in the database that can be expired on demand to be sure.  All communication will occur over HTTPS for that extra level of security.  Each session will be unique to a browser and will be created when no valid session is found (i.e., the current session has been expired, or no priod session exists), in which case when a user authenticates the session is updated with the user's identifier, and when the logout all user specific information is disassociated from the account.