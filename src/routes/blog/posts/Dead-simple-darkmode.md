---
title: Dead simple dark mode with css custom properties
date: '2021-12-16T09:12:03.284Z'
---

There's a lot of snark on various social channels any time a platform adds dark mode to their UI. To me, it's a decision based totally on the user and I think its great any time people get more control in their digital experiences. So, with that spirit in mind, let's look at potentially the most straightforward approach to applying theming based on device preference setting.

<!-- more -->

There's a lot of snark on various social channels any time a platform adds dark mode to their UI. To me, it's a decision based totally on the user and I think its great any time people get more control in their digital experiences. So, with that spirit in mind, let's look at potentially the most straightforward approach to applying theming based on device preference setting.

In recent years, just about all modern browsers have implemented `prefers` media queries that allow web sites and web apps to apply styling or behavipr based off overall operating system preferences. In addition to more robust media query support, we also have near universal support for CSS vustom properties. So, let's put these two technologies to work for some super simple dark mode.

First, let's start with some CSS custom properties, defined at the `:root` level.

```css
:root {
  --color-primary: #36393b;
  --color-secondary: white;
  --color-tertiary: #737171;
  --color-highlight: #34e4f6;
}
```

Then, let's apply those to our base CSS for our page:

```css
body {
  margin: 0;
  font-family: 'Kanit', sans-serif;
  font-size: 16px;
  line-height: 1.6;
  color: var(--color-primary);
  background: var(--color-secondary);
}
```
So far, so good. Now, all we need to do is to flip the value of some of those custom properties inside of our user preferences media query:

```css
@media (prefers-color-scheme: dark) {
  :root {
    --color-primary: white;
    --color-secondary: #36393b;
    --color-tertiary: #b3b0b0;
  }
}
```
That's it! Now, your site will base it's custom property values and your site's visitors will get the experience they prefer. For all the heat CSS takes, techniques like this demonstrate the immense progress and power it has made in recent years.
