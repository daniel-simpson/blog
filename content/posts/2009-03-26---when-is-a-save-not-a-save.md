---
title: When is a save not a save?
date: "2009-03-26"
template: "post"
draft: false
slug: "/posts/2009/when-is-a-save-not-a-save/"

tags:
- "old"
- "xpages"
- "ibm-sucks"
- "domino"
description: "I hear you all look at my with a curious expression on your face."
---
I hear you all look at my with a curious expression on your face.

I find myself asking that question far too many times a day lately.

Today I spent the better half of (well, near full) the day trying to figure out why my Lotus Domino XPages page would not save the document.

Access issue? No.

Code issue? Not exactly.

Developer issue? Definitely not.

Quirk with XPages?  You guessed it.

It was discovered that when the document was being saved, the option to compute the document against the form was enabled and therefore validation in the Form was being executed and guess what, it was failing.

Domino threw up no errors, no warnings, no logs.  Just no document modifications.

Things to look out for in this are the computeWithForm attribute of the document element, and certain validations on fields (such as number fields). 

Something else I encountered was the same quirk when I had a text field with the "convertor" set to convert it to currency, if I forgot the currency symbol it would simply not save the document, returning no errors.

*Edit: 2009-04-01 12:09*

It was further found that issues were being caused by documents created with older versions of the form in use.  Refreshing the documents against the form solved this.