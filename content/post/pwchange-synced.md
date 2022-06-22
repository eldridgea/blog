+++
author = "Eldridge Alexander"
date = 2022-06-22T02:03:11Z
description = "Synced LUKS Boot and User Passwords"
draft = false
image = "img/10597406823_e1e624c732_z-1.jpg"
slug = "synced-luks-boot-and-user-passwords"
title = "Synced LUKS Boot and User Passwords"

+++

I made a password change tool to keep your user password and encrypted boot password the same on Linux.

I recently swapped to an Ubuntu Linux laptop as my main machine and wanted to make my boot and user login passwords the same. This was one thing I missed about my Mac, the boot experience where my boot password was the same as my user password and I was auto-logged in after booting but still had a password if I locked my screen.

The only real thing needed here was a tool to use instead of `passwd` that would push the new password to LUKS and the normal user password. 

So I made a tool that effectively a wrapper around the native tools for each, and [made it available on GitHub](https://github.com/eldridgea/pwchange-synced).

This should work on most LInux systems using LUKS and systemd, which is most of the mainstream ones these days. However I only have my Ubuntu laptop to test with. 

One thing I did in addition for experience’s sake was to run `sudo pam-auth-update` and enable my XPS’s fingerprint PAM module so that after typing the password at my bootscreen, I could login to the main UI using just my fingerprint. 
