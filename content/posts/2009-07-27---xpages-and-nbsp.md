---
title: XPages and &nbsp;  
date: "2009-07-27"
template: "post"
draft: false
slug: "/posts/2009/xpages-and-nbsp/"

tags:
- "old"
- "xpages"
- "web"
- "notes"
description: "I encountered an issue with XPages and a text field in a Lotus Notes document."
---
I encountered an issue with XPages and a text field in a Lotus Notes document.

This is what the field looks like in Lotus Notes.

    image missing

When I loaded this document up in XPages this is what it came out looking like:

    image missing

Notice the new line after "Since."  This is a very long line of text and what was causing me problems was the fact that it was going off the screen and not wrapping around to new lines.

I couldn't figure out what was going on, until I loaded up fiddler and watched the HTML coming through.

This is what I found.

    image missing

Every word was separated by &nbsp; which I initially thought of as just a space character, then it dawned on me what nbsp actually means.  **N**on-**B**reaking **SP**ace.  After "Since I" every word is separated by `&nbsp;` so no breaks are added in, therefore no wrapping.

Solution?  I'm yet to find one.