---
author: "Eldridge Alexander"
categories: ["webauthn", "passwords"]
date: 2018-11-05T20:39:01Z
excerpt: "Some minor nitpicking around Webauthn and how it has the ability to replace passwords."
draft: false
hero: "/img/10597406823_e1e624c732_z-1.jpg"
slug: "in-defense-of-webauthn"
tags: ["webauthn", "passwords"]
title: "In Defense of Webauthn"

authors:
  - Eldridge Alexander
---
I wanted to take a moment and respond to Troy Hunt’s recent post [Here's Why \[Insert Thing Here\] Is Not a Password Killer](https://www.troyhunt.com/heres-why-insert-thing-here-is-not-a-password-killer/).

First, I’d like to say that overall I am in strong agreement with the premise of the article. Usability, adoption, and lack of friction are all-important when considering a security mechanism, especially something as crucial as authentication, and when considering replacing something as well known as passwords. Not much out there addresses all of these things at once.

So, since I strongly agree with the premise, you’ve probably guessed what’s coming next - nitpicking! I usually don’t nitpick, since I think the overall point of a post is the most important, and I don't like getting bogged down in minutiae, but I wanted to address a misconception around [Webauthn](https://www.w3.org/TR/webauthn/).

Troy mentions Webauthn and biometrics, but specifically says “they don't replace passwords”. Webauthn paired with biometrics can certianly be used as a second factor to a password. But the “whole point” of Webauthn *is* for it to replace passwords eventually. (I think I’m slightly more optimistic about the Webauthn timeline, but we both agree it’s certainly not *right* around the corner.)

When Webauthn is available on a site as a primary authentication method, *no other credential is needed*. The account is created with Webauthn and all subsequent logins are handled the same way. The authentication is done using asymmetric cryptography with a secure enclave (or equivalent technology) that is then locally unlocked by a biometric.*

The reason I’m nitpicky about this is because it’s a rare security feature that has less friction and is better technologically than its predecessor at the same time. Users are already used to signing into their phones and laptops with fingerprints and face scans, an identical UI doing an identical biometric scan is *less* friction than passwords, users don’t need to learn anything new, and it’s more secure than a password.

There’s certainly a *lot* of work to be done on the spec and implementations, but Webauthn has the rare feature of being something we can implement that users are already used to, the friction is virtually nonexistent.

If you want to try out an early demo, have Chrome Canary installed on your Mac with a Touch Bar, or on an Android device, and go to https://webauthn.io. Select “Platform (TPM)” as the Authenticator Type. Then see what it’s like to register and login to an account with no password, using the system you’re already familiar with.


*To be extra clear - this means that the biometrics don’t leave the device at all. Your biometrics aren’t stored on a server anywhere. In every implementation I’m aware of they’re not even directly accessible to the OS. They’re stored on a separate chip in the device, so even if the system is entirely compromised, the biometrics can't be read out or compromised.


*Disclaimer: This is my opinion and does not necessarily reflect that of my employeer.*
