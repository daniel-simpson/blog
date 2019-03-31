---
title: IIS + Domino + XPages
date: "2009-06-18"
template: "post"
draft: false
slug: "/posts/2009/iis-domino-xpages/"

tags:
- "old"
- "domino"
- "iis"
- "xpages"
description: "I have come across an issue when using IIS as the HTTP front end to Domino where XPages fails to work."
---
I have come across an issue when using IIS as the HTTP front end to Domino where XPages fails to work.

What made it obvious was all the 404 errors I was getting when looking at the Firebug console.

It turns out there is some extra configuration required on the server side to make it work, [described here](http://www-01.ibm.com/support/docview.wss?uid=swg21369735).

It appears that all you need to do is add the following to the <UriGroup> and it should work

    <Uri Name="/domjs/*"/>
    <Uri Name="/xsp/*" />
    <Uri Name="/domjava/*"/>