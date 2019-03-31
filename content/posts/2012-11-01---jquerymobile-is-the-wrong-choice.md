---
title: jQuery Mobile is the wrong answer
date: "2012-11-01"
template: "post"
draft: false
slug: "/posts/2012/jquerymobile-is-the-wrong-choice/"
category: "Technology"
tags:
- "jquery"
- "development"
- "css"
- "javascript"
- "mobile"
- "jquery-mobile"
description: "Whatever the question is, jQuery Mobile is never the right answer. Well, unless you're throwing something together very quickly and have absolutely zero concern for customisability **and** are targeting *only* phones with screens 4.5' and smaller."
---
Whatever the question is, jQuery Mobile is never the right answer. Well, unless you're throwing something together very quickly and have absolutely zero concern for customisability **and** are targeting *only* phones with screens 4.5" and smaller.

Why? Because any phone with a screen bigger than say 5" the website will just look silly. To whatever question might prompt the response "jQuery Mobile" the correct answer will **always** be "[Responsive website](http://en.wikipedia.org/wiki/Responsive_web_design)."  If you design a website to be responsive, you limit yourself to nothing. From the smallest screen to the largest you cover them all, leaving no gaps.  Take this very website for example - granted I did cheat (only because I have zero design skills) and purchased a responsive template - but make the window big, then slowly shrink it down and watch how the website lays itself out to fit whatever the size of the window.

This makes a whole lot more sense than saying "I need to build a mobile website" and taking off down the path of building a mobile-targeted website. Then you realise half way (or further) through planning there are questions like: "What browsers will we support? What resolutions should we make the website for? What devices are we targeting?" If you make a [responsive website](http://stuffandnonsense.co.uk/projects/320andup/) these questions become redundant. Take a leaf out of 320 and up's book and design for the small screen, then work your way up. Do that, or use [Twitter's Bootstrap](http://twitter.github.com/bootstrap/) to base your website on. You'll thank me later.