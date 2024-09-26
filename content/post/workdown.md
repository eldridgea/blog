---
author: "Eldridge Alexander"
date: 2019-09-23T12:03:11Z
excerpt: "An app to write Markdown and have it published and hosted via Cloudflare Workers."
draft: false
hero: "/cdn-cgi/image/format=auto/img/workers-illustration.png"
slug: "workdown"
title: "Workdown"
authors:
  - Eldridge Alexander
---

Today I'm open sourcing an app [Workdown](https://github.com/eldridgea/workdown/) -- you write Markdown and it will be converted to a site, uploaded, and hosted on Cloudflare Workers.

On occasion I run into situations where I want to spin up a site relatively quickly, and I want a (mostly) static site.
After all, static is fast! Generally I use Hugo and Netlify for these things, but using Cloudflare Workers on a few projects recently made be want to write Markdown and have it served directly from Cloudflare's edge.

So I wrote Workdown - an app to take Markdown, and upload it to be served directly from Workers. All you have to do to create a page, is create a file ending in `.md`, write some Markdown and run the `workdown` command and your content will be live in about 60 seconds or less.

It also supports custom HTML headers, footers, and CSS if you want to add it fonts or other stylings.

Any questions feel free to [tweet me](https://twitter.com/magiceldridge) or open a [GitHub Issue](https://github.com/eldridgea/workdown/issues)

<blockquote class="imgur-embed-pub" lang="en" data-id="a/UXouVgZ" data-context="false" ><a href="//imgur.com/a/UXouVgZ"></a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>