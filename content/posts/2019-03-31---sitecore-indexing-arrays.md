---
title: Sitecore indexing arrays with Azure Search
date: "2019-03-31"
template: "post"
draft: true
slug: "/posts/2019/sitecore-indexing-arrays-with-azure-search/"
category: "Sitecore"
tags:
- "sitecore"
- "development"
- "web"
description: "Overcoming an issue with indexing lists of data on Azure Search"
---
A lot of our projects are built upon the Habitat framework.  Admittedly, in the early days we blindly copy-pasted the Habitat foundation-layer projects into our solutions.

Most projects we deploy into AWS or on-premesis infrastructure.  One project we came across the client wanted it deployed into Azure using the full Azure stack.  One notable difference here is the use of Azure Search over Solr.

The Habitat Foundation.Indexing project includes a custom field for indexing "all_templates" - a combination of all the templates the current item is comprised of.

This custom field processor, [AllTemplatesComputedField](https://github.com/Sitecore/Habitat/blob/release/8.2/src/Foundation/Indexing/code/Infrastructure/Fields/AllTemplatesComputedField.cs#L30-L32), returns `List<string>` which turns out to be an issue when it comes to Azure Search.  In Lucene/Solr environments this works as expected.  When deployed into Azure Search environments, only the first entry in the array is stored.

The solution, though it took some time to find, was a simple one.

Convert the `List<>` to an array and all was resolved.
