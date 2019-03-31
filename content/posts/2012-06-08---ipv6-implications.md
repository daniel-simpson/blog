---
title: The implications of IPv6
date: "2012-06-08"
template: "post"
draft: false
slug: "/posts/2012/ipv6-implications/"

tags:
- "ipv6"
- "internet"
description: "Today I was tasked with answering a customer query regarding IPv6 and whether it will have any impact on their website.  I initially wasn't sure how to address this, but did my best to respond."
---
Today I was tasked with answering a customer query regarding IPv6 and whether it will have any impact on their website.  I initially wasn't sure how to address this, but did my best to respond.

This is what I wrote...

> The "launch" (the IPv6 specification was published in 1998) of IPv6 will not impact any of our websites.  Currently all domains are mapped to IPv4 addresses, via DNS (essentially the core of how anything on the internet works), to "support" IPv6 all we would need to do is have the IPv6 addresses allocated by our provider to our servers (which will function alongside IPv4 with no issues) and add to our DNS records.  That way when a client comes along that supports IPv6 it will find our servers IPv6 address and connect via that, instead of IPv4.
>
> A little background…
> When you open a web browser and type in an address (say `www.example.com`) what happens is the computer goes off to a DNS server which is setup on your computer and looks up the IP address of that domain.  First it finds `example.com` then queries the `A` records associated with the domain and finds where `www.example.com` points.  Once found the browser connects to that address on port 80 and issues the necessary HTTP requests to get the content of the webpage.  After the initial lookup the IP address is cached so that a call to the DNS server is not necessary every time a connection is required.
>
> With IPv6, what the client will do is query the DNS server for the `AAAA` record of `www.example.com` and if found, it will use connect to the server using the IPv6 address (which is in the format of `xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx`) still on port 80.
>
> As operating systems and service providers update their software and hardware users will be able to connect using IPv6.  To everyone involved, except for the person here who manages DNS, no action is required.  Simply once we have IPv6 addresses allocated, the DNS will be updated and that will be it.
>
> However, I must reiterate that even if we did nothing for the next few years there will be no impact.  Think of it like how they phased out analogue TV and cell phones, but over a much longer time frame.

I felt that adequately answered the customer's question and even helped me gain a better understanding of something I knew but didn't know why I knew.