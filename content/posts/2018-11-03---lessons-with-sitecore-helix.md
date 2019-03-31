---
title: Lessons with Sitecore Helix
date: "2018-11-03"
template: "post"
draft: false
slug: "/posts/2018/lessons-with-sitecore-helix/"
category: "Sitecore"
tags:
- "sitecore"
- "development"
- "web"
description: "Before we discovered the [Helix framework](https://helix.sitecore.net/) developed by Sitecore our projects were disorganised, to say the least.  We had no real guideline to follow when building out our solutions.  Helix changed that."
---
Before we discovered the [Helix framework](https://helix.sitecore.net/) developed by Sitecore our projects were disorganised, to say the least.  We had no real guideline to follow when building out our solutions.  Helix changed that.

We stumbled across Helix thanks to a contractor we had on board for some time we ran with it full force.  After some internal discussions, it was decided from that point forward all our projects would be built around the Helix framework.

As with most paradigm shifts, there's a teething period, mistakes were made, lessons were learnt.  One major mistake we made was viewing the provided Habitat project as a boilerplate.  We initialised projects by copying and pasting the Habitat project, bringing along all the cruft that comes with it.  Sites that didn't need forms had hard dependencies on Web Forms For Marketers.

Fast forward a couple of years and we have certainly found our groove using the framework.  We've also found ways to optimise the development process and integrate the concepts within Helix more cohesively in our projects.

As with most advancements, older projects tend to be left behind.  Thankfully, the company I work for allows me time to retroactively apply the advancements we find on newer projects to our legacy projects, simplifying and unifying the development process across our projects.

This article will detail what we encountered and where we made enhancements.

### Choosing the topology

The terminology and documentation around the available "topologies" you can setup with Sitecore 9 can be a little confusing.

For local development we were spinning up the full XP0 topology which included the full xConnect setup.  We were also using Solr locally which made the onboarding process much more intricate.

By switching to the XM1 toplogy - Content Management only - and using Lucene indices locally, the time it took for new developers to start working on projects droppped dramatically.  The only thing we had to be careful about was making any configuration changes that affected the indexes.  We had to make sure the changes we made worked with both Lucene and Solr.

### Project bootstrapping

The first place we found optimisations was in how we bootstrapped our projects.  As previously mentioned, we started new Helix-based projects by copying and pasting the latest copy of Habitat from Sitecore's Github.

The approach we now take is to initialise a blank Visual Studio Solution and structure our repositories inline with the Helix structure.  This is a process that happens once per project, so a little more time spent up front doesn't cost us much lost time.

### Build scripts

The gulp build scripts that come with Habitat are very comprehensive and do build out the project as required, however, they are very slow.  They utilise the Web Deploy feature of projects which slows down package build times.

We re-wrote the gulp script files used to build the solution once then deploy all necessary files to the target build directory.  Our build times went from ~20 minutes for large projects to no more than 3 minutes.

### Layer definitions

One of the constant questions asked when adding new features to a project was "where does this belong, in the foundation, feature or project layer?"

The simplified view we now take is this -

* Foundation - the feature belongs here if it's absolutely abstracted away from the specific project, such that it can - without any further modification - be dropped into another project.
* Feature - most all features belong in this layer
* Project - there should be absolutely minimal amounts of code in this layer, the majority of the content of this layer should be configuration and serialisation objects

Furthermore, we have made the decision that foundation layer projects should have no UI elements, there should be no styling or views (renderings) contained in any foundation layer projects.

Our approach to handling markup views is still evolving, see the Future section at the end of this article.

### Front-end assets

The base Habitat install didn't really pay much attention to how front-end developers are meant to work with Helix solutions.

We use webpack across most of our projects.  The default gulp task we have (initiated by simply running `yarn start`) starts a webpack-dev-server that will proxy all requests (other than Javascript/CSS) through to the Sitecore instance.

What this means is that developers can work on the project from wherever they like and not be restrained to Windows.  I have found that I can work entirely in macOS, using Visual Studio for Mac, with a slim Windows virtual machine running in Parallels.  Our gulp tasks copy views, binaries, configuration to the IIS instance in the virtual machine, and webpack-dev-server serves front-end assets (CSS, Javascript, etc...).  The only problem I have faced with this approach is debugging - there is no way of debugging remote applications from Visual Studio for Mac.

There has been some chatter around Sitecore moving to .NET Core, so hopefully, in the near future, we will not be constrained to Windows for developing and running Sitecore applications.

### Git submodules

We rely heavily on the use of Git submodule for sharing Foundation layer projects between solutions and for unifying the build scripts.

Git submodules allow us to target specific versions of a Foundation project based on a commit, leveraging the way the submodule mechanism works in Git.  This allows us to ensure that changes introduced to one solution won't adversely affect other solutions until fully tested and verified.

With the advances in the C# project file format where package references can be added to .csproj files (rather than using packages.config), we are able to build submodules that target multiple versions of Sitecore simultaneously.

### Helix CLI and module repository

We have developed a CLI package to simplify common tasks involved with Helix projects, such as creating new projects and importing common projects.

If you need to add a new feature layer project, instead of manually constructing the project in Visual Studio you can simply run `yarn helix new feature MyFeature` (or `npm`, if you prefer).

Coupled with the CLI is a module repository of well-known community-based modules.

# The future

We have come a long way since we started exploring the Helix architecture for Sitecore projects and have learnt a lot.  There are still many more advancements we would like to make to have an even more streamlined development process and an efficient, effective client experience.

A few of the future enhancements we will likely explore are discussed below.

### Moving views into a single location

At present we have our views (.cshtml) files scattered throughout our solution in a number of project, feature and foundation layer projects.  To simplify the development process - specifically from a front-end perspective - we will investigate creating a single "UI" project that essentially contains all the HTML markup alongside the Javascript and CSS.

### Creating an entry point project

The build and package process we currently use involves building the entire Visual Studio solution (.sln), then iterating through all foundation, feature and project layer projects then copying their App_Config, binaries, views, etc... (n.b. this differs from the base Habitat process where it utilises Web Deploy as discussed previously).  We will investigate creating a single entry point C# project that makes reference to all projects used in the solution then taking the binary output from only that project.  This should optimise build times and help resolve stray reference violations

### Virtualising the hosting environment

When front-end developers are tasked with working on Sitecore projects, there is always a steep setup cost involved, on newer projects with the discussed enhancements that cost has been drastically improved, but on some legacy projects, setup times can exceed a day to just get the project running.  We would like to find a way where starting work on a project is as simple as running a single command and having a full Sitecore environment ready to work on.  With Sitecore's alleged move towards .NET Core this could be achieved by using Docker, but in the interim, we will investigate hypervisor tools such as Parallels, Hyper-V and VirtualBox.