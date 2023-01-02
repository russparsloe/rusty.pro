---
title: Font Awesome
date: 2023-01-02T11:03:13Z
tags: ["hugo", "website"]
cover: 2023-01-02-font-awesome.png
coverAlt: Font Awesome Icons
coverCaption: The clue is in the name!
useRelativeCover: true
---

While in the procoess of writing my (currently unpublished) [About](/about/) page, one of the things I wanted to add were icons for the links to my various social media profiles. I could add these as images, but I figured it might be cool to add [Font Awesome](https://fontawesome.com) to the blog. Turns out it's actually very simple to do...<!--more-->

A quick online search led me to a few articles on how to do this. The implementation I favoured was from Michael Ryan on [Something Strange](https://somethingstrange.com/posts/hugo-with-fontawesome/) as it doesn't modify the theme files directly, and has support for colours, sizes and opacity.

Copying from Michael's post, the shortcode syntax to use it is as follows:

```
{{</* <style-shortcode> <icon> [color] [size] */>}}
```

- `<style-shortcode>`
  - One of the Font Awesome shortcodes: `fab`, `fad`, `fal`, `far`, or `fas`. (Unlike Michael, I am using the free version, so only `fab`, `far`, and `fas` are available).

- `<icon>`
  - A Font Awesome icon code such as `rocket-launch`.

- `[color]`
  - A color pattern, which may include a single color value using standard CSS color notation: `[color]`
    - `orange`
    - `#ffa500`
    - `rgb(255, 165, 0)`
    - `hsl(39, 100%, 50%)`
  - A color and an opacity: `[color][/<opacity>]`
    - `orange / 50%`
    - `#ffa500 / 0.5`
  - Two colors with optional opacity: `[color][/<opacity>];[color][/<opacity>]`
    - `orange / 50% ; blue / 100%`
    - `#ffa500 / 0.5 ; #00f / 1`
  - To set opacity without affecting color, leave the color value blank or set it to currentColor:
    - `/ 50%`
    - `currentColor / 0.5`
  - To set secondary color without affecting the primary, leave the primary color value blank or set it to currentColor:
    - `; blue`
    - `currentColor ; #00f`
  
  {{< fas triangle-exclamation >}} If the value includes any non-alphanumeric characters, wrap it in quotes.

- `[size]`
  - The size value using standard CSS length notation.
  
  {{< fas triangle-exclamation >}} If the value includes any non-alphanumeric characters, wrap it in quotes.

Awesome! {{< fas font-awesome gold >}}

##### Cover photo by [Font Awesome](https://fontawesome.com)
