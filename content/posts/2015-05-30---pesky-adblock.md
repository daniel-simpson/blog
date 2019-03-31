---
title: Pesky Adblock
date: "2015-05-30"
template: "post"
draft: false
slug: "/posts/2015/pesky-adblock/"

tags:
- "programming"
- "javascript"
- "adblock"
description: "I was tasked with implementing some extra levels of validation on the registration form of a website I built.  Registration was a simple AngularJS form that hit an ASP.NET WebAPI endpoint."
---
I was tasked with implementing some extra levels of validation on the registration form of a website I built.  Registration was a simple AngularJS form that hit an ASP.NET WebAPI endpoint.

The validation had to occur on usernames and email addresses.  I checked both individually and found that they worked as expected so shipped it to QA.

QA sent it back to me saying that username validation worked fine but email failed, it just hung.

Odd, I tried again on my local instance and everything still worked fine, until I tried subsequent validations on the same page without refreshing.

I would enter an existing username and an existing email address, submit the form and get a validation error on the username - as expected, then I would change the username to something unique and try to resubmit the form.  Nothing happened, the request hung, just as described by QA.

I set breakpoints on the API endpoint to see if the requests were even hitting the web server.  They were not.

After a few minutes of fiddling I opened the "Network" tab in Chrome DevTools and saw that only "Provisional headers" were being shown for the subsequent request which indicated that the request wasn't actually being executed.

I did a quick Google of this and some StackOverflow posts pointed towards AdBlock blocking the subsequent requests.

I disabled AdBlock and everything worked as expected.

Why AdBlock was causing this I'm not sure, but now a little notice next to the "Register" button has to inform users that if they are experiencing difficulties that they should disable AdBlock for our website - which thankfully doesn't even serve ads.