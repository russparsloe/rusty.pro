---
title: "Sweating the Small Stuff - Part 1"
date: 2022-12-25T17:55:47Z
tags: ["website"]
cover: 2022-12-25-sweating-the-small-stuff-part-1.jpg
coverAlt: A sign saying sweat
coverCaption: Sweating the Small Stuff makes all the difference
useRelativeCover: true
---

I am much more enthusiastic about this site since the theme change! I would say it satisfies about 95% of what I would have created myself had I the skills to do so!

There are a few things I would like to change to take care of that final 5%. Here is how I tackled a couple of them.<!--more-->

## Post Excerpts

The first is how excerpts for posts are created on list pages. The [code](https://github.com/panr/hugo-theme-hello-friend/blob/95a746521aa4b445dd0a6dfd9750e8e04fbeff6a/layouts/_default/list.html#L41-L56) used for this is:

```go
<div class="post-content">
    {{ with .Description }}
        {{ . | markdownify }}
    {{ else }}
        {{ if .Truncated }}
            {{ .Summary }}
        {{ end }}
    {{ end }}
</div>
```

This code relies on at least one of two things being true to show a post excerpt:

1. The post has a `Description` in its front matter
2. The post is longer than [`summaryLength`](https://gohugo.io/getting-started/configuration/#summarylength) (which is 70 words by default)

There are several ways Hugo [generates a summary](https://gohugo.io/content-management/summaries/), but for really short posts without a description, the excerpt will not be displayed as the post will be shorter than the `.Truncated` length.

I am not sure of the original thought process behind the code above, but I want to ensure a summary will be displayed in all cases, especially as writing a `Description` for all posts feels like it could be a duplication of effort.

The fix is actually quite simple — remove the check for `.Truncated` in the code so either a description or summary are always displayed.

```go
<div class="post-content">
    {{ with .Description }}
        {{ . | markdownify }}
    {{ else }}
        {{ .Summary }}
    {{ end }}
</div>
```

While the code change itself is simple, implementing it comes with a couple of challenges. One way to implement the change, is to modify the code in the original theme that is referenced in my GitHub repository (this was added as a git submodule).

I prefer to keep the original theme as is and I don't want to manage my own fork of the code. So I'm going to use a feature of Hugo that allows me to keep the original theme unmodified while implementing my own changes.

Hugo uses a specific [lookup order](https://gohugo.io/templates/lookup-order/#hugo-layouts-lookup-rules-with-theme) for layouts, and so I can create a copy of the files I need to change, namely `index.html` and `list.html`, modify them with the above code, and place them in `/layouts/_default`. Hugo will use those in place of the corresponding files in my theme directory, while any files other than those two, will continue to be used from the theme directory.

The downside to this approach is that while I don't have a full code fork to maintain, I will need to maintain any upstream changes to these two files. As the theme doesn't change that often, hopefully it is not too onerous. I will look at ways to better tackle this in the future, such as attempting to raise a Feature Request for the original theme, or by creating a patch/diff that I can reapply as needed.

## The Read More button

Right next to the code I modified above is another change I'd like to make. The `Read More` button is displayed on every post by default. It can be hidden on a post by post basis by using `hideReadMore: true` in the post's front matter.

However for really short posts that are not truncated, there is no need for the button to appear as there is nothing more to read!

Let see how to fix this. The original code to display the `Read More` button looks like this.

```go
{{ if not .Params.hideReadMore }}
<div>
    <a class="read-more button" href="{{ .RelPermalink }}">
    {{ $.Site.Params.ReadMore | default "Read more" }} →</a>
</div>
{{ end }}
```

The change we have to make is quite simple — we only want to show the button on the post if the front matter has `.hideReadMore` as false (which is the default when it's not set) **and** the post is `.Truncated`. Hugo has [Conditionals](https://gohugo.io/templates/introduction/#conditionals) that allow us to do this easily.

```go
{{ if and .Truncated (not .Params.hideReadMore) }}
<div>
    <a class="read-more button" href="{{ .RelPermalink }}">
    {{ $.Site.Params.ReadMore | default "Read more" }} →</a>
</div>
{{ end }}
```

Implementing this is the same as before - this code is added to the modified copies of `index.html` and `list.html` that are kept in `/layouts/_default`.

## End of Part 1

In this post, I showed how you can improve excerpts to ensure they are displayed in almost every case as well as how to only show the `Read More` button when there is more to read!

There are more changes I want to make but as this post is getting a little long, I'll continue them in a new post soon.

---

##### Cover photo by [Claudio Schwarz](https://unsplash.com/@purzlbaum) on [Unsplash](https://unsplash.com/photos/wdXv6IVXIy8)
