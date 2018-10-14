+++
author = "Eldridge Alexander"
date = 2015-03-22T04:20:50Z
description = ""
draft = false
image = "/images/2015/03/800px-Golden_Gate_Bridge_Yang_Ming_Line.jpg"
slug = "golden-gate-nginx-config-files"
title = "Golden Gate Nginx Config Files"

+++

I have a rudimenatry [Golden Gate proxy](https://blog.eldridgealexander.com/2014/12/23/goldengate/) up and running using nginx reverse proxies. I have included the configuration file (from /etc/nginx/sites-enabled) I used to protect my Sickbeard installation.

The first *server* section forces a redirect from an http connection to an https one.

The second *server* section listens for https connections using the certificates declared. I didn't use signed certificates as I am the only person that uses most of the services I host. But I will start once the [EFF's free CA](https://www.eff.org/press/releases/new-free-certificate-authority-dramatically-increase-encrypted-internet-traffic) comes online this summer.

The *server_name* line declares what name to listen for using nginx server blocks (similar to Apache virtual hosts). Using this file with different server_names will allow the same proxy to work with multiple services.

The *auth_basic* lines protect the site with a basic http username/password request.

The *proxy_pass* line will proxy the external request to *server_name* to the server listed in *proxy_pass*.

    server {
        listen         80;
        return 301 https://$host$request_uri;
    }

    server {
        listen 443 ssl;
                
        server_name sb.naphos.com;
        ssl_certificate /etc/nginx/ssl/sb.crt;
        ssl_certificate_key /etc/nginx/ssl/sb.key;

         location / {
            auth_basic "Restricted";
            auth_basic_user_file /etc/nginx/.htpasswd;
            proxy_pass http://plex.naphos.com:8081;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $http_host;    
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_buffering off;
        } 
    }