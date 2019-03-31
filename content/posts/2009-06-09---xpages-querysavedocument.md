---
title: XPages querySaveDocument  
date: "2009-06-09"
template: "post"
draft: false
slug: "/posts/2009/xpages-querysavedocument/"

tags:
- "old"
- "xpages"
- "ibm"
- "lotus"
description: "More playing with XPages and I've come across another anomily."
---
More playing with XPages and I've come across another anomily.

I have a document in which I would like to have some code execute before it's saved.  So naturally I look towards the querySaveDocument event on the data source.  This is where the fun begins.

The code in this event will only fire if I use the "Save Data Sources" (<xp:save />) simple action, using the "Save Document" (<xp:saveDocument />) action does not execute the querySaveDocument (or computeDocument) events.

This is all well and good, the document saves, the querySaveDocument code executes... however, there is a but.

But, using the "Save Data Sources" action, XPages wants to re-direct to another page afterwards, which breaks some niceties of "Save Document"

If I use "Save Document" the view-state of the current page is held, and I can simply tell XPages to change the document mode to read-only and it works fine.

If I use "Save Data Sources" the entire view-state is lost, and leaving the re-direct page blank makes XPages re-direct to the same page, but in doing so reverts to the default action of the XPages, generally in my case(s) that's "Create New Document."  This makes editing the saved document more cumbersome.

References

* <http://www-10.lotus.com/ldd/nd85forum.nsf/DateAllThreadedWeb/e0fed355e231c6bc8525759f0070e8a1?OpenDocument>
* <http://www-10.lotus.com/ldd/nd85forum.nsf/dba3ca7e515d55ff85256a0700727b35/70876ccc74b51a528525754c0067d946?OpenDocument>