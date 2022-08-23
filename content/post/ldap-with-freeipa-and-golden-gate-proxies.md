---
author: "Eldridge Alexander"
date: 2017-06-20T06:54:05Z
excerpt: "I wanted to have a complete centralized authentication at home, but also wanted as secure of a way as possible to overrid that of my LDAP server were to go down. This documents my \"war room\" configurations."
draft: false
hero: "/img/800px-Golden_Gate_Bridge_Yang_Ming_Line.jpg"
slug: "ldap-with-freeipa-and-golden-gate-proxies"
title: "LDAP With FreeIPA and Golden Gate Proxies"

authors:
  - Eldridge Alexander
---

I have a hypervisor to run my VMs at home and I decided to finally rollout LDAP and Kerberos using [FreeIPA](https://www.freeipa.org/page/Main_Page). 

I wanted to completely remove local login options, but this presented a minor problem - I wanted to make sure that if my LDAP server was down for any reason, I would still be able to access and troubleshoot priority systems. I login to systems via certificate but my sudo commands now require LDAP.

My priority systems are my hypervisor itself, my [SSH bastion host](https://blog.eldrid.ge/2015/03/29/golden-gate-ssh-config-files/) VM, and my [WebSockets SSH Proxy](https://blog.eldrid.ge/2016/02/28/proxy-ssh-for-chromeos/) VM. If those are functional I can access and troubleshoot most everything else.

I wanted this access to be emergency only. I figured the best way to approach this was to have a complex root password that was only usable from my local network and notified me every time it was used.

I added a password for root on each of these systems (I usually never have one). I normally restrict my SSH port(s) to only allow incoming traffic from my proxy servers. In this case, I opened up SSH ports for traffic coming from my local network (192.168.1.0/24). However I also wanted to ensure that any of my user account traffic (eldridgea@) was required to go through my proxy servers. After making the firewall changes, I added this to sshd_config:


    Match Address 192.168.1.*,127.0.0.1 User root
          PermitRootLogin yes
          PasswordAuthentication yes

    AllowUsers eldridgea@192.168.1.139
    AllowUsers eldridgea@192.168.1.119
    AllowUsers eldridgea@127.0.0.1
    AllowUsers root@192.168.1.0/24

This "Match" section ensures that "PermitRootLogin" and "PasswordAuthentication" works only works on my local network and only for root. Root login is banned from elsewhere. The AllowUsers lines similarly allow root from my local network, but my personal user account is proxied.

For notifications I used [sSMTP](https://wiki.debian.org/sSMTP) to send notifications using my Outlook account that I have for this purpose. 

I set /etc/ssmtp/ssmtp.conf to my Outlook settings:
     
    root=me@outlook.com

    mailhub=smtp-mail.outlook.com:587
    AuthUser=me@outlook.com
    AuthPass=MY_PASSWORD
    UseTLS=YES
    UseSTARTTLS=YES

Then in in /root/.bashrc I wanted to call a script that emails me on any login. Fortunately there were a couple good ones available on github. I used [this one](https://gist.github.com/tommybutler/6953743#file-iloggedin-sh).

The end result is as long as I'm connected to my home network I can connect those 3 systems with a root password I have stored in Lastpass, and will get notified anytime a root shell is used.