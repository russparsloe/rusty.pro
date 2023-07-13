---
title: Fixing RSS
date: 2023-07-01T17:36:22+01:00
tags: [ "hugo", "rss", "website" ]
cover: 2023-07-01-fixing-rss.jpg
coverAlt: Blue and red linked paper clips with one link broken
coverCaption: Fixing broken links in my RSS feed
useRelativeCover: true
---

One of the unintended effects of [automating the posting of blog post links](/2023/publishing-new-posts-to-mastodon) to Mastodon has led to the fix of a long standing issue I had with my RSS feed. As seems to be a recurring theme with running this blog, the fix was very simple, taught me more about the way Hugo works, and has delivered other benefits too.<!--more-->

While trying to get [Mastofeed](https://mastofeed.org/) to pick up my new posts, it reported that there were no links in my RSS entries. This was somewhat confusing because I have my feed enabled in [NetNewsWire](https://netnewswire.com) and posts with the correct links appear just fine. That being said, the cover images for my posts in NetNewsWire did not appear and displayed as broken images, suggesting something janky was happening with links in general.

## In Search Of Answers

I used `curl` to examine my [RSS XML](https://rusty.pro/index.xml) directly, taking specific note of the `<link>` value for an item. Here's a snippet of the output:

```xml
<channel>
    <title>Rusty.Pro</title>
    <link>https://rusty.pro/</link>
    ...

    <item>
        <title>Publishing New Posts to Mastodon</title>
        <link>/publishing-new-posts-to-mastodon/</link>
        ...
    </item>

    ...
</channel>
```

Hmmm... that doesn't look quite right. I'd expected the item link to be the full URL to the post, and not simply the path without the domain name. My assumption is that NetNewsWire is smart enough to know how to build the full URL by combining the channel link and the item link, but Mastofeed (and possibly other software) cannot. 

Time to go spelunking in the RSS generation code in `/themes/hello-friend/layouts/_default/rss.xml`:

```go
<item>
      <title>{{ .Title }}</title>
      <link>{{ .Permalink }}</link>
      ...
</item>
```

This tells me that the link value should be coming from Hugo's `.Permalink` value for the post. It's hard to find [documentation](https://gohugo.io/content-management/urls/#permalinks) to say exactly how permalink values are generated, but brief searching suggested they are supposed to be the full URL. Which defies what I see in the rendered RSS. So what is the missing link?

## I'm All About That Base (URL)

The missing piece is the `baseURL` config parameter. Hugo takes this value, appends the URL path and BOOM - that's your permalink value. 

When I set up my site config originally, I copied the one offered in the hello-friend theme readme, which sets `baseURL = /`. This is why my `.Permalinks` are generating the link above of `/publishing-new-posts-to-mastodon/` - I'd pretty much told Hugo that my domain name is "/" 🤦‍♂️.

The fix then becomes very simple. The `baseURL` value should be set to **the absolute URL (protocol, host, path, and trailing slash) of your published site**. Updating my config to set `baseURL = "https://rusty.pro/"` changed the item links in my RSS feed to the full URL as required:

```xml
<item>
      <title>Publishing New Posts to Mastodon</title>
      <link>https://rusty.pro/2023/publishing-new-posts-to-mastodon/</link>
      ...
</item>
```

As a result, Mastofeed is now able to detect links to my new posts and publish them to Mastodon!

## Bonus Prizes

Changing `baseURL` has had other unintended improvements. The cover image now appears in NetNewsWire where it just displayed the broken image before. 

It seems that while NetNewsWire was able to construct the full links to my posts with the previously incorrect config, it could not do the same for images in the `description` field. Now images have their full path and show as intended!

I had worried that by hardcoding the `baseURL` in my config to the value of the public DNS name of the site, it would cause local testing to break in some way. In actual fact, Hugo is smart enough to replace the domain and port with `localhost:1313` when running `hugo server` on my computer so all links work locally as expected. It even displays the correct link in the terminal so I can click on to open the site in my browser!

## Learnings

What turned out to be a simple configuration change has had a "ripple" effect of touching upon a few areas of this website. Although this site is relatively simple, I realise that Hugo is a powerful tool that needs care and attention to work as desired. 

Slowly I am converging on a setup that works well for my needs, and had fun learning more about Hugo along the way!

---

##### Cover photo by [Jackson Simmer](https://unsplash.com/@simmerdownjpg) on [Unsplash](https://unsplash.com/photos/Vqg809B-SrE)
  