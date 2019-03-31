---
title: Thoughts on D
date: "2014-07-17"
template: "post"
draft: false
slug: "/posts/2014/thoughts-on-d/"

tags:
- "d"
- "programming"
- "development"
description: "I have spent the last few days learning a bit of [D](http://dlang.org), I have [contributed to a library](https://github.com/brendanmckenzie/ddb), [written my own library](https://github.com/brendanmckenzie/scrypt) and developed a basic understanding of the language.  It comes across as a very powerful and developer-friendly language. However there are a few downsides to it."
---
I have spent the last few days learning a bit of [D](http://dlang.org), I have [contributed to a library](https://github.com/brendanmckenzie/ddb), [written my own library](https://github.com/brendanmckenzie/scrypt) and developed a basic understanding of the language.  It comes across as a very powerful and developer-friendly language. However there are a few downsides to it.

 1. Try searching (particularly Google - important) for anything related to "D", it's impossible.  The same issue existed for C# not so long ago, but now Google recognises the "#" symbol as not just noise to be ignored.  Searching for "write output to file in D" will return results for Python and C IO routines.  If you specify "dlang" you will be asked "Did you mean *golang*?" which I guess is fair enough since I'm using Golang's creator's website.
 2. There's a significant lack of libraries for fundamental operations.  I had to hack away at the ddb (PostgreSQL library) to make it accept BYTEA parameters.  The scrypt library relied on having an entire software platform installed instead of just a simple library reference.
 3. If I wanted to develop a large-scale application that would require more than just myself working on it I will have a hard time finding paid D developers to assist me.  Whereas Golang has the backing of Google so immediately gets a good reputation and following on that basis alone.

I spent the last few days playing with [vibe.d](http://www.vibed.org) and have enjoyed it, but I think for now, if I were to choose a technology to build a large system in, I'd have to go for something more mainstream.  I definitely will be keeping my finger on the D pulse and using it for smaller scale projects.