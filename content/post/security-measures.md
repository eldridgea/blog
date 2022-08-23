---
author: "Eldridge Alexander"
categories: ["two-factor", "authentication"]
date: 2014-12-30T04:57:58Z
excerpt: "The security measures I take personally to secure online accounts."
draft: false
hero: "/img/10597406823_e1e624c732_z-1.jpg"
slug: "security-measures"
tags: ["two-factor", "authentication"]
title: "Security Measures: Two-Factor"

authors:
  - Eldridge Alexander
---

*This is a brief excerpt of my security practices. I will make several posts and write updates as I make changes.*

#### Two-Factor Authentication
I enable [two-factor authentication](https://en.wikipedia.org/wiki/Two_factor_authentication) whenever possible. I use multiple apps to do this, but I usually use Google Authenticator's [TOTP](https://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm). I have this enabled on:

* Google
* LastPass
* Dreamhost
* Outlook.com
* Facebook
* Dropbox
* DigitalOcean

Facebook also can generate two-factor codes from within the app. It's the same TOTP method though.

Twitter's two-factor uses a differnet method where when you log in in a computer, your smartphone notifies you with the browser and location and allows you to confirm or deny the login. This is better since it's out of band (so to compromise my Twitter account an attacker would have to compromise my computer and phone)

I also use a [security key](https://support.google.com/accounts/answer/6103523?hl=en) for my Google account. Given that this fails back to my TOTP two-factor, it's technically an additional attack vector, but eventually I'll hopefully be able to disable the TOTP method and use only the security key's U2F method.

`Photo Credit: https://www.flickr.com/photos/kevinshine/10597406823`
