---
title: Unique file name
date: "2013-01-04"
template: "post"
draft: false
slug: "/posts/2013/unique-file-name/"

tags:
- "csharp"
- ".net"
description: "I came across a curious piece of code as I was working my way through the project I work day-in-day-out on; not that curious pieces of code [are rare](http://bad-code.com) in this project."
---
I came across a curious piece of code as I was working my way through the project I work day-in-day-out on; not that curious pieces of code [are rare](http://bad-code.com) in this project.

This one made me stop and think.  I knew it was wrong, but how could I make it right?  The problem is how to determine a unique filename in a directory, say for example if I wanted to allow users to upload images which would be stored in a folder, I don't want to overwrite existing files and I don't want to use the filename of the uploaded file.

Here's the code I came across.

    int count = 1;
    while (count < 1000)
    {
        string tmp = Path.Combine(this.ImagesPhysicalFolder, modifiedFileName) + count.ToString() + ".jpg";
        if (!File.Exists(tmp))
        {
            modifiedFileName = tmp;
            break;
        }
        ++count;
    }

It's a little verbose, and calling the `Path.Combine()` inside the loop could be costly.  This is the solution I came up with.

    var root = ...;

    /* snip */

    var count = 0;
    var template = Path.Combine(root, "file_%%.jpg");
    var filename = template.Replace("%%", (count++).ToString());
    while (File.Exists(filename))
    {
        filename = template.Replace("%%", (count++).ToString());
    }