---
title: Font-Display is the Hot Jam
date: '2017-10-23T22:12:03.284Z'
---

Ah, sweet web fonts.. Like a typographic oasis in a desert of mid-2000's 'web safe' fonts, they offered a unique aesthetic and the potential for consistent brand recognition without resorting to generic Georgia or Verdana.

<!-- more -->

Ah, sweet web fonts.. Like a typographic oasis in a desert of mid-2000's 'web safe' fonts, they offered a unique aesthetic and the potential for consistent brand recognition without resorting to generic Georgia or Verdana.

But, unfortunately, they came with a price. Designers didn't like the early browser behavior of swapping a system font for a custom font when it loaded, so browser vendors collectively implemented FOIT, or Flash of Invsible Text, which gave a window of time for custom fonts to load before a fallback font was provided. For most browsers, this meant there were potentially up to three seconds of invisible text before a font would render. For older `-webkit-` browsers, however, this window was (and is) unlimited. Meaning, if the web font never loads, then no text will ever render.

So what, then, to do about this? While there have been a number of highly effective [JavaScript based solutions](https://github.com/bramstein/fontfaceobserver), a new browser API has started to ship which will largely solve this problem and put the solution in the hands of CSS authors.

## Enter font-display

By using the `font-display` descriptor inside your `@font-face` declaration, you can now tell the browser how to handle the lag in load time for web font parsing. Admittedly, browser support is currently on the "not awesome" side of the spectrum.

![font-display support chart](img/font-display-support.png)

That said, it's behind a flag in Firefox and is in Safari Technology Preview, as well as stable Chrome, so the future looks good. Plus, it's progressive enhancement, so what do you have to lose?

## So, How's it Work?

The `font-display` takes four potential values, each telling the browser how the author wants to deal with font-loading.

### Block

The `block` value is essentially a stand in for the browser default of 3000ms timeout before a system font is loaded. It's the equivalent of the author saying, "No, really, this font is super important, to the exclusion of all other things, and I want you to wait for it". I'm not really sure why you would bother with this, unless you were very passionate about your typeface.

### Swap

The `swap` value provides the fallback font until the custom font is available. This is guaranteed FOUT, but also guaranteed text, immediately on the page.

### Fallback

The `fallback` value is a bit of a compromise between the two. It dramatically cuts the wait time for the custom font to 100ms. Meaning, there's a decent chance the fallback font won't be displayed on a good connection, keeping aesthetics clean, but also that users will never have to wait an excruciating 3 seconds.

### Optional

The `optional` value is particularly interesting. It displays the fallback font immediately, then gives a very short window for the custom font to arrive before giving up on displaying it and sticking it in a cache for subsequent viewings. This value minimizes the chance of FOUT, but also maximizes the chance of the fallback font being the primary experience on initial view. It also lets the browser decide based on connection (sort of like `srcset` for images) if it even uses it at all. The upshot of this value is that the custom font could still be put in a service worker cache for future visits and a seamless experience.

All together, this is some big time power for typography control in CSS. It makes it so we no longer to be afraid of a terrible UX based on our font choice and we can optimize for repeat users. It feels pretty great to have this much control in one line of CSS and, used in conjunction with slightly more elaborate [JS solutions](https://www.zachleat.com/web/comprehensive-webfonts/), we can get our content on the page and ready to consume almost instantly.
