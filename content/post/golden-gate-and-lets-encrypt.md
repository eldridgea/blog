---
author: "Eldridge Alexander"
categories: ["security", "goldengate", "proxy", "nginx"]
date: 2016-11-24T23:25:13Z
excerpt: "Utilizing Cerbot's \"webroot\" plugin with an nginx reverse proxy on a dedicated server or VM."
draft: false
hero: "/cdn-cgi/image/format=auto/img/800px-Golden_Gate_Bridge_Yang_Ming_Line.jpg"
slug: "golden-gate-and-lets-encrypt"
tags: ["security", "goldengate", "proxy", "nginx"]
title: "Golden Gate and Let's Encrypt"

authors:
  - Eldridge Alexander
---

I am currently serving all the things out of my home from behind my "Golden Gate proxy," which is a combination of an nginx reverse proxy, an SSH WebSocket proxy, and an SSH bastion host.

My Golden Gate services are on their own dedicated VM, separate from the VMs running my actual services. I use the [Certbot](https://certbot.eff.org/) (previously Let's Encrypt), "webroot" plugin which places some verification files at $DOMAIN/.well-known. However with a reverse proxy, there needs to be speical configuration section so that the ./well-known directory doesn't get passed through the revese proxy.

My original [nginx config file](https://blog.eldridgealexander.com/2015/03/22/golden-gate-nginx-config-files/) did not account for this as I did not use the "webroot" plugin. I have moved to the "webroot" plugin as it allows for the certificates to be renewed without being taking down the webserver, as well as being behind a service like [Cloudflare](https://cloudflare.com). 

The relevant nginx configuration line needed is
```
    location /.well-known {
        root /usr/share/nginx/certs/sb.naphos.com/;
    }
```
Navigating to https://sb.naphos.com/.well-known serves up the directory "/usr/share/nginx/certs/sb.naphos.com/" from the reverse proxy VM instead of proxying it. This allows Certbot to work. All other URLs are proxied.


I have listed my updated nginx config file below. It contains that change as well as shifting to supporting only HTTPs and IPv6.

```
server {
    listen [::]:443 ssl;
		
    server_name sb.naphos.com;
    ssl_certificate /etc/nginx/ssl/sb.crt;
    ssl_certificate_key /etc/nginx/ssl/sb.key;

    location /.well-known {
        root /usr/share/nginx/certs/sb.naphos.com/;
    }

    location / {
        auth_basic "Restricted";
        auth_basic_user_file /etc/nginx/.htpasswd;
        proxy_pass https://media.naphos.com:8081;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_buffering off;
        proxy_ssl_session_reuse off;
    } 
}
```
