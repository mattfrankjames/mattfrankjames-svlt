---
title: Belated 2019 Year in Review
date: '2020-01-25T22:12:03.284Z'
---

2019 was a weird year. I left a job of four plus years where I was very happy and joined a much smaller company focused on eCommerce and brick and mortar retail.

<!-- more -->

I can look back with pride on a number of things I accomplished at my previous role - contributing to the responsive redesign and build of an enterprise level site that had been collecting dust for years, the first [React project within the line-of-business](https://www.wellsfargoadvisors.com/planning/ira-potential/index.htm) and a number of performance and workflow improvements within our team. But, having spent the last several years going deep on studying the modern web stack and watching the rise of new and exciting UI platforms, I was beginning to feel antsy for a greater challenge, one where I could leverage the things I had been putting so much energy into learning. So, when the opportunity came to rebuild the front-end of a major eCommerce site as a progressive web app with the stack of my choosing and incorporate it into the new headless Magento API, it was a promise too good to pass up.

Admittedly, the first few months were a bit rocky. There was a major platform upgrade to address, more extremely late nights and early mornings than I was used to at my previous job, and a large amount of time spent taping together legacy CSS littered with [crazy town selectors](https://css-tricks.com/crazy-town-selectors/), the result of deeply nested `.less` partials. Add to that, learning to navigate the default front-end implementation of Magento, and I was beginnng to wonder what I had signed up for. If you've had the good fortune to have avoided the standard Magento frontend architecture at this point in your career, I'd humbly recommend you keep it that way.

Still, I can look back at my first six months with the company and point to some legitimate accomplishments:

- Implementing a suite of automated Webdriver IO tests connected to Cross Browser Testing.
- Bringing our Lighthouse accessibility score from a 37 to 91. (The nav still has some `<ul>` elements with `<div>`s as direct children and there's a marketing `<iframe>` without a label. Not ideal, but a big improvement).
- Implenting a `serviceworler` and `manifest` into the site, giving us a baseline PWA and a massive performance boost.
- UI improvements projected to generate over \$5 million in additional sales year over year if current analytic trends hold.
- Implementation of a code splitting module within our Magento instance that has cut our time-to-interactive metrics in half and doubled our Lighthouse performance score for product pages on a throttled connection with 4x CPU slowdown.

And, things are looking up for the coming year. I've begun the headless front-end of our site with Next JS and Apollo and have assempled a solid, working proof of concept on [now.sh](https://now.sh) that blows our previous performance metrics away and already delivers a much improved UX for our customers.

So, all in all, the job change was positive and I feel confident saying that I've learned far more and gained far more experience that will help grow my career than if I had stayed where I was. I definitely miss the people, gym and general level of comfort and familiarity at my old job, but sometimes compromises have to be made to keep moving forward.

To add to the complexities of the year, my dad passed away over the summer. It was and continues to be extremely hard. Our relationship was complicated and by no means perfect, but his loss was a brutal and unexpected blow that cast a pall over many aspects of the rest of my year. I let my health deteriorate a fair amount, largely stopped exercising and got a bit too comfortable with my alcohol intake. The sting of the loss is still there, as I imagine it always will be, but I've started to turn things around for my health. As of this writing, I haven't had any alcohol in over three weeks and, while I don't intend to stop completely, it's good to know that I can take a prolonged break. I've also either been on the treadmill or the rollers every day except for one and have closed all my Apple watch rings each day of 2020 so far.

So, all in all, things seems to be trending in the right direction. I'm feeling much better physically and mentally, I'm engaged in a challenging and fulfilling project at work that I know will grow my skills as a developer many times over, and I have the most amazing family around me through it all. I'm hoping that the rest of 2020 follows a similar trajectory, not just for me but for the world writ large. It definitely feels like we're all on a precipice most of the time...

One thing I'm hoping to do in 2020 is blog more. I'm not putting major pressure on myself, but once a month feels doable. Who knows, maybe I'll actually get around to re-working this site into a Gatsby/headless WordPress set up like I keep threatening. For now, though, this years old Jekyll GitHub pages site suffices just fine, even though the design leaves a bit to be desired. One thing at a time, though.

Thanks for reading.
