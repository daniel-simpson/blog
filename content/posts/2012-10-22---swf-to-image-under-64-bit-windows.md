---
title: SWF to Image under 64 bit Windows
date: "2012-10-22"
template: "post"
draft: false
slug: "/posts/2012/swf-to-image-under-64-bit-windows/"
category: "Technology"
tags:
- "32-bit"
- "windows"
- "swftoimage"
description: "This is definitely a reminder post for myself.  Twice now I have fallen victim to issues working with 32-bit COM libraries running under ASP.NET websites under Windows 64-bit. The main issue in this case was a library used by a legacy app that had to be ported from an older server to a newer one."
---
This is definitely a reminder post for myself.  Twice now I have fallen victim to issues working with 32-bit COM libraries running under ASP.NET websites under Windows 64-bit. The main issue in this case was a library used by a legacy app that had to be ported from an older server to a newer one.

The library is SWFToImage, was (discontinued support) a piece of software by [ByteScout](http://bytescout.com) that converts a flash file into a JPEG. I won't go into the reasons and requirements of such a library but here are the simple steps to make it work.

 1. Install [Flash Player v11.x ActiveX control content debugger](http://www.adobe.com/support/flashplayer/downloads.html)
 2. Enable 32-bit applications in the App Pool your website is running in under IIS
 3. regsvr32.exe the SWFToImage.dll

And that's it.