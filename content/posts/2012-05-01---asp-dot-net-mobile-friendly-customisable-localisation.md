---
title: ASP.NET MVC 4 Mobile friendly, client customisable, localised website
date: "2012-05-01"
template: "post"
draft: false
slug: "/posts/2012/asp-dot-net-mobile-friendly-customisable-localisation/"

tags:
- "development"
- ".net"
- "asp.net"
- "mvc"
- "i18n"
- "mobile"
description: "My current task is to investigate what technologies to port the current WebForms application to, it's been decided that we will go towards MVC, but I need to determine what extra technologies will be needed to match (and of course, better..) the current site."
---
My current task is to investigate what technologies to port the current WebForms application to, it's been decided that we will go towards MVC, but I need to determine what extra technologies will be needed to match (and of course, better..) the current site.

This got me playing with localisation for websites using MVC, the website runs as a single instance servicing multiple clients, some that require their own custom styling, it must be multilingual and support mobile devices.

I wasn't particularly fond of going down the embedded/compiled resources path; so I decided to go for the structured-views approach.

This is what I came up with

	Views
	+ ControllerA
	  + ViewA.cshtml
	  + ViewB.cshtml
	+ ControllerB
	  + ViewA.cshtml
	  + ViewB.cshtml
	+ i18n
	  + en-AU
		+ ControllerA
		  + ViewA.cshtml
		  + ...
	  + fr
		+ Shared
		  + Navigation.cshtml
	  + fr-FR
		+ ControllerB
		  + ViewA.cshtml
		  + ...
	+ Mobile
	  + ControllerA
		+ ViewA.cshtml
	  + i18n
		+ en-AU
		  + Shared
			+ Navigation.cshtml
	  + Shared
		+ Navigation.cshtml
		
The only constraint is that the controller structure of the mobile site must match the structure of the main site (to a certain degree)

It seems like a lot to maintain, but the way I implemented the `ViewEngine` means the website will always fall gracefully back to the default of English It also will fall back from say "fr-FR" and "fr-CA" to just plain "fr" if a higher level isn't available.

[You can see the view engine here](https://gist.github.com/2570631).