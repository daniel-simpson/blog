---
title: Installing Sitecore 9 Manually
date: "2018-03-21"
template: "post"
draft: false
slug: "/posts/2018/installing-sitecore-9-manually/"
category: "Sitecore"
tags:
- "sitecore"
- "technology"
- "web"
- "development"
description: "All Sitecore documentation directs users to use the SIF or SIF-less tools to install Sitecore."
---
All Sitecore documentation directs users to use the SIF or SIF-less tools to install Sitecore.

This isn't a valid approach in certain circumstances such as CI pipeline builds or environments where installing Powershell modules is not possible/permitted.

Through a lot of wasted hours, hair pulling and odd feedback from Sitecore support I managed to get Sitecore up and running.

The situation I was dealing with was a hosting environment running Windows Server 2012 R2 that didn't allow me to install the SIF Powershell module.  I also had pre-existing certificates I wanted to use for client certificate authentication with xConnect.

My solution to this was to use the SIF tool to install Sitecore locally, then copy it up.  Instead of using SIF to do the installation locally, you could also download the "ZIP archive of the Sitecore site root folder" and work with that.

### Topologies

A short note on topologies as they were not explained in an obvious manner.

- __XP0__ refers to a "standalone" installation, this installs all of Sitecore XP on one instance and all Sitecore xConnect in one instance instead of breaking them up into their delivery/management/processing/reporting roles.  This is what you would most likely use during development.
- __XP1__ breaks XP0 into its smaller components.  This allows you to distribute the processing of Sitecore amongst multiple hosts rather than running everything on the one server.
- __XM__ is similar to XP1 in that it breaks the packages down, however it only includes the CD and CM components.

The topology I am working with in this installation is __XP0__.

## Installation

This is the process I followed.

1. Install SIF on your local development machine
2. [Install Java](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)
3. [Install SOLR locally](https://jermdavis.wordpress.com/2017/10/30/low-effort-solr-installs/)
4. Download the "Packages for XP Single" archive
4. Run SIF for [xconnect-solr.json](https://gist.github.com/brendanmckenzie/6603caf4d08f456fa427d6fd85d74ae3#file-xconnect-solr-ps1)
5. Run SIF for [sitecore-solr.json](https://gist.github.com/brendanmckenzie/6603caf4d08f456fa427d6fd85d74ae3#file-sitecore-solr-ps1)
6. Run SIF for [xconnect-xp0.json](https://gist.github.com/brendanmckenzie/6603caf4d08f456fa427d6fd85d74ae3#file-xconnect-xp0-ps1)
7. Run SIF for [sitecore-xp0.json](https://gist.github.com/brendanmckenzie/6603caf4d08f456fa427d6fd85d74ae3#file-sitecore-xp0-ps1)

At this point you should have Sitecore running at http://sitecore9-website/ and xConnect running at https://sitecore9-xconnect/ on your local machine.  The next step is to package this up and deploy it to a remote hosting environment.

1. [Backup and archive all the databases](https://gist.github.com/brendanmckenzie/6603caf4d08f456fa427d6fd85d74ae3#file-backup-dbs-sql) (prefixed with `SC90_`)
2. Archive the `C:\inetpub\wwwroot\sitecore9-website\` folder
3. Archive the `C:\inetpub\wwwroot\sitecore9-xconnect\` folder
4. Archive the `C:\solr\solr-6.6.2\server\solr\SC90_*` folders
5. Copy all these archives to their intended destination
6. Install your certificate on the servers that will run Sitecore and xConnect, ensure you're using a certificate that includes its private key (i.e., a p12/pfx certificate)
7. On the Sitecore XP server, extract the sitecore9-website archive to its destination
8. Create an IIS website pointed at that directory
9. On the xConnect server, extract the sitecore9-xconnect archive to its destination
10. Create an IIS website pointed at that directory
 * This website will need an SSL binding
 * This website will also need to be configured to handle client certificates
  1. Open IIS Manager
  2. Browse to the website
  3. Open SSL Settings
  4. Check the "Require SSL" box
  5. Change "Client certificates" to "Require"
11. [Restore all the databases](https://gist.github.com/brendanmckenzie/6603caf4d08f456fa427d6fd85d74ae3#file-restore-dbs-sql) on the database server
12. Update the `[__ShardManagement].[ShardsGlobal]` table in the `SC90_Xdb.Collection.ShardMapManager` database
 * The `[ServerName]` field will need to be updated
13. Update the connection strings in the sitecore9-website and sitecore9-xconnect websites
 * The xConnect connection strings in the sitecore9-website will need to be updated to point at the new sitecore9-xconnect site
14. Update the SOLR endpoint URL, this can be patched in to the `ContentSearch.Solr.ServiceBaseAddress` Sitecore setting

Now the websites should be running in their intended environment.  The next step is to setup the background xConnect services.

1. Download the [nssm](https://nssm.cc/download) tool on the server that will be running the services.
2. Update the ConnectionStrings.config file in the `sitecore9-xconnect\App_data\jobs\continuous\*` folders
3. Run `nssm.exe install "Sitecore XConnect IndexWorker" full-path-to\sitecore9-xconnect\App_data\jobs\continuous\IndexWorker\XConnectSearchIndexer.exe`
4. Run `nssm.exe install "Sitecore XConnect AutomationEngine" full-path-to\sitecore9-xconnect\App_data\jobs\continuous\AutomationEngine\maengine.exe`
5. Run `net start "Sitecore XConnect IndexWorker"`
6. Run `net start "Sitecore XConnect AutomationEngine"`

Finally, the Sitecore environment should now be running in a stable state.  In my instance the sitecore9-website folder will be dynamic and change on each deployment of the application; the original sitecore9-website folder will be used as a template where our updates will be deployed into.

The assumptions made for this process are below.

- Sitecore will be running at http://sitecore9-website/
- xConnect will be running at https://sitecore9-xconnect/
- SOLR will be running at https://solr:8983/solr/
- The database server will be running on the local machine
 - The database `sa` password is "password"
- The certificate used for client authentication is called "sitecore-certificate"

## Gotcha's

- Make sure you have no intermediary certificates sitting in your "Trusted Root Certification Authorities", [Thanks Dan](https://getfishtank.ca/en/blog/sitecore-9-xconnect-status-403-forbidden-certificate-error)
- Make sure the appropriate users have access to the private key of your certificate (lazy way would be to give "Everyone" access, less lazy would be to give "IIS_IUSERS" access)
- Not using SIF will mean that you have to manually configure the database sharding for xDB
- In environments outside production you may receive an error similar to below.  Ensure you have [SQL Server Data Tools in Visual Studio 2015](https://msdn.microsoft.com/en-us/mt186501.aspx) installed, as per the installation guide.  [Thanks Grant](https://grantkillian.wordpress.com/2018/01/03/sitecore-9-sif-webdeploy-gets-what-webdeploy-wants/)
- Ensure that "contained database authentication" is enabled. [Link](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/contained-database-authentication-server-configuration-option)

## Recommendations

- I am currently investigating the use of Docker (Windows Containers) for most of this.