---
title: AngularJS Models
date: "2014-08-18"
template: "post"
draft: false
slug: "/posts/2014/angular-models/"
category: "Technology"
tags:
- "programming"
- "javascript"
- "angularjs"
description: "I was looking for a method to abstract away integrating my RESTful services for regular CRUD operations.  There's ngResource, but it's a bit voodoo and restrictive.  I wanted to come up with a solution that was a bit more simplictic that's also not surrounded by magic."
---
I was looking for a method to abstract away integrating my RESTful services for regular CRUD operations.  There's [ngResource](https://docs.angularjs.org/api/ngResource/service/$resource), but it's a bit voodoo and restrictive.  I wanted to come up with a solution that was a bit more simplictic that's also not surrounded by magic.

You can [find the code here](https://gist.github.com/brendanmckenzie/cdb3e2a7c8e20c6d4062) along with a simple implementation.  Prior to this I had a service that returned promises that I had to implement the callbacks for.

The implementation isn't tightly coupled to AngularJS so could realistically be used with any framework.

The primary goals of this were:

 * Simplify CRUD operations
 * Be easily adaptable
 * Avoid having to handle promises all over the place