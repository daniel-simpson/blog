---
title: Going Serverless
date: "2016-06-07"
template: "post"
draft: false
slug: "/posts/2016/going-serverless/"
category: "Technology"
tags:
- "aws"
- "serverless"
- "concepts"
- "lambda"
- "contentful"
description: "I work for a digital agency - [Deepend](http://www.deepend.com.au).  We primarily build and maintain content managed websites for clients.  We are platform and technology agnostic meaning we deal with a lot of different programming languages, operating systems and databases.  That's great for me because it gives me the freedom to play with a whole assortment of toys."
---
I work for a digital agency - [Deepend](http://www.deepend.com.au).  We primarily build and maintain content managed websites for clients.  We are platform and technology agnostic meaning we deal with a lot of different programming languages, operating systems and databases.  That's great for me because it gives me the freedom to play with a whole assortment of toys.

Although agnostic most of our sites fit into either PHP or .NET.  With PHP it's generally Wordpress and .NET it's either Umbraco, Kentico or Sitecore.

Having worked in this space for some time it was hard for me to envision other ways of building websites.

Enter Amazon Web Services (AWS).

I've known about AWS basically since it begun but aside from using it to run virtual servers (EC2 instances) I never really paid much attention to what else it had to offer, I knew there was a whole lot of services but never really had the drive to try them out.

That is until the AWS Summit conference I attended earlier this year in Sydney.

The one session that stood out above all the rest was one where a company had gone entirely server-less.  They run an online training service with videos and tests.  They went on to explain how it all worked and inspired me to work on implementing that to solve problems for our clients.

What I have built so far is a single AWS Lambda function that takes input from Contentful, looks up configuration, generates HTML based on dotjs templates and outputs it to an S3 bucket that can be distributed behind a Cloudfront distribution.

Ultimately scalable, and zero-downtime.  Globally accessible.

What I intend on doing with this is turning it into a lightweight service that can be used by others.

Given that the output is all static HTML, how do you have dynamic sections? React, AngularJS, Knockout, Ember, etc... you just need to structure your application so that all dynamic content is rendered on the front-end powered by back-end APIs.