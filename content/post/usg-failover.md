+++
author = "Eldridge Alexander"
date = 2019-07-05T12:00:11Z
description = "Using a secondary Internet source for seamless failover if my AT&T goes down."
draft = false
image = "/img/ubiquiti-switch.jpg"
slug = "usg-failover"
title = "Home Nework Internet Failover"

+++

### Overview

My home AT&T fiber goes down on rare ocassion.
Overall the realibiltiy is pretty high but I wanted to have a failover just in case.
This is my home Intenet connection -- it runs some services, but nothing crucial.
I didn't want to spend a lot of money on this.
I have a pasword for [Xfinity WiFi](https://wifi.xfinity.com/) and my neighbors have an Xfinity hotspot so I decided I wanted to use this.

### Parts and Services
I already had Ubiquiti gear for my home network including a
[Security Gateway](https://store.ui.com/products/unifi-security-gateway). I also had my Xfinity password. 
The only new piece of hardware I got was a [GL.iNET travel router](https://www.amazon.com/gp/product/B073TSK26W).

![Travel Router](/img/glinet.png)

### Travel Router Setup
The GL.iNET travel router is somewhat cheap, so if you use one, adjust expectations accordingly, but it's extremely configurabe.
It uses a whiltlabeled verion of OpenWRT, with some nice defaults. One easy-to-setup option taking a WiFi connection and providing it via the device's LAN port, called "Repeater".

I chose the "Scan" option under "Repeater" and selected "xfinitywifi" as my upstream connection. I then connected my laptop to the LAN port, hit Xfinity's captive portal, and logged in.

![Menu Screen](/img/glinet_ui.jpg)

Once this was done, I connected the LAN port from the travel router to the WAN2/VoIP port on my Security Gateway.

### Ubiquiti Setup

Once this was connected, I went to my controller, opened the configuration for my Security Gateway, went to the Ports menu and enabled the WAN2 port.

![USG Menu Screen](/img/usg1.png)

Then, I went to the Site settings for my home and created a new network called WAN2.
I set the "Load Balancing" type to "Failover only" as I want to use my fiber line if it's available. 

I saved my setting and that's it! Ubiquiti makes it easy.

### Notifications

