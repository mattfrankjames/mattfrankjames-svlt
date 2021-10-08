---
title: Getting Started With Container Queries
date: '2021-10-04T22:12:03.284Z'
---

For as long as I’ve been working full-time on the front-end, I’ve heard about the promise of container queries and their potential to solve the majority of our responsive web design needs. And, for as long as I’ve been working on the front-end, there has been a running joke that we’d never actually get them coupled with a fair amount of anguish over their absence from our front-end toolbox.

<!-- more -->

For as long as I’ve been working full-time on the front-end, I’ve heard about the promise of container queries and their potential to solve the majority of our responsive web design needs. And, for as long as I’ve been working on the front-end, there has been a running joke that we’d never actually get them coupled with a fair amount of anguish over their absence from our front-end toolbox.

All that is starting to change. Seemingly out of nowhere, a draft spec for container queries became available in Chrome Canary, giving developers the opportunity to experiment with them in the browser and provide meaningful feedback to help advance the spec forward.

So, now that we have the ability to play with an initial implementation of container queries, let’s look at what they are, what problems they solve, and how we can use them in their current state.

Before we do that, let’s look at what we currently have available to us.

## Media Queries

Media queries unlocked responsive web design, giving developers the ability to respond to the user’s browser viewport and adjust styles and layout accordingly. To use them, we set a base style in CSS, then set up a media query within which styles are adjusted when whatever condition the media query is testing for i

```css
.wrapper {
  padding: 1em;
}
@media (min-width: 60em) {
  .wrapper {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    padding: 2em;
  }
}
```

More recently, media queries have evolved to allow developers to tailor styling based on a user’s system preferences for things like dark mode or reduced animation.

```css
body {
  color: #44464a;
  background: white;
}
/*== invert colors if a user's system is set to dark mode ==*/
@media (prefers-color-scheme: dark) {
  body {
    color: white;
    background: #44464a;
  }
}

.animation {
  animation: pulse 1s linear infinite both;
}
/*== remove or lessen the animation if a user's system is set to prefer reduced motion ==*/
@media (prefers-reduced-motion) {
  .animation {
    animation: none;
  }
}
```

## Feature Queries

In recent years, feature queries have been added to all modern browsers, allowing us to test for browser support of various CSS properties and provide a suitable fallback for non-supporting browsers. Here, I’m testing support for the initial-letter property and applying styles for a dropcap if a browser supports it.

```css
@supports (initial-letter: 4) or (-webkit-initial-letter: 4) {
  .article::first-letter {
    font-weight: bold;
    margin-right: 0.5em;
    -webkit-initial-letter: 4 1;
    initial-letter: 4 1;
  }
}
```

## What are container queries and what problems do they solve?

Container queries are an emerging browser feature that allow us to target elements based on the context of a containing element. They allow us to focus on the context of a component for our styling outside of the context of the viewport. This means we can drop a component anywhere and get the styling we expect.

It’s important to note the only children or descendants of an element designated as a container can have their styling affected by rules in a container query. This makes it possible for an element within a container to be a container itself. This also solved the recursive issue that plagued container queries, initially called element queries, where an element would query itself to apply styles.

## The current state of container queries

Container queries are in an experimental draft implementation within Google Chrome Canary. The spec is a work in progress and is subject to change, so you shouldn’t start shipping them just yet.

However, the implementation means that we can start experimenting with the syntax by enabling a flag within Canary. By going to `chrome://flags` and enabling the container queries flag, we can get a feel for the current syntax.

![Chrome Canary Flags](https://res.cloudinary.com/mjtestrun/image/upload/v1633377095/personal-site/Screen_Shot_2021-10-04_at_2.50.25_PM.png)

## The syntax

In this example, the `layout` value is creating a block formatting context which prevents the contents from affecting contents in another container. Meanwhile, the `inline-size` value is part of the spec authored by [Miriam Suzanne](https://twitter.com/TerribleMia), which creates a single axis containment context and allows us to begin experimenting with container queries.

Now that we have a container established, we can alter the styles of the children of that container as the container itself changes sizes.

```css
/*=== some base styles ===*/
.card-wrapper__card svg {
  width: 60px;
  border: 1px solid lightblue;
  border-radius: 5px;
  fill: DodgerBlue;
  box-shadow: 3px 3px 0 pink;
  padding: 0.25em;
}
/*=== update based on container's width ===*/
@container (min-width: 300px) {
  .card-wrapper__inner {
    display: flex;
    gap: 16px;
    align-items: center;
  }
  .card-wrapper__card svg {
    width: 100px;
    flex: 1 0 100px;
    box-shadow: none;
    border: none;
  }
}
```

As you can see, the syntax for writing a container query is strikingly similar to what we’re used to with media queries. This alignment, should it continue, should make experienced CSS developers quite comfortable with using them. Click the image below if you'd like to see the result of the above code.

[![Link to container queries on YouTube](https://res.cloudinary.com/mjtestrun/image/upload/v1633709276/container-queries_pxyudg.png)](https://youtu.be/9A6CZknr-t4)

Here, we can see that each card depicting the daily weather is responsible for its own layout. As an aside, the overall page layout adjusts to the viewport in classic responsive behavior, but now the layout for each card is removed from the context of the viewport. This gives us immense control over more granular layout concerns.

## A note of caution

As exciting as it is to finally see this in the browser, it’s worth noting that container queries are a long way from production ready. First, they are only enabled in Canary builds at the moment. Second, the current spec is a work in progress and is likely to change before it is finalized.

If you do decide to throw caution to the wind and start implementing container queries in your work, make sure to lean heavily on progressive enhancement. Using a combination of the feature queries mentioned earlier in the post and a layout that holds up without container queries, you could be relatively safe incorporating them into your work. Provided, of course, you’re not squeamish about an inevitable re-factor.

Still, after waiting so long to see this feature that developers have been begging for, it’s incredibly satisfying to finally see a working implementation, however fragile.

## Where to go from here

As developers, the rough spec for container queries gives us an immense opportunity to leverage influence over the browser’s ultimate implementation. Download [Chrome Canary](https://www.google.com/chrome/canary/), turn on the feature flag and start playing around. And, if you want to contribute to the process, there is an issue tracker on [Github](https://github.com/w3c/csswg-drafts/projects/18) where you can contribute feedback and follow various issues.

## Container queries are the future

CSS has come a long way over the last few years. From Grid to logical properties to the nascent approach to container queries, much of what the front-end landscape has needed for so long is finally available, or close to it. With this initial pass at container queries, developers have a unique opportunity to test drive a long sought after feature and contribute to its specification. Here’s hoping the pace of progress with CSS doesn’t let up and we see a stable version of container queries in all browsers within a short period of time.
