---
title: Umbraco Specification File
date: "2015-01-16"
template: "post"
draft: false
slug: "/posts/2015/umbraco-spec-file/"

tags:
- "programming"
- "asp.net"
- "umbraco"
description: "Umbraco is a powerful CMS that isn't overly intrusive.  It can work nicely side-by-side your web appliction providing a nice and easy way to manage dynamic content pages.  The latest version also has a nice fresh UI."
---
[Umbraco](http://umbraco.com/) is a powerful CMS that isn't overly intrusive.  It can work nicely side-by-side your web appliction providing a nice and easy way to manage dynamic content pages.  The latest version also has a nice fresh UI.

If I am starting a new project that's to be developed in the Microsoft environment and requires a CMS I will always push for Umbraco given it's price tag (free) and flexibility.

There is one flaw that it has, it's not unique to Umbraco, almost all CMSs suffer the same flaw.  The problem is maintaing multiple environments.

During development of an Umbraco site there is generally one central Umbraco database that all developers will work from, each making changes as needed to document types, the content tree, media, etc...

That's all fine until the site moves into the next stage of development.  Testing, staging, whatever you want to call it.  You generally end up with a copy of the original database.  Now you have two versions of the site running.  Developers pointing at their database, testing pointing at the testing database.

The issue I need to address is keeping in sync changes from this point forward.  If a developer wants to add a field to a document type, they need to add the field to their database, update their templates, make sure everything is working right and then deploy.  But to deploy, they need to manually add the field to the testing database and update the codebase.

A colleague and I were discussing this problem and comparing in general Windows development to non-Windows (i.e., Python, Ruby, etc...) development and what some features of the frameworks are.  He pointed out the fact that with [Django](https://www.djangoproject.com/) you specified the model in code and Django took care of migrations, etc... and I told him that [Entity Framework](http://msdn.microsoft.com/en-au/data/ef.aspx) does the same thing for database structures in .NET, but I never saw a connection between that and the issue I've been facing with CMSs.

The problem is keeping a single source of truth.  You can do it in the Umbraco admin portal, but trying to manage it between environments gets messy.  There are packages that can do it for you, but it depends on reading and writing changes to and from Umbraco as its running which can end up with losses of data, or the system getting out of sync.

What I propose is that instead of building the structure of Umbraco using the Umbraco interface, define it in an external Umbraco specification file.  This will basically be a seed file that will be the single source of truth.  It will contain all the document types, their fields, their relationship with each other (child/parent), permissions, even the document tree.  There will be a flag on document tree objects that specifies whether it's to overwrite what's already there, or just leave what already exists.

This will essentially do away with the *Developer* and *Settings* section of the CMS portal giving the developer necessary control in the specification file, and content editors will still have access the niceties that the Umbraco CMS portal has to offer.

The actual format of the file is still under consideration, but it will most likely be either YAML or JSON.  Knowing how large projects can get, there will be the option to construct the specification across multiple files (think LESS/SASS and `@import`).

There should also be a validation tool to allow a developer to quickly verify the specification and see any potential errors.

What I'm thinking is something like...

```json
{
    "project": "MyUmbracoApp.Web.UI",
    "author": "Brendan McKenzie",
    "docTypes": {
        "Base": {
            "alias": "base",

            "fields": [
                {
                    "alias": "metaTitle",
                    "name": "Meta Title",
                    "type": "shortText",
                    "mandatory": true
                },
                {
                    "alias": "metaDescription",
                    "name": "Meta Description",
                    "type": "shortText",
                    "mandatory": true
                }
            ],

            "children": [
                {
                    "alias": "content",

                    "fields": [
                        {
                            "alias": "title",
                            "name": "Title",
                            "type": "shortText"
                        },
                        {
                            "alias": "body",
                            "name": "Body",
                            "type": "markdown"
                        }
                    ],

                    "children": {
                        "@import": "contentChildrenDocTypes.json"
                    }
                }
            ]
        }
    },
    "tree": [
        {
            "alias": "home",
            "name": "Home page",
            "docType": "content",

            "fields": {
                "metaTitle": "My Website",
                "metaDescription": "My awesome website for...",
                "title": "Welcome to my website",
                "body": { "@import": "content/home.md" }
            },

            "children": [
                "..."
            ]
        }
    ]
}
```