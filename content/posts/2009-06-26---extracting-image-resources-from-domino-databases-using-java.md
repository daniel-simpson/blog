---
title: Extracting image resources from domino databases using Java
date: "2009-06-26"
template: "post"
draft: false
slug: "/posts/2009/extracting-image-resources-from-domino-databases-using-java/"

tags:
- "old"
- "domino"
- "notes"
- "java"
description: "I had the necessity to extract an image that is embedded in the database an a resource out to the file system."
---
I had the necessity to extract an image that is embedded in the database an a resource out to the file system.

What ensued was a lot of fun with DXL, XML and Base 64 encoding.

In the end it's a pretty simple process.

1. Find the NoteID for the image resource
2. Build the DXL export collection
3. Export the DXL
4. Parse the DXL XML file
5. Locate the Base 64 encoded image in the XML
6. Decode the Base 64 encoded image
7. Write the decoded image to disk
8. Use accordingly

Attached is the Java code to perform the above (step 8 excluded).

There are 3 parameters to the main function (`ImageResourceExtractor.extract()`).

1. The Lotus Notes session (in an agent's main body this is simply `getSession()`)
2. The name of the image resource you want to extract
3. Where you want the image resource to be extracted to

The function returns a `java.io.File` object pointing to the newly exported file.

Enjoy!

    File resource missing