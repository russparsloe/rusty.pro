---
title: Archetypes Are Really Useful
date: 2022-12-26T10:04:00Z
tags: ["hugo", "website"]
cover: 2022-12-26-archetypes-are-really-useful.jpg
coverAlt: Person Using a Cookie Cutter
coverCaption: Having an easily repeatable pattern removes friction from a task
useRelativeCover: true
---

One of the reasons I feel have failed to blog at all over the past 4 years is that the barrier to entry was too high. Rather than focusing on writing content, I would spend lots of time trying to remember how to use the tools, get frustrated, and give up. Some of this friction can be removed with a handy Hugo feature called Archetypes.<!--more-->

There are many pages that describe the benefits and how to use archetypes so I won't try to cover them again here. One page that I found that really helped me to understand how they worked was written by [Bruce Wray on CloudCannon](https://cloudcannon.com/blog/maximizing-the-convenience-factor-archetypes-in-hugo/).

By creating an archetype, it makes it easier and faster for me to get the outline of a post ready to go, and then I can focus more of my time on writing the actual content.

A couple of things I needed to be mindful of when creating my archetype were:

- I am using [Leaf Bundles](https://gohugo.io/content-management/page-bundles/#leaf-bundles) for my pages
- My folder/file naming structure uses the format `posts/yyyy/yyyy-MM-dd-page-title`, whereas the title should appear using the format `Page Title`

The first is easy enough to deal with. Hugo has support for [directory based archetypes](https://gohugo.io/content-management/archetypes/#directory-based-archetypes), so I just made sure to save my file with the path `/archetypes/posts/index.md`.

The second is a little more involved, but also relatively simple once you realise Hugo supports a number of functions that can be linked together to manipulate text. I used [`slicestr`](https://gohugo.io/functions/slicestr/) to remove the 11 character date portion from the `.Name`, [`humanize`](https://gohugo.io/functions/humanize/) to turn the hyphens into spaces, and finally [`title`](https://gohugo.io/functions/title/) to convert the text to title case.

As I post more, I'll learn what I need (and what I don't) in my archetype but here's what I settled on for now.

```go
---
title: {{ slicestr .Name 11 | humanize | title }}
date: {{ .Date }}
tags: [ "hugo", "website" ]
cover: {{ .Name }}.jpg
coverAlt: Cover Alt Text
coverCaption: Cover Caption
useRelativeCover: true
draft: true
---

---

##### Cover photo by
```

With this in place, the command I used to create this post was:

> `hugo new posts/2022/2022-12-26-archetypes-are-really-useful`

This resulted in this ready to edit file being created with most of the boilerplate stuff in place:

```toml
---
title: Archetypes Are Really Useful
date: 2022-12-26T10:04:00Z
tags: ["hugo", "website"]
cover: 2022-12-26-archetypes-are-really-useful.jpg
coverAlt: Cover Alt Text
coverCaption: Cover Caption
useRelativeCover: true
---

---

##### Cover photo by
```

This should dramatically speed up the initial part of the blog writing process, and hopefully lead to more posts!

---

##### Cover photo by [Nicole Michalou](https://www.pexels.com/photo/person-using-a-cookie-cutter-6061742/)
