---
title: Sitecore 9 Prerequisites (SIF)
date: "2018-03-27"
template: "post"
draft: false
slug: "/posts/2018/sitecore-9-prerequisites-sif/"
category: "Technology"
tags:
- "sitecore"
- "sif"
description: "The prerequisites for installing Sitecore 9 using SIF are *technically* detailed in the installation guide.  However it's a bit obscure.  Here's a summarised list of additional packages that need to be installed to run the SIF installation tool for Sitecore 9."
---
The prerequisites for installing Sitecore 9 using SIF are *technically* detailed in the installation guide.  However it's a bit obscure.  Here's a summarised list of additional packages that need to be installed to run the SIF installation tool for Sitecore 9.

You'll need a server running Windows Server, ideally 2016+ but 2012 R2 will work __if__ you have Powershell 5+ installed.  IIS will need to be installed as well.

1. [Microsoft ODBC Driver 11 for SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=36434)
2. [Microsoft Command Line Utilities 11 for SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=36433)
3. [SQL Server Data Tools in Visual Studio 2015](https://msdn.microsoft.com/en-us/mt186501.aspx)
4. [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)
 * After installing Web Platform Installer, the following packages will need to be installed: UrlRewrite2, DACFX, WDeploy36PS, SQLDOM.  This command will run the installation for you. `C:\Program Files\Microsoft\Web Platform Installer\WebpiCmd-x64.exe /Install /Products:UrlRewrite2,DACFX,WDeploy36PS,SQLDOM,SMO_11_0 /AcceptEula`