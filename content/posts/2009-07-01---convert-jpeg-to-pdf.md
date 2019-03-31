---
title: Convert a JPEG image to PDF document
date: "2009-07-01"
template: "post"
draft: false
slug: "/posts/2009/convert-jpeg-to-pdf/"

tags:
- "old"
- "domino"
- "notes"
- "java"
- "jpeg"
- "pdf"
description: "I had the requirement to export data to a PDF document recently, which involved plotting data from a Domino database over an map that was stored in JPEG format."
---
I had the requirement to export data to a PDF document recently, which involved plotting data from a Domino database over an map that was stored in JPEG format.

The process I took was this:

1. Extract the map from the Domino document to the file system
2. Load the map in a Java agent using the java.awt.* package
3. Plot the data on the map image
4. Save the changes to the JPEG image on the file system
5. Load the JPEG image again
6. Slice the JPEG image into "pages"
7. "Print" the sliced JPEG images into a PDF document
8. Save the PDF document to the file system
9. Use accordingly

I use step 5 because I built a custom script library to do the processing from that point forward so it seemed logical for code reusability to store the changes to disk.

Attached is the code for the script library to do the JPEG to PDF conversion.

It relies on an open source Java library freely available on the internet called gnujpdf.  [Google it](http://www.google.com/), or [click here](http://gnujpdf.sourceforge.net/).

    File resource missing