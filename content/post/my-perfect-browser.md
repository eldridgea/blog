+++
author = "Eldridge Alexander"
categories = ["security", "chrome", "firefox", "opera", "safari", "edge", "broswer", "web"]
date = 2015-05-19T20:34:28Z
description = ""
draft = false
image = "/images/2015/06/13792583873_832a262252_k.jpg"
slug = "my-perfect-browser"
tags = ["security", "chrome", "firefox", "opera", "safari", "edge", "broswer", "web"]
title = "My Perfect Browser"

+++

I'm trying to make everything I do online as secure as possible, while compromizing my expereince as little as possible. The most significant choice here is my web browser.

I rotate between a lot of them because none of the realistic options I've found meet all of my requirements.

######Requirements:
* Open source
* Tab sandboxing
* Supports [Privacy Badger](https://www.eff.org/privacybadger), [uBlock](https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm?hl=en), and [HTTPS Everywhere](https://www.eff.org/HTTPS-EVERYWHERE) (or equivalent feature set)

######Preferred:
* Automatic updates
* Cross platform (Windows, Mac, Linux, Android)
* [U2F support](https://www.yubico.com/applications/fido/)
* [LastPass](https://lastpass.com/) support

<table border="1">
  <tr>
    <td></td>
    <td>FOSS</td>
    <td>Sandboxing</td>
    <td>Privacy Extensions</td>
  </tr>
  <tr>
    <td><a href="https://www.google.com/chrome/">Chrome</a></td>
    <td>No</td>
    <td>Yes</td>
    <td>Yes</td>
  </tr>
  <tr>
    <td><a href="https://www.chromium.org/">Chromium</a></td>
    <td>Yes</td>
    <td>Yes</td>
    <td>Yes</td>
  </tr>
  <tr>
    <td><a href="https://www.firefox.com">Firefox</a></td>
    <td>Yes</td>
    <td>No</td>
    <td>Yes<Yes/td>
  </tr>
  <tr>
    <td><a href="http://www.opera.com/">Opera</a></td>
    <td>No</td>
    <td>Unknown</td>
    <td>Not all</td>
  </tr>
  <tr>
    <td><a href="https://www.apple.com/safari/">Safari</a></td>
    <td>No</td>
    <td>Yes</td>
    <td>No</td>
  </tr>
  <tr>
    <td><a href="http://windows.microsoft.com/en-us/windows/preview-microsoft-edge-pc">Edge</a></td>
    <td>No</td>
    <td>Unknown</td>
    <td>No</td>
  </tr>
  </table>

So, Chromium meets my security requirements, but it's unrealistic for a few reasons:

######It has no way to download a compliled binary for the stable track
If you want to use Chromium, you have to build it yourself, or download a binary someone else built. I don't generally trust 3rd-party compiled binaries, and I don't want to have to build a binary each new release. If you're only running Linux distros that have Chromium in their repositories, it's a pretty great choice, but I have Macs and Android too much in my daily workflow.

######No Automatic Updates
This isn't really a deal-breaker but it does pose a problem, espeically when you have to build each version yourself.

######Made by Google
(This is vereing a bit from security practices into mild paranoia.) If possible, I prefer my browser to come from a non-profit -- or failing that, somewhere that has proven their primary devotion is the open web with little or no "distractions".


######Long Story Short
Chromium would be great if there were available binaries for the stable track. *Best* would be if Mozilla implements sandboxing and U2f support. In the meantime, everything is a compromise. Or I might spin up a VM on my hypervisor just for Chromium builds.

`Photo Credit: https://www.flickr.com/photos/110751683@N02/13792583873`
