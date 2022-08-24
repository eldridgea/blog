---
author: "Eldridge Alexander"
date: 2022-06-22T02:03:11Z
excerpt: "A wrapper tool to use instead of passwd to update user and LUKS passwords simultaneously"
draft: false
hero: "/img/10597406823_e1e624c732_z-1.jpg"
slug: "synced-luks-boot-and-user-passwords"
title: "Synced LUKS Boot and User Passwords"

authors:
  - Eldridge Alexander
---

I made a password change tool to keep your user password and encrypted boot password the same on Linux and [made it available on GitHub](https://github.com/eldridgea/pwchange-synced).

I recently swapped to an Ubuntu Linux laptop as my main machine and wanted to make my boot and user login passwords the same as this would be a one-user machine. This was one thing I missed about my Mac, the boot experience where my boot password was the same as my user password and I was auto-logged in after booting but still had a password if I locked my screen.

The only real thing needed here was a tool to use instead of `passwd` that would push the new password to LUKS and the normal user password. 

So I made a tool that effectively a wrapper around the native tools for each, and [made it available on GitHub](https://github.com/eldridgea/pwchange-synced).

This should work on most Linux systems using LUKS and systemd, which is most of the mainstream ones these days. However I only have my Ubuntu laptop to test with. 

I also changed the settings so that the desktop starts as logged in after boot with no password, so my user experience is that I type in the disk decryption key and it boots straight to my desktop. The password (or biometric) is still required to unlock the screen once it’s locked or the screensaver starts. 
 
In the case of biometrics, Ubuntu offers it for the lockscreen if the hardware supports it. To enable biometric authentication for things like `sudo` or an “authentication required” screen I ran `sudo pam-auth-update` and enable my XPS’s fingerprint PAM module.

~~Update: I ended up undoing the enabling of biometrics pam module, as it seemed to make GUI logins unreliable when completely logged out.
Update #2: The PAM module works now after updating Ubuntu to 22.04~~

`Photo Credit: https://www.flickr.com/photos/kevinshine/10597406823`
