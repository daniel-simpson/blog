---
title: Global Printers  
date: "2009-04-14"
template: "post"
draft: false
slug: "/posts/2009/global-printers/"

tags:
- "old"
- "windows"
- "microsoft"
- "printers"
description: "Recently I have been trying to add a printer on a server available to all users, using the add printer wizard with no luck."
---
Recently I have been trying to add a printer on a server available to all users, using the add printer wizard with no luck.

It turns out that the add printer wizard only adds printers for the current user and there are no options to make this stick for all users.

I came across this site that solves that issue using the PrintUI.dll.

<http://members.shaw.ca/bsanders/NetPrinterAllUsers.htm>

Heaven forbid that website disappear, attached is the contents of a batch file that will do that which is required.

    File resource missing

Usage

    AddGlobalPrinterRemotely.cmd <client computer> <print server>\<shared printer name>