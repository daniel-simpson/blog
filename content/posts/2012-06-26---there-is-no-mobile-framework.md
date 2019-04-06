---
title: There is no mobile framework
date: "2012-06-26"
template: "post"
draft: false
slug: "/posts/2012/there-is-no-mobile-framework/"

tags:
- "mobile"
- "css"
- "development"
description: "When it comes to developing websites for mobile devices, there is no set framework.  There are tools, helpers, quasi-frameworks, but there is no specific *framework* for developing these applications."
---
When it comes to developing websites for mobile devices, there is no set framework.  There are tools, helpers, [quasi-frameworks](http://jquerymobile.com/), but there is no specific *framework* for developing these applications.

What a lot of web developers/designers tend to do is ignore the fact that what they're actually doing is developing a website, exactly the same way as they would any other website and get sidetracked by the idea that they're designing a *mobile* website instead of just designing a website that's accessible from a mobile devices.

I've taken care to try and make my website, this website, as mobile friendly as possible.  I didn't sit there when I was putting together the data model thinking "I better be careful how I design the data model for this website since I'm hoping to have visitors hit it from a mobile device."  I designed the data model exactly as I would have regardless of the medium on which it's accessed.  What back-end is running my website (be it Python, ASP.NET, PHP, Java, node.js, whatever..) it doesn't make a difference to how it's consumed by the browser; at the end of the day, it's all just HTML and CSS.

Don't let people throw you by asking about [HTML5](http://www.html5rocks.com/en/).  HTML5 is just a newer version of HTML, the markup language that has been used since the dawn of the internet.  It brings in a few new tags (`<canvas />`, `<audio />`, `<video />`, are the most significant ones - to me), and the `data-*` attribute which helps with JavaScript interaction.  That's it, there's nothing else you need to worry about.

All it took to make my website friendly for mobile devices was adding a few extra lines of CSS.  I made the somewhat safe assumption (unless you're looking to support Windows Phone 5) that all mobile devices hitting my website will be CSS3 compatible (iPhone, Android, WP7, etc...).  CSS3 supports media queries, that is having CSS that differs based on the type of media the document is being presented; it's actually something that has always been there, you could specify a `media="print"` on your `<link />` tag to pull in a different stylesheet to be used when printing.  CSS3 media queries work much the same way.  If you take a look at the CSS of my website you will be able to see (sorry it's a bit hard to read, it's compressed for optimisation not obfuscation!) and you'll see down the bottom where I resize/hide elements based on the browser dimensions.

The two ways of using media queries is to embed them in the same stylesheets you use across your site, for example...

    @media only screen and (min-width : 321px) {
      /* Styles */
    }

The alternative is to only include the stylesheet when the media query is matched, like so...

    <link rel="stylesheet" type="text/css" href="mobile-styles.css" media="only screen and (min-width : 321px)" />

A few websites that came in handy when putting this website together...

* <http://css-tricks.com/snippets/css/media-queries-for-standard-devices/> - gives you the media queries you'd probably want to use
* <http://html5boilerplate.com/mobile> - my favourite HTML5 boilerplate for mobile devices (has stylesheets already prepared with media queries)
* <http://google.com/webfonts> - mobile devices tend to render these web fonts a bit nicer than desktops

Actually developing the websites isn't hard either, once you have the media queries in place, open up your [favourite browser](http://google.com/chrome) and shrink it down to roughly the width of a mobile device.  Once you're satisfied with how it looks, give it a run through on an actual mobile device.

And for no other reason than to add a bit of colour, here are some photos from my travels. :)

<p style="text-align:center">
<img src="https://farm6.staticflickr.com/5339/7437654846_219d4e6c57_q.jpg" />
<img src="https://farm8.staticflickr.com/7136/7436254430_8a7af6fa04_q.jpg" />
<img src="https://farm6.staticflickr.com/5319/7436305836_4856a4e692_q.jpg" />
</p>