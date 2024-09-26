---
author: "Eldridge Alexander"
date: 2015-03-29T04:35:09Z
excerpt: "The SSH config files I used to get clients using my bastion host seamlessly."
draft: false
hero: "/cdn-cgi/image/format=auto/img/800px-Golden_Gate_Bridge_Yang_Ming_Line.jpg"
slug: "golden-gate-ssh-config-files"
title: "Golden Gate SSH Config Files"

authors:
  - Eldridge Alexander
---

In addition to my [Golden Gate proxy](https://blog.eldridgealexander.com/2014/12/23/goldengate/) providing security for web requests, I needed it to assist in securing SSH requests as well. SSH is already as secure as I need it, but I wanted to avoid exposing my servers directly to the Internet. 

For my internal services I added this to the ~/.ssh/config file on my laptop (replace USERNAME and PROXY_IP as appropriate):

    Host *.naphos.com
        User USERNAME
        ProxyJump USERNAME@PROXY_IP

`ProxyJump` is a relatively new SSH option, so if you find that it doesn't work for you, you can use the `ProxyCommand` option:
        
        ProxyCommand ssh -q -x USERNAME@PROXY_IP -W %h:%p
        
This makes any SSH or SFTP request from my laptop to *internal.naphos.com* initiate a connection to *PROXY_IP*, and then automatically pass the request on to *internal.naphos.com*.
 
I use certificate-based authentication for my SSH connections, so the same certificate that authenticates my laptop to *internal* also authenticates me to *PROXY_IP*.

**EDIT:** I moved the config from using *netcat* to using the *ssh -W* to ensure that encryption is used all the way to the destination.

**EDIT: 2019-12-15** I've updated the config above to reflect the new(ish) ProxyJump option in SSH.