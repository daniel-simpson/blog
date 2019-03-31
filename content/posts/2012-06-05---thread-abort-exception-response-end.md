---
title: ThreadAbortException and Response.End
date: "2012-06-05"
template: "post"
draft: false
slug: "/posts/2012/thread-abort-exception-response-end/"

tags:
- "development"
- "asp.net"
- "webforms"
description: "So the project I'm working on one of the tasks was to review the countless exception emails that get sent to all the developers and triage them.  Determine which ones to fix and which to ignore."
---
So the project I'm working on one of the tasks was to review the countless exception emails that get sent to all the developers and triage them.  Determine which ones to fix and which to ignore.

One I came across earlier was the `ThreadAbortException`, the exception never should have been an issue if they had used a generic handler (.ashx) instead of a web form (.aspx), as the actual page is not actually used.  It's a tracking image for an email, where a query string parameter is passed, it's tracked, then a 1x1 pixel gif is returned.

Since deployment is too close I opted for suppressing the error as opposed to fixing the issue (moving to a handler).

The solution was simple.

    try
    {
        Response.End(); 
    }
    catch(ThreadAbortException) { }

The reason for the exception is simply because `Response.End()` tells the current executing thread that it is terminating, or aborting.  The exception is less of an error and more of a notification.