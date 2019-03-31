---
title: Notes... has to go
date: "2009-04-07"
template: "post"
draft: false
slug: "/posts/2009/notes-has-to-go/"

tags:
- "old"
- "lotus"
- "notes"
- "microsoft"
- "windows"
- "exchange"
- "outlook"
- "domino"
- "iis"
description: "I would like to hear from one person, who is not currently making or has not recently made a decent income from the Lotus Notes suite of products, who can strongly say they support IBM's Lotus Notes as a user-friendly, efficient, productivity increasing piece of software."
---
I would like to hear from one person, who is not currently making or has not recently made a decent income from the Lotus Notes suite of products, who can strongly say they support IBM's Lotus Notes as a user-friendly, efficient, productivity increasing piece of software.

I don't know what my chances are of finding someone who can say such a thing.

Lotus Notes/Domino developers will defend it with their life.  Lotus Notes users will loathe it like nothing else.

It is a well known fact that Microsoft release products with deficiencies, but the experience I have had using the Lotus Domino/Notes suite of products is nothing like the experience I have had with Microsoft products.

Innumerable times per day I am faced with productivity halting issues caused by flaws, oversights, omissions and what appears to be sheer laziness of developers working on these products.

Microsoft products are intuitive, they work the way users expect them to, because they work the way the rest of the environment (namely for this arguments sake, Windows) does.  Lotus Notes is just YAMPA (yet another multi-platform application) and it is in this that I see it's greatest unravelling.  The software is not intuitive, it does not work the way the majority of it's users expect it to, and last of all, it's down-right ugly.

Lotus Notes/Domino is a full-on collaboration platform "in a box."

To achieve what you have with Lotus Notes/Domino with Microsoft products you would require:

- Microsoft IIS
- Microsoft Exchange
- Microsoft Outlook
- Microsoft SQL Server

So?

- IIS comes with every installation of Microsoft Windows Server (not to mention it's an option for every client copy of Microsoft Windows).
- Granted, Exchange is not a cheap piece of software, but it's scalable and a lot easier to manage and maintain than Domino
- Chances are on all the client PC's where a user will be working they will have the rest of the Microsoft Office suite installed, more-than-likely including Microsoft Outlook
- SQL Server can be described similarly as I have Exchange with the exception of the Express editions which are... free

Neither option is cheap, neither option can be set up by monkies, so why go for the less-supported, harder-to-develop-for option?

There is also one more option one could explore, strangely enough the cheapest one, coming in at $0 - excluding hardware costs.

- Linux/BSD
- Apache
- QMail
- Mozilla Thunderbird
- PostgreSQL

The open source option.

Complete off-topic but I felt it warranted a mention.

Granted with the Microsoft solution you require 4 pieces of software (5 if you include the operating system) compared to the Lotus solution that requires only Domino server and Notes client.

But what about the actual implementation and application of each solution?

To develop for Notes/Domino what are your options?

# Thick client

- Forms
- Views
- Navigators

All contained within the Lotus Notes client.

# Web

- Forms
- Pages
- XPages (new in Domino 8.5 - yet highly unsupported and undocumented) What appears to be Lotus' attempt to achieve what Microsoft has with ASP.NET and what the open source community has achieved with a number of software languages
- Custom built agents
- There is one other option that I forget the name of...

To develop for the Microsoft solution there is really no boundary.

# Thick client

- .NET - WinForms
- Vista (and beyond) - Windows Presentation Foundation 
- MFC
- VCL (for those Delphi/BCB developers out there)
- Direct OS API
- DirectX

# Web

- .NET - ASP.NET
- PHP
- Perl
- Ruby
- ... the list goes on, if you want it to.

You can use whatever development environment you like, you are not locked into a small handful of languages, databases, libraries.  The world is your oyster.

What follows are two words that have been killing me ever since I started with Lotus development.

# Version Control

Where is it in the Lotus world?  The only way to keep versions of your application in the Lotus world is to keep a template, a copy of the application in it's entirity for each "revision."

In the Microsoft world, and far more prevalent in the open-source world?  Subversion, git, CVS, VSS, SourceGear Vault, etc... The list goes on.

No doubt there once was a time and place for Lotus Notes/Domino.  But that time is over, the world is moving to software-as-a-service, and to develop and support development of such services is far too cumbersome to achieve in the Lotus Domino world.

Lotus, your days are numbered.

Love, your Microsoft (and open-source software) loving fan...

Brendan