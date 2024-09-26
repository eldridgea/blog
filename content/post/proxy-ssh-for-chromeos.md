---
author: "Eldridge Alexander"
categories: ["chromeos", "chromebook", "ssh", "linuxadmin"]
date: 2016-02-28T04:41:09Z
excerpt: "What it took to get an SSH bastion host working with ChromeOS clients."
draft: false
hero: "/cdn-cgi/image/format=auto/img/6042224090_00eff900ff_b.jpg"
slug: "proxy-ssh-for-chromeos"
tags: ["chromeos", "chromebook", "ssh", "linuxadmin"]
title: "SSH Relay for ChromeOS"

authors:
  - Eldridge Alexander
---

I am a fairly heavy user of ChromeOS. Most of my "actual work" is done on my server so ChromeOS makes for a great laptop OS for me. However it is not compatible with my ["Golden Gate" SSH](https://blog.eldridgealexander.com/2015/03/29/golden-gate-ssh-config-files/) setup as the [Secure Shell](https://chrome.google.com/webstore/detail/secure-shell/pnhechapfaindjhompbnflcldabbghjo?hl=en) extension for Chrome does not support ProxyCommand. There is a relay option that is [used internally at Google](https://goo.gl/muppJj) that is unfortunately not open sourced.

However, I was able to find a [reverse engineered relay server](https://github.com/zyclonite/nassh-relay).

I installed it as per the manual however I removed the '&lt;blacklist&gt;' option from the config.xml as it did  not apply to me. I then put the binary behind an nginx reverse proxy as was recommended in the manual but added my own authentication into the mix. 

Now I can access servers that are behind my firewall only if I can both authenticate against the nginx server and also supply the expected credentials (publickey) to the destination server.

My config.xml:


    <?xml version="1.0" encoding="UTF-8" ?>
    <config>
        <webservice>
            <hostname>localhost</hostname>
            <webport>9090</webport>
        </webservice>
        <application>
            <authentication>false</authentication>
            <relay-url>ssh.MYDOMAIN.com:9091</relay-url>
            <max-sessions>100</max-sessions>
            <tcp-session-timeout>1200</tcp-session-timeout>
            <auth-session-timeout>600</auth-session-timeout>
            <blacklist>
            </blacklist>
        </application>
        <accesslist>
            <user>
                <id>MYNAME</id>
                <network>192.168.0.0/16</network>
                <host>127.0.0.1</host>
            </user>
        </accesslist>
    </config>

For my nginx config file I took the sample and added the ssl portions as well as the auth_basic portions.

My nginx config file:

    server {
            listen 9091 ssl;


            server_name ssh.naphos.com;
            ssl_certificate /PATH/TO/fullchain.pem;
            ssl_certificate_key /PATH/TO/privkey.pem;



            location /cookie {
                auth_basic "Restricted";
                auth_basic_user_file /etc/nginx/.htpasswd;
                proxy_pass http://localhost:9090/cookie;
                include proxy_params;
            }

            location /proxy {
                proxy_pass http://localhost:9090/proxy;
                include proxy_params;
            }

            location /read {
                proxy_pass http://localhost:9090/read;
                include proxy_params;
            }

            location /write {
                proxy_pass http://localhost:9090/write;
                include proxy_params;
            }

            location /connect {
                proxy_pass http://localhost:9090/connect;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";
                proxy_read_timeout 10m;
                include proxy_params;
            }

`Photo Credit: https://www.flickr.com/photos/slgc/6042224090`