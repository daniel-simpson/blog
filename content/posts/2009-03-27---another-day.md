---
title: Another day...
date: "2009-03-27"
template: "post"
draft: false
slug: "/posts/2009/another-day/"

tags:
- "old"
- "ibm-sucks"
- "notes"
description: "Another half day wasted trying to work my way around the shoddy piece of software IBM like to call Lotus Notes."
---
Another half day wasted trying to work my way around the shoddy piece of software IBM like to call Lotus Notes.

This time it was designer. 

The day started off well enough but then a simple mis-hit on the keys saw my Programmers Pane reading right-to-left, not knowing what keys I pressed I played around with  some client settings and restarted Notes.

**Problem!**  Designer wouldn't start.  No way, no how.  No inclination as to what was happening either.  Stuck.  Again.

After some searching I found the error log file in `Lotus\Notes\Data\workspace\logs` and saw the first entry gave some insight into what the problem was.

    msg="The workspace exited with unsaved changes in the previous session; refreshing workspace to recover changes."

Ahuh!  It seems I must have had some unsaved changes, but how does that help me?

Well knowing that Eclipse uses a workspace directory to store all the configuration for it's layout and what projects you're working on I fished around and renamed the `Lotus\Notes\Data\workspace` directory to `Lotus\Notes\Data\__workspace` and started up designer (after quickly running `KillNotes.exe`) and it loaded up, fresh.

I had lost all my projects but at least I could get back to work...

Thankfully tomorrow marks the beginning of the weekend where I need not suffer the constant quarrels with this *Production* software IBM have released for a couple of days.