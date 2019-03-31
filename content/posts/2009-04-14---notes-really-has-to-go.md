---
title: Notes... really has to go
date: "2009-04-14"
template: "post"
draft: false
slug: "/posts/2009/notes-really-has-to-go/"

tags:
- "old"
description: "Further to my post a few days ago..."
---
Further to my post a few days ago...

There are a few more points I have thought of that show Lotus Notes/Domino as a sub-standard product.

# Debugging

There is next to no support out there for developers.  Coming from a Microsoft background of development, trying to develop for Domino is neigh on impossible given the little interaction you are given with the running application.  When debugging applications/systems/websites in Microsoft-land the first place you look is the debugger, it gives you access to call stacks, current variables, and allows you to compute values on-the-fly while the application is running.

Lotus gives you the LotusScript debugger.  But what good is that for agents running on schedules, agents running on the web and most of all, agents that aren't running LotusScript?

# Reporting

I admit, Crystal Reports is terrible, but it gets the job done.  Where is reporting in the Lotus world??

Thus-far the only way I have been able to create anything near "user-friendly" reports has been to write an agent to output HTML and mess around with Javascript libraries to generate something remotely-readable, forget about maintainability though.

# I admit...

There are certain aspects of the Lotus Notes/Domino system that are amazing, the replication, security, etc...

But what good is all that when the implementation and end-user experience is horrific?

The system may be great to administer, but for an end-user to use?  Forget it.