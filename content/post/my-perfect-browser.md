---
author: "Eldridge Alexander"
categories: ["security", "chrome", "firefox", "opera", "safari", "edge", "broswer", "web"]
date: 2015-05-19T20:34:28Z
excerpt: "An examination of how I selected my preferred browser"
draft: false
hero: "/cdn-cgi/image/format=auto/img/13792583873_832a262252_k.jpg"
slug: "my-perfect-browser"
tags: ["security", "chrome", "firefox", "opera", "safari", "edge", "broswer", "web"]
title: "My Perfect Browser"

authors:
  - Eldridge Alexander
---

I'm trying to make everything I do online as secure as possible, while compromizing my expereince as little as possible. The most significant choice here is my web browser.

I rotate between a lot of them because none of the realistic options I've found meet all of my requirements.

### Requirements:
* Open source
* Tab sandboxing
* Supports [Privacy Badger](https://www.eff.org/privacybadger), [uBlock](https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm?hl=en), and [HTTPS Everywhere](https://www.eff.org/HTTPS-EVERYWHERE) (or equivalent feature set)

### Preferred:
* Automatic updates
* Cross platform (Windows, Mac, Linux, Android)
* [U2F support](https://www.yubico.com/authentication-standards/fido-u2f-standard/)
* [LastPass](https://lastpass.com/) support

|  | FOSS | Sandboxing | Privacy Extensions |
|---|---|---|---|
| [Chrome](https://www.google.com/chrome/) | No | Yes | Yes |
| [Chromium](https://www.chromium.org/) | Yes | Yes | Yes |
| [Firefox](https://www.firefox.com) | Yes | No | Yes |
| [Opera](http://www.opera.com/) | No | Unknown | Not all |
| [Safari](https://www.apple.com/safari/) | No | Yes | No |
| [Edge](http://windows.microsoft.com/en-us/windows/preview-microsoft-edge-pc) | No | Unknown | No |

So, Chromium meets my security requirements, but it's unrealistic for a few reasons:

### It has no way to download a compiled binary for the stable track
If you want to use Chromium, you have to build it yourself, or download a binary someone else built. I don't generally trust 3rd-party compiled binaries, and I don't want to have to build a binary each new release. If you're only running Linux distros that have Chromium in their repositories, it's a pretty great choice, but I have Macs and Android too much in my daily workflow.

### No Automatic Updates
This isn't really a deal-breaker but it does pose a problem, especially when you have to build each version yourself.

### Made by Google
(This is veering a bit from security practices into mild paranoia.) If possible, I prefer my browser to come from a non-profit -- or failing that, somewhere that has proven their primary devotion is the open web with little or no "distractions".


### Long Story Short
Chromium would be great if there were available binaries for the stable track. *Best* would be if Mozilla implements sandboxing and U2f support. In the meantime, everything is a compromise. Or I might spin up a VM on my hypervisor just for Chromium builds.

`Photo Credit: https://www.flickr.com/photos/110751683@N02/13792583873`
