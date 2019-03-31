---
title: Developers are not designers
date: "2012-11-09"
template: "post"
draft: false
slug: "/posts/2012/developers-arent-designers/"

tags:
- "development"
- "design"
- "rant"
description: "As chaotic as the advertising world is, working at a couple of agencies in London gave me perspective and a lot of insight into the way things should be done; sometimes this was done inversely: I could see what was being done and realised that it wasn't exactly the right way to do it, but it made me realise a way that what was being done could be adapted to a more practical way."
---
As chaotic as the advertising world is, working at a couple of agencies in London gave me perspective and a lot of insight into the way things should be done; sometimes this was done inversely: I could see what was being done and realised that it wasn't exactly the right way to do it, but it made me realise a way that what was being done could be adapted to a more practical way.

Having recently moved to Toronto, and out of the advertising world into the corporate one there is a major issue I am constantly facing, and it goes against everything I learnt in London.

When we begun working on developing a mobile version of our flagship product the process that ensued to getting us where we are today has left a bad taste in my mouth. One of my initial tasks was to assess the current site and determine what technologies could be useful in developing the mobile version. This inevitably lead to me designing the website's look-and-feel and how the user would interact. I raised concerns at the beginning stating "I am a developer, not a designer" but it went unheeded and my *designs* were used.

From my lessons I learnt there is a method to be followed (even if it's loosely) when building for the web. What should happen is this: A client (be it internal or external) has a requirement.  

* The account and/or product handlers take the requirement and build a specification of what the client actually wants in terms that everyone - from the client to the techs - involved can understand.  
* The user-experience planners get to work with the creatives consulting the techs where necessary planning out how the overall website will look and function 
 * Note: At this point the techs are only consulted, their job isn't to make decisions in this step it's more to give the user-experience experts guidance, the creatives and user-experience guys should know basically what they can and can't do
* From here the creatives take the UX documents and build the look-and-feel of the website.  
* Once the creatives have finished the designs it finally ends up at the techs who get working on the functionality of the website, generally split into two parts - front-end and back-end.  
* The front-end developers take the designs from the creatives and generate the HTML/CSS/JS that's required to make the website look right.  
* The back-end developers take the specification of what the website is meant to do, and the HTML/CSS/JS then get to work implementing the required functionality. 
 * Again, there should be some overlap between the front and back-end developers.

What I want to make clear is that the techs should really have very little input in the project until the creative is done. We (I say we - because it's what I do) should have everything we need before we get started. If there are pages or extra functionality that can be bolted on at a later date then that's acceptable, but for the most part, the creatives should finish their work and hand it off to the techs and be done with it until it goes through QA and client-review.

Breaking this process and getting the tech involved too early will lead you to a path where technical minds will get in the way of creativity and functionality. Which is very much the case here. There has been too much emphasis put on the functionality of the back-end system and the front-end has suffered: it's not a website built for the user, it's a website built for the system behind it.