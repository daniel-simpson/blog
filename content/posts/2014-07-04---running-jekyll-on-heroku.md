---
title: Running Jekyll on Heroku
date: "2014-07-04"
template: "post"
draft: false
slug: "/posts/2014/running-jekyll-on-heroku/"
category: "Technology"
tags:
- "jekyll"
- "ruby"
description: "My website once was an ASP.NET MVC website that was very full featured.  I realised that most of the features weren't actually being used and I wanted to free up some spacing on my webhost."
---
My website once was an ASP.NET MVC website that was very full featured.  I realised that most of the features weren't actually being used and I wanted to free up some spacing on my webhost.

This lead me to start investigating alternatives to blogging platforms.  Wordpress seemed a little over the top and I didn't want to have to manage the website and server myself.  I wanted to be able to quickly and easily publish a blog post when I (rarely) want.

I started looking into GitHub pages, and it was great and had free hosting on custom domains.  It lead me to [Jekyll](http://www.jekyllrb.com) and static built websites. However there were two downsides:

 1. The source code to the site was entirely open.  Not that this really matters since there's no sensitive information contained within it, it's just not the greatest.
 2. It doesn't allow for plugins and collections aren't supported.  It appears to be running a version of Jekyll prior to 2.0 when collections were added.

Enter [Heroku](http://www.heroku.com), where those two issues were addressed.

I had a bit of trouble transitioning the site to run on Heroku (I'm not a Ruby dev and haven't paid too much attention to these technologies).  I ended up following [this article](http://mwmanning.com/2011/11/29/Run-Your-Jekyll-Site-On-Heroku.html), however there was one issue with it.  I followed "Method 1" since "rack-jekyll" required Jekyll <2.0, which brought me back to point 2 above.  The only change to what's in that article is what goes in the `Procfile` file. Instead of:

```gemfile
web: bundle exec jekyll --server -p $PORT
```

It should be

```gemfile
    web: bundle exec jekyll server --port $PORT
```

And that's it.  All the rest is valid.  This website is now entirely static content.  I even started using Amazon's CloudFront for hosting media files, more for the fun of it than because of traffic.