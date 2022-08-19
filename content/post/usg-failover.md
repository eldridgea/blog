+++
author = "Eldridge Alexander"
date = 2019-07-05T12:00:11Z
description = "Using a secondary Internet source for seamless failover if my AT&T goes down."
draft = false
hero = "/img/ubiquiti-switch.jpg"
slug = "usg-failover"
title = "Home Network Internet Failover"

+++

### Overview

My home AT&T fiber goes down on rare occasion.
Overall the reliability is pretty high but I wanted to have a failover just in case.
This is my home Internet connection -- it runs some services, but nothing crucial.
I didn't want to spend a lot of money on this.
I have a password for [Xfinity WiFi](https://wifi.xfinity.com/) and my neighbors have an Xfinity hotspot so I decided I wanted to use this.

### Parts and Services
I already had Ubiquiti gear for my home network including a
[Security Gateway](https://store.ui.com/products/unifi-security-gateway). I also had my Xfinity password. 
The only new piece of hardware I got was a [GL.iNET travel router](https://www.amazon.com/gp/product/B073TSK26W).

![Travel Router](/img/glinet.png)

### Travel Router Setup
The GL.iNET travel router is somewhat cheap, so if you use one, adjust expectations accordingly, but it's extremely configurable.
It uses a whiltlabeled version of OpenWRT, with some nice defaults. One easy-to-setup option taking a WiFi connection and providing it via the device's LAN port, called "Repeater".

I chose the "Scan" option under "Repeater" and selected "xfinitywifi" as my upstream connection. I then connected my laptop to the LAN port, hit Xfinity's captive portal, and logged in.

![Menu Screen](/img/glinet_ui.jpg)

Once this was done, I connected the LAN port from the travel router to the WAN2/VoIP port on my Security Gateway.

### Ubiquiti Setup

Once this was connected, I went to my controller, opened the configuration for my Security Gateway, went to the Ports menu and enabled the WAN2 port.

![USG Menu Screen](/img/usg1.png)

Then, I went to the Site settings for my home and created a new network called WAN2.
I set the "Load Balancing" type to "Failover only" as I want to use my fiber line if it's available.

![USG Menu Screen](/img/usg2.png)

I saved my setting and that's it! Ubiquiti makes it easy.

### Notifications

Ubiquti has a pretty good notification system. In the Site settings, I enabled email alerts. 
(You can configure your email credential settings in your Settings > Controller menu.)

![Email Alert Screen](/img/usg3.png)

As my Internet seamless failed over I was no longer made immediately aware if my Internet went down.
Now I get an email alert when my AT&T fiber goes down.

`Image Credit: https://ccsearch.creativecommons.org/photos/fe524643-f6ba-48bc-b489-06041d4589b5`
