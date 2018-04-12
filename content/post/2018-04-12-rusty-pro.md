---
title: "Rusty.Pro - or how I host a robust, cutting edge website for just $2"
date: 2018-04-12T21:29:01+01:00
draft: false
tags: [ website, hugo, namecheap, netlify, mailgun ]
slug: "rusty-pro"
---
Welcome to my tiny corner of the web! I've wanted a place to put my learnings online for a good while, and with time on my hands to finally do it, this is the outcome. <!--more-->

I haven't had a website for over a decade, and so with a blank slate I looked at the current options available. I've used [Wordpress](https://wordpress.org) in the past with it's famous 5 minute install. Although it's a great platform, it feels a little "heavy" for a tiny site like mine. Managing version updates, plugins, and a database would add management overhead that I just don't have time for. Also Wordpress is a dynamic site, meaning content has to be pulled from the database and generated on the fly for every page view, which creates a performance hit. There are some mitigation strategies such as using caching plugins, but this is yet another thing to manage.

While dynamic website have their place, there is a growing tendancy to switch back to static webpages, that are pre-generated, making them fast to load (it's just plain HTML and Javascript). And there are mature tools which allow you to create a template, and merge it with content, which gives you many of the benefits of dynamic sites without many of the drawbacks.

After looking at many of the options available today, enter [Hugo](https://gohugo.io). Written in Go from the ground up, Hugo is a fast and flexible static site generator, and while newer than some alternatives, has developed a large community and a has large number of themes available. Content can be written into plaintext files in [Markdown](https://en.wikipedia.org/wiki/Markdown), which can then be version controlled in Git.

After going backwards and forwards for an age, I settled on the theme [Kiss](https://github.com/ribice/kiss/) by [Emir Ribic](https://www.ribice.ba/). I even spotted an issue, raised a PR on GitHub and I'm now officially a contributor!

Now I had the ability to create a site, I needed a way to host it online. Here are the steps I took to make that happen, and for almost zero cost.

**Domain name** - Namecheap ($2)

One of the hardest parts of this whole endeavour was choosing a suitable domain name! I wanted it to be short enough to remember, easy to spell, and of course, it had to be witty. I think I hit 2 out of 3 and Rusty.Pro describes me pretty well! I'd heard good things about [Namecheap](https://www.namecheap.com/) and for the princely sum of $2, I got the domain for a year.

**Hosting** - Netlify (Free)

I originally considered using [GitHub pages](https://pages.github.com/), especially as the source code for the site lives in GitHub. This would mean pulling code from GitHub, building the site locally, and then re-pushing the branch back with the static HTML in the correct directory. There was also a few caveats to this, so I carried on my search and discovered the incredible [Netlify](https://netlify.com).

Netlify allow you to connect to a git repository on GitHub, and every time a new change is pushed to the repo, Netlify will invoke Hugo, build the site, and then host it for you on their CDN network. They can generate a SSL certificate so people can browse your site securely and they also manage your DNS records for you. And they have a free plan for all of this. It's truly incredible!

**Email** - Mailgun (Free)

The only thing that Netlify don't offer, is any kind of email management. This is something you need to provide yourself. I considered a number of free email hosts, or even a Google Apps account, but having another email system to manage is something I wanted to avoid. Enter Mailgun. Using their servers, you can create mail routes to forward email to an existing account. They offer powerful routing to create different rules for different email aliases, as well as a catch all option. The account is free for up to 10,000 emails per month, overkill for my site. My experience using them so far has been excellent, and the support I received for a couple of minor issues I had has been first rate.

**Comments** - Disqus (Free)

Although I don't expect (m)any comments on this site, one of the things that is more challenging with static pages, is the ability to provide a function for people to leave comments. Fortunalely Hugo provides first rate support for [Disqus](https://disqus.com/), the most popular comment plug-in available. They offer a couple of free options. For small, ad-free, non-commercial sites such as mine, they offer a generous "Plus" plan for free. It's got some really nice features, and I no longer have to worry about managing comments.

So there you have it. By leveraging some really great online services, I have a robust, fast and modern website for minimal cost. Leave a comment below if there's anything else you'd like to know, and welcome!