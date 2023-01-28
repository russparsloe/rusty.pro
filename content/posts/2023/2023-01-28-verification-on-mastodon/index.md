---
title: Verification on Mastodon
date: 2023-01-28T17:11:36Z
tags: [ "mastodon", "website" ]
cover: 2023-01-28-verification-on-mastodon.jpg
coverAlt: Two mobile phones showing the Mastodon website
coverCaption: Mastodon is a free, open-source decentralized social media platform with nice people
useRelativeCover: true
---

With the demise of 3rd party Twitter clients such as [Tweetbot](https://tapbots.com/tweetbot/) (and with it my use of Twitter itself), I've started using [Mastodon](https://joinmastodon.org) as an alternative. One of the capabilities it offers is verification of links added to your profile. There are a couple of ways to do this, and I've settled on what I think is a nice clean method.<!--more-->

Mastodon itself recommends the use of anchor tags such as `<a rel="me" href="https://mas.to/@rustypro">Mastodon</a>` on the page you want to verify. This would require adding a link on my homepage. I could add it without text, or by using a non-breaking space, but that feels hacky.

Thanks to [Dave Barr](https://barrd.dev/article/add-a-verified-website-to-your-mastodon-account-using-link-tag/) I discovered you can use a `link` tag instead to achieve the same verifying effect without cluttering up a page with a hyperlink.

It then became a simple matter of adding `<link rel="me" href="https://mas.to/@rustypro">` to `layouts/partials/extended_head.html` in my site code and now I have a lovely checkmark on Mastodon to verify ownership of this site!

---

##### Cover photo by [Battenhall](https://unsplash.com/@battenhall) on [Unsplash](https://unsplash.com/photos/bQRqXz7mZe4)
  
