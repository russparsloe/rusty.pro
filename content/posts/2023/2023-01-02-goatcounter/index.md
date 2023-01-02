---
title: GoatCounter
date: 2023-01-02T14:59:28Z
tags: [ "hugo", "website" ]
cover: 2023-01-02-goatcounter.png
coverAlt: A sample of analytics from GoatCounter
coverCaption: GoatCounter is an open source privacy-friendly web analytics platform
useRelativeCover: true
---

I haven't really told anyone about this blog as it's more of a project to give me somewhere to do something technical rather than a place I want to drive traffic to. Even so, as I write more content, it would be nice to see more traffic  arrive organically at the site. To track how this grows over time, I've enabled [GoatCounter](https://www.goatcounter.com) on the site...<!--more-->

Besides having a great name, I am a fan of [why](https://www.goatcounter.com/why) it was created. Google Analytics is the most popular tool in this space, but its overkill for my needs, as well as having concerns around privacy. GoatCounter is much simpler and has enough information for me to track how traffic to the site is growing. 

Most free tools require you to self-host and maintain the server component, which I want to avoid. Most hosted SaaS tools have paid-for entry tiers that are expensive for a tiny site like this one. GoatCounter is offered as SaaS that is free for non-commercial use. It is the perfect combination!

To add it to the site, I needed to add a small piece of code to every page:

```html
<script data-goatcounter="https://rustypro.goatcounter.com/count"
        async src="//gc.zgo.at/count.js"></script>
```

Thankfully the `hello-friend` theme makes it very simple to add this code by placing it in the `/layouts/partials/extended_footer.html` file.

Easy as that!

---

##### Cover photo by [GoatCounter](https://www.goatcounter.com)
