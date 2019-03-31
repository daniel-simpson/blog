---
title: Playlist script for ices
date: "2009-06-18"
template: "post"
draft: false
slug: "/posts/2009/playlist-script-for-ices0/"

tags:
- "old"
description: "I use ices0 + icecast to stream my music to me all over the globe.  I created a python script to build generate the playlist of songs that are played."
---
I use ices0 + icecast to stream my music to me all over the globe.  I created a python script to build generate the playlist of songs that are played.

Create a folder `/var/ices` and put in it a file called `cur-pl` and `playlist.txt`

cur-pl should contain:

    [location of playlist file]  [play-type]  

Where `[location of playlist file]` is the play text file with a list of music files.

And `[play-type]` is either `'normal'` or `'random'`

    File resource missing