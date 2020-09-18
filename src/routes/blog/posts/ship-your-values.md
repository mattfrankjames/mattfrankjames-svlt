---
title: Ship Your Values
date: '2020-09-16T22:12:03.284Z'
---

When I set out to rebuild my site earlier this year, I wanted something that felt fast and relied on a modern stack. My previous site was built Jekyll and GitHub pages and was generally ok, but I wanted an excuse to get deeper into the current JavaScript landscape so I could use the experimentation to keep my skillset sharp.

<!-- more -->

When I set out to rebuild my site earlier this year, I wanted something that felt fast and relied on a modern stack. My previous site was built Jekyll and GitHub pages and was generally ok, but I wanted an excuse to get deeper into the current JavaScript landscape so I could use the experimentation to keep my skillset sharp.

Initally, I thought about doing the headless Wordpress thing with a Gatsby front-end. I was already teaching my Web Design students Wordpress, so there was some logic there. Then, I realized I would just be writing my posts in Markdown anyway, so why bother with the whole database?

I was pretty jazzed on React and Gatsy, so that felt like a natural fit. I could use the Netlify pipeline hooked up to GitHub and I'd get a site that was "fast in every way that matters". So, I got most of the way through it, but didn't find myself super motivated blog or take the layout through to completion. Something about writing a bunch of `graphQL` just to fetch an image felt like a bit much. The start of a global pandemic probably didn't do much for my motivation, either.

Then there was this nagging in the back of my head. With every Alex Russell tweet, with every shitpost by another tech bro, I got less and less excited about the site. After all, I was just making a blog. Did I really need to ship all of React to parse some markdown? I like the UX of a SPA, but shipping mbs of JS for that experience felt like a bit much.

Then, Gatsby, the company, let someone I have a deep respect for, an objectively kind person go in what semed like a very acrimonious manner. And then there was this Twitter thread. The whole thing felt gross.

Along the way, I had gotten more and more excited about Svelte and both the feature set and performance it offered. So, I threw out the Gatby site and found this wonderful Svelte/Sapper blog starter. It came together super fast with a little customization and is super close to a perfect Lighthouse score out of the box.

Out of curiosity, I decided to run the Gatsby site and the Svelte site through webpagetest. Low and behold, 3.6mb of JavaScript for the Gatsby compared to 2.6kb of it for Svelte. Same content, still just parsing markdown. My suspicions were confirmed.

The point of this post is less to do the whole, "I made a new site and here's how I built it" thing, but to highlight how our values impact our decisions in tech. I deeply value performance in everything I build and here I was ignoring obvious performance implications out of convenience. I deeply value empathy and compassion among teams and that put me over the edge, overriding my desire to build in more experiene with React to help my career.

As developers and designers, we face decisions like this every day. Do we bring up the missing `for` attribute on a `<label>` or let it go? At work, I've become the "Please make this a `<button>` guy on almost every code review. While I'm a little uncomfortable being a constant squeaky wheel, I know that these kinds of details are important. Our codebase is immensely complex and entirely intimidating for someone new to the team, but I'm confident that my insistence on semantic HTML and accessibility coniderations is making our platform better for all users and setting the team on a more inclusive path going forward.

While some of these changes are small and the impact on a given PR might be pretty insignificant, they can make a big impact long term for users. And, that sentiment ties into tech as a whole- both in the way that it impacts individual users but society as a whole. We're in a deeply troubling period that is abetted in no small part by the decisions of thousands of developers who look the other way as the product they work on is busy monetizing dischord and abuse. While there are no doubt many developers who legitimately don't care that, say, YouTube's algorithm is radicalizing people, there are many more that are showing up to work who would never voluntarily sign on to such a project. Yet, it can be so much easier to go about one's day with the viewpoint that you need a paycheck.

If we all step back and look at the decisions we are making in tech, from the minutiae of a missing alt tag to the bias of a platform toward white nationalism, and truly put our values into the products we ship, we can start to bend the curve away from this moment in history. We can start to turn it back to the idealism that was so prevalent in the early days of the web.
