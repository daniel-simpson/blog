---
title: Git and Powershell 
date: "2012-09-12"
template: "post"
draft: false
slug: "/posts/2012/git-and-powershell/"
category: "Technology"
tags:
- "git"
- "powershell"
description: "Git is an awesome piece of software, not just for developers working in large teams, but also for individual developers. I have projects where I can track the entire history of it via it's Git repository and most of the time I'm working alone. I have had issues working with other developers who haven't used it as much as I have, but we've always worked through it."
---
Git is an awesome piece of software, not just for developers working in large teams, but also for individual developers. I have projects where I can track the entire history of it via it's Git repository and most of the time I'm working alone. I have had issues working with other developers who haven't used it as much as I have, but we've always worked through it.

I started off using Git via [SmartGit by Syntevo](http://www.syntevo.com/smartgit/), which is free for non-commercial use. This was a great way to get used to the way Git worked. For a (very) brief period I tried TortoiseGit as I came from the SVN playground and thought it would be comparable to TortoiseSVN, alas, that was not the case.

After a while I started playing with git-bash and it wasn't too long before I (for the most part) ditched SmartGit, when it comes to tricky merge conflicts I prefer the GUI that SmartGit has but for everything else it's all command line.

Not too long after that I found [Phil Haack](http://haacked.com/)'s [post on using Git in PowerShell](http://haacked.com/archive/2011/12/13/better-git-with-powershell.aspx), it works really well, gives great feedback to what you're doing and is a very useful module for PowerShell.

Then a little later I came across [this post](http://nvie.com/posts/a-successful-git-branching-model/) which is a great guideline on successful branching with Git. Before reading this I generally worked with two branches: `master` and `development`, which for the most part works just fine. But for keeping track of versions and making the repository history flow more nicely you need more than that.

It took a little adapting but after a while it just became second nature to use this model for branching, and I realised there were a few commands that I was repeating that could be simplified by using PowerShell aliases.

So I give to you, my [Git PowerShell aliases file]({{ "media/blog/2012-09-12-git-and-powershell/git-helper.ps1" | prepend: site.cdn_root }}).  All it does is simplifies the git commands into shortcuts.  If you want to see what's available, just load the `.ps1` and type `g<enter>`.

Add it to your PowerShell profile by typing `notepad $profile` in PowerShell and adding the line `. path\to\git-helper.ps1`

Since I work in the office and at home and I wanted these shortcuts to be available to me wherever I am: I put the [file]({{ "media/blog/2012-09-12-git-and-powershell/git-helper.ps1" | prepend: site.cdn_root }}) into my [SkyDrive](http://skydrive.live.com/), and load it in my PowerShell profile on both PC's.

Here it is in action...

![Powershell with Git Extensions](//images.contentful.com/olq6un8g3480/3MC9z04K7Yi4wo8UoksKMK/44d27c26ca793ce8544c283b96c3cbdb/git-powershell-example.png)