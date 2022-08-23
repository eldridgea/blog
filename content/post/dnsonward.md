---
author: "Eldridge Alexander"
date: 2020-03-27T12:03:11Z
excerpt: "Easily proxy traditional DNS requests to a DoT server ensuring no eavesdropping or MITM manipulation of DNS requests."
draft: false
hero: "/img/dig-command.png"
slug: "dnsonward"
title: "Dnsonward: Moving to encrypted DNS"
authors:
  - Eldridge Alexander
---

Encrypted DNS is an improvement to end-user privacy and security. While there are occasionally trade offs to consider especially in enterprises, for home users, moving to encrypted DNS is almost universally an improvement. It closes [huge privacy gaps](https://www.eff.org/deeplinks/2019/09/encrypted-dns-could-help-close-biggest-privacy-gap-internet-why-are-some-groups) and prevents ISPs from harvesting user data from DNS queries. (Currently that information can also be harvested from TLS headers but that gap will be closed too as connections move to using [encrypted SNI in TLS 1.3](https://blog.cloudflare.com/encrypted-sni/)). It also prevents ISPs from redirecting to ad laden pages when there is no DNS result as opposed to letting the OS or browser handle the empty reasons as expected. 

Operating systems and even [browsers](https://blog.mozilla.org/blog/2020/02/25/firefox-continues-push-to-bring-dns-over-https-by-default-for-us-users/?utm_content=buffer85f7d&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer) are beginning to look at incorporating the new encrypted DNS standards, [DNS over TLS (DoT)](https://en.wikipedia.org/wiki/DNS_over_TLS) and [DNS over HTTPS (DoH)](https://en.wikipedia.org/wiki/DNS_over_HTTPS). DoT is supported natively in Android 9.0+ but no other major OS supports encrypted DNS natively yet. Even as OSes update there will inevitably be a long tail of devices in homes using traditional DNS such as older computers and tablets, smart TVs, and other IoT devices. Most consumer home networks give out DHCP leases where the DNS server is the home router, which then forwards DNS requests to a DNS service -- often one provided by the ISP. 

I wanted to have a home DNS service similar to consumer routers that would take local traditional DNS requests and forward them to an upstream DNS service but only using encrypted DNS. This way all my home devices could be upgraded to encrypted DNS in one fell swoop. I also wanted to make it easy for others to use and have some well known services preconfigured for use.

I built and open sourced [Dnsonward](https://github.com/eldridgea/dnsonward). It’s a docker container that can be started and pointed to some popular DoT servers and also allow you to configure your own. This is built on top of the excellent [CoreDNS](https://coredns.io/) -- being written in go, performant, and modular made it fit this use case perfectly.

## Quickstart 

If you want to give it a try you can spin up it up with Docker:
`docker run -e SERVICE="cloudflare" -p 53:53 -p 53:53/udp eldridgea/dnsonward`

You can replace `cloudflare` with either `google` or `quad9`. You can also pass environment variables to have it point at any DoT server, those details are in the [README](https://github.com/eldridgea/dnsonward).
