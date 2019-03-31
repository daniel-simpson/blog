---
title: Clipboard Cleaner
date: "2012-11-28"
template: "post"
draft: false
slug: "/posts/2012/clipboard-cleaner/"
category: "Technology"
tags:
- ".net"
- "clipboard"
description: "You know what grinds my gears?  Long URLs, URLs littered with UTM tracking information, and YouTube URLs that contain more than they need - which is just the video ID."
---
You know what grinds my gears?  Long URLs, URLs littered with UTM tracking information, and YouTube URLs that contain more than they need - which is just the video ID.

Enter: Clipboard Cleaner!  It will monitor your clipboard, and when you copy a link that contains any of the aforementioned nuisances it will be cleaned and ready for pasting.

The application runs in the background, so running the `.exe` might appear to do nothing, but it does.  Once you've run it, copy ([this link: http://www.youtube.com/watch?v=QmMtIG0St64&feature=g-user](http://www.youtube.com/watch?v=QmMtIG0St64&feature=g-user)), then paste it somewhere.

Also, a big thanks to [Raminder Hundal](http://www.raminderhundal.co.uk/) for the logo!

Full [source code](https://github.com/brendanmckenzie/clipboard-cleaner) is available on GitHub and you can [download the executable here]({{ "media/blog/2012-11-28-clipboard-cleaner/ClipboardCleaner.exe" | prepend: site.cdn_root }}).