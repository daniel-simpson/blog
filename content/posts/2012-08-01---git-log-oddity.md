---
title: Git log oddity
date: "2012-08-01"
template: "post"
draft: false
slug: "/posts/2012/git-log-oddity/"

tags:
- "development"
- "git"
description: "I love git, nothing will change that.  I just came across some odd functionality today.  I use the command line client most of the time, though it's getting a bit tiring so I will probably switch back to using SmartGit again soon."
---
I love git, nothing will change that.  I just came across some odd functionality today.  I use the command line client most of the time, though it's getting a bit tiring so I will probably switch back to using [SmartGit](http://www.syntevo.com/smartgit/) again soon.

What I wanted to do was see the history on a specific file.  Let's say the root of my repository resides at `D:\Projects\Project\` and the file within the project is at `.\Content\css\site.css`, this is what I would have expected to work:

    > cd D:\Projects\Project\Content\css
    > git log site.css

Unfortunately, that wasn't to be.  The log came back empty.

After some toying around it turns out that trying to do a `log` on a file from it's directory does not work.  This was the solution:

    > cd D:\Projects\Project
    > git log .\Content\css\site.css

I'm not sure if this is a bug or expected functionality, either way, it's slightly perturbing.