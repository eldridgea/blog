+++
author = "Eldridge Alexander"
categories = ["android", "dns"]
date = 2019-01-07T20:39:01Z
description = "System-wide ad and tracker blocking on Android"
draft = false
image = "/img/androids.jpg"
slug = "project-erised"
tags = ["android", "dns"]
title = "Project Erised"

+++

Android 9.0 [introduced](https://android-developers.googleblog.com/2018/04/dns-over-tls-support-in-android-p.html) native suppport for [DNS over TLS](https://tools.ietf.org/html/rfc7858) (DoT). I like blocking ads and trackers on my device, but I don't like rooting or using an always-on VPN.
I begain investigating using DoT as a method for adblocking, as Android uses DoT for all DNS requests if it's enabled. I used a combination of off-the-shelf stuff in a docker network to handle this. 

The incoming DoT request is handled by [Caddy](https://caddyserver.com/) which strips the TLS and forwards it as a standard DNS request within the private Docker network to a container running [PiHole](https://pi-hole.net/).
PiHole will blackhole any requests that are on its blacklist, and otherwise forward them upstream to the container running [cloudflared](https://developers.cloudflare.com/1.1.1.1/dns-over-https/cloudflared-proxy/), which will re-encrypt the request and send it upstream to Cloudflare's [1.1.1.1](https://1.1.1.1.) DNS service.

So the only DNS requests that will get legit responses are ones not on PiHole's blacklist, and this applies across the web and within apps.

[I've uploaded the project to GitHub](https://github.com/eldridgea/erised). If you have docker and docker-compose already installed you can get this up and runnning in about 5 minutes and with 2 commands.


Once configured, a DNS request will look like this:

    ---------
    |Your   |
    |Device |
    |       |
    ---------
        |
        |
        |
        |
    ---------
    |       |
    |Caddy  |
    |       |
    ---------
        |
        |
        |
        |
    ---------
    |       |
    |pihole |
    |       |
    ---------   
        |
        |
        |
        |
    ---------------
    |             |
    |cloudflared |
    |             |
    ---------------
        |
        |
        |
        |
    -------------------
    |                 |
    |Cloudflare's     |
    | 1.1.1.1 service |
    -------------------

`Photo Credit: https://www.flickr.com/photos/rbulmahn/6180104944`