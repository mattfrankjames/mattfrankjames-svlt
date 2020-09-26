---
title: A Little Think I Learned About `sapper export`
date: '2020-09-26T22:12:03.284Z'
---

I put this site together with [Svelte](https://svelte.dev/) and [Sapper](https://sapper.svelte.dev/) and am hosting it on [Netlify](https://www.netlify.com/). It's a glorious workflow. Write a post or make a new route, push to `main` and viola, instant deploys. The other day I decided to make a `/uses` page as I've enjoyed looking at other people's uses page. I stuck it in the `routes` folder of the `src` directory, saw it when developing but it kept not making it through the Netlify deploy. What was the deal? It turns out that the behavior of the `sapper export` command that Netlify was running on deploy was at fault. Let'd take a look at this little quirk of that build command.

<!-- more -->

I put this site together with [Svelte](https://svelte.dev/) and [Sapper](https://sapper.svelte.dev/) and am hosting it on [Netlify](https://www.netlify.com/). It's a glorious workflow. Write a post or make a new route, push to `main` and viola, instant deploys. The other day I decided to make a `/uses` page as I've enjoyed looking at other people's uses page. I stuck it in the `routes` folder of the `src` directory, saw it when developing but it kept not making it through the Netlify deploy. What was the deal? It turns out that the behavior of the `sapper export` command that Netlify was running on deploy was at fault. Let'd take a look at this little quirk of that build command.

Per the [Sapper](https://sapper.svelte.dev/docs#sapper_export) docs, the `sapper export` command will export a production ready site to the `__sapper__/export` directory. So far so good. But, the way it actually works is where my little rub came in.

Again, from the [Sapper](https://sapper.svelte.dev/docs#sapper_export) docs:

> When you run `sapper export`, Sapper first builds a production version of your app, as though you had run sapper build, and copies the contents of your static folder to the destination. It then starts the server, and navigates to the root of your app. From there, it follows any `<a>`, `<img>`, `<link>` and `<source>` elements it finds pointing to local URLs, and captures any data served by the app.

> Because of this, any pages you want to be included in the exported site must either be reachable by `<a>` elements or added to the `--entry` option of the sapper export command.

> The `--entry` option expects a string of space-separated values. Examples:

```shell
sapper export --entry "some-page some-other-page"
```

> Setting `--entry` overwrites any defaults. If you wish to add export entrypoints in addition to `/` then make sure to add `/`as well or `sapper export` will not visit the index route.

My problem was that I wasn't linking to the `/uses` page anywhere, so `sapper export` wasn't picking it up during it's crawl of `localhost`. Solving this was as easy as changing my `npm run export` command to this:

```json
"sapper export --entry '/ uses'"
```

With that minor change, Netlify, or rather Sapper, deployed the page. Not only did this little adventure teach me something about Sapper, it also reminded me that the first place to check when encountering an issue is not necessarily the first Google result, but the official project documentation.

<a onclick="document.location.hash='top';" href="javascript:;">[Top]</a>
