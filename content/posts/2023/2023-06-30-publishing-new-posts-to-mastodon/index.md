---
title: Publishing New Posts to Mastodon
date: 2023-06-30T18:14:19+01:00
tags: [ "hugo", "website", "mastodon" ]
cover: 2023-06-30-publishing-new-posts-to-mastodon.webp
coverAlt: A clipboard with a bullet list of tasks to publish a blog post next to a MacBook
coverCaption: Automation can help reduce the friction when publishing a new post
useRelativeCover: true
---

An thought struck me when browsing Mastodon yesterday - how can I automate the posting of a link to my new blog posts on my Mastodon account? While this took me on something of a journey to find what options exist, the actual solution I landed upon is very straightforward.<!--more-->

## The Challenge

The idea I wanted to implement was simple. Every time I publish a new post on this blog, automatically post a message with its title and link to my Mastodon account. My desire to do this is almost entirely technical - satisfying my problem solving needs - more than any social media strategy I may have.

I've used [IFTTT](https://ifttt.com) in the past to achieve similar things. IFTTT used to be entirely free, and while there is still a free tier, it is severely limited in the number of automations you can have. I looked to see if there were any alternative well-known services  that had a more generous free tier, but if anything it was worse. [Zapier](https://zapier.com) is the other big name in this space, and their Webhooks service is classified as Premium which means on their free tier, it would not be available. My needs are meagre, so to pay to use a fraction of what these services offer doesn't seem worth it.

Continuing to look for alternatives, I stumbled across [Actionflows](https://actionsflow.github.io) that uses GitHub Actions to create automated workflows. It's something I would like to explore more, but there is lots to learn and consider, and given my use case is quite simple, I decided to keep looking.

The last option I considered was to write something myself and run it locally on my laptop. The [Mastodon API](https://docs.joinmastodon.org/client/intro/) is well documented with good examples, but this feels quite manual and brittle. I don't want to have to think about running an additional job when creating a post.

## The Solution

Close to the point I was about to give up, I saw mention of [Mastofeed](https://mastofeed.org). This is a web service that does one thing - take new items discovered in a specified RSS feed and post them to your Mastodon account. Perfect!

Having found the perfect solution, I was a bit hesitant to use it. The homepage for the service is devoid of any information about who created the service. I was again about to give up when I happened to stumble across a link to a Mastodon post from it's creator [Alex Barredo](https://mastodon.social/@barredo). A little further digging and I discovered this [About](https://mastofeed.org/?s=about) page that you wouldn't normally find until you had logged in.

I plan to contact Alex with some feedback on how to improve the service, as while niche, I can see it being very useful to others!

## The Proof Of The Pudding

With my account set up, I've written this post with the sole purpose to test how well it works as soon as I publish it! Wish me luck! 🤞

---

##### Cover photo by [Markus Winkler](https://unsplash.com/@markuswinkler) on [Unsplash](https://unsplash.com/photos/5ofa31FPKYY)