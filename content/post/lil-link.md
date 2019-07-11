+++
author = "Eldridge Alexander"
date = 2019-07-09T12:03:11Z
description = "A shortlink system built entirely on Cloudflare workers."
draft = false
image = "img/workers-illustration.png"
slug = "lil-link"
title = "Lil Link"

+++

Today I'm open sourcing a shortlink project I'm calling [Lil Link](https://lillink.co) that runs entirely on [Cloudflare Workers](https://workers.cloudflare.com/).

At every company where I've worked, there has always been a "go link" or a "shortlink" system.
As there aren't many modern and maintained open source systems, this tends to get reimplemented a lot. In fact. as an employee, I wrote the shortlink system that Cloudflare itself used (and may still use) in AppEngine before Workers was a product.
The big difference between these shortlink systems and something like bit.ly is the shortlinks typically are aimed at employees and insiders as opposed to the public, so anyone is allowed to make "branded" shortlinks - a link named whatever the user wants.
This makes it easy to share the links verbally or in text form and have the link be remembered, a huge benefit as many internal links to resources are often long and unwieldy. 

As this runs entirely on Cloudflare Workers this is quick and easy to implement and relatively cheap to run.

I'll be offering a hosted version later this summer for anyone that doens't want to, or can't maintain with their own installation, but some organziations will hopefilly find this useful after a quick `wrangler publish`.

[The code is available in this GitHub repo](https://github.com/eldridgea/lil-link).