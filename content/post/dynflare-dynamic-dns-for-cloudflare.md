+++
author = "Eldridge Alexander"
categories = ["cloudflare", "dns", "dynamicdns", "hoemlab"]
date = 2018-09-26T22:57:01Z
description = ""
draft = false
image = "/img/lava-lamps.jpg"
slug = "dynflare-dynamic-dns-for-cloudflare"
tags = ["cloudflare", "dns", "dynamicdns", "hoemlab"]
title = "Dynflare: Dynamic DNS for Cloudflare"

+++

### *Disclaimer: This is not a product of Cloudflare and is not supported or endorsed by them.*
<br></br>
I currently use Cloudflare for all my DNS needs. No surprises there, it's awesome!

I recently changed home ISPs and my new one doesn't offer a free static IP. I run several services out of my lab at home. I'm the only person that really uses any of the services–definitely not a crucial setup with a 99.999% SLA. So it's not really a good investment to send more money AT&T's way for a static IP, but it would be nice for my DNS records to get updated automatically.

So I threw together a quick Python script I'm calling Dynflare that will automatically update by DNS record for my home server. All the benefits of Cloudflare and all the benefits of dynamic DNS without adding a third service in the mix.

I'm planning on adding more soon (e.g. IPv6 support, and Spectrum support for SSH) but this should work for anyone else at the moment with a relatively simple setup like me. Standard warnings about pre-alpha software apply.