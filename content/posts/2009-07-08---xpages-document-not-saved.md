---
title: XPages document not saved 
date: "2009-07-08"
template: "post"
draft: false
slug: "/posts/2009/xpages-document-not-saved/"

tags:
- "old"
- "domino"
- "notes"
- "xpages"
description: "*This is a follow up to my previous post: 'When is a save not a save?'*"
---
*This is a follow up to my previous post: "When is a save not a save?"*

An easy way I found to get around this, if you want to keep the document computing with form under XPages is to create a test document under XPages with computeWithForm set to `false`.

After doing that, open the document in Notes client and try and save it.  It will display any errors it encounters when trying to save.

Fix those errors in XPages and you will be able to save the document with XPages and computing with the form.