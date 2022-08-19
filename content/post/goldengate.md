+++
author = "Eldridge Alexander"
categories = ["security", "proxy", "reverse proxy"]
date = 2014-12-23T21:23:44Z
description = "Golden Gate aims to be a transparent reverse proxy that sits on the border of a network."
draft = false
hero = "img/800px-Golden_Gate_Bridge_Yang_Ming_Line.jpg"
slug = "goldengate"
tags = ["security", "proxy", "reverse proxy"]
title = "Project Golden Gate"

+++

### Overview

This is an outline for a project I'm working on. I'll post updates as I progress.

Golden Gate aims to be a transparent reverse proxy that sits on the border of a network. It will handle all web requests coming into the newtork and pass them to the appropriate server. Except for Golden Gate, nothing will be open to the Internet in general.

Golden Gate aims to provide

* Security
* SSL Configuration
* Virtual hosts/subdomain management
* Centeralized Authentication
	* Kerberos
    * Two factor authentication

### Technologies
* nginx reverse proxy
* Python/Django for web management
* iptables/ufw for internal security


### Resources
* http://wiki.sabnzbd.org/howto-apache
* https://gist.github.com/Thermionix/3375989

`Photo Credit: https://commons.wikimedia.org/wiki/File:Golden_Gate_Bridge_Yang_Ming_Line.jpg`


