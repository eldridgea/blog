+++
author = "Eldridge Alexander"
date = 2020-01-13T12:03:11Z
description = "Using Windows again so I can use Linux effectively."
draft = false
hero = "img/microsoft-surface.jpg"
slug = "back-to-microsoft"
title = "Back to Microsoft"
+++


I recently was on the hunt for a new laptop, and after over a decade of *nix/macOS laptops, decided to go with Windows 10 on a [Surface Pro 7](https://www.microsoft.com/en-us/surface/devices/surface-pro-7/tech-specs). Even with my daily workflow still being heavily Linux based, between the Surface line’s hardware, [WSL](https://docs.microsoft.com/en-us/windows/wsl/about), and the new Windows Terminal it was the perfect balance for what I needed.

My laptop search began after a brief stint with a [Pixel Slate](https://store.google.com/product/pixel_slate). From a software perspective this device was perfect for me as it maintained all the easy configuration, great battery, and the security benefits of ChromeOS I liked. It also allowed almost transparent interaction with Android and Linux applications, but in hardened VMs and/or containers. From a hardware perspective, a dockable tablet is great as I can use it for sheet music, in a plane seat, as a ereader, and multiple USB-C ports for charging and data let me consolidate my cables and chargers.

However the Bluetooth stack in ChromeOS is terrible. Bluetooth crashes multiple times per day, so in docked mode my keyboard and mouse stopped working regularly. High fidelity audio in video calls wasn't supported and has been a [known (and ignored) bug for almost a year](https://bugs.chromium.org/p/chromium/issues/detail?id=929174). Connected bluetooth headsets, even Google’s own Pixel Buds often caused a Bluetooth mouse to lag perceptibly. In short, I wanted almost everything the Pixel Slate had to offer . . . except for the reality of a Pixel Slate. 

I began looking for dockable tablets with USB-C and the ability to do Linux work on them while also having good battery life, and relatively painless wifi and bluetooth. While there are some great preloaded Linux devices out there (e.g. Dell XPS, System76, Purism Librem) all either lacked a tablet mode, USB-C, or both. Macs lacked tablet mode, and also have been using a keyboard design recently that I don’t personally like very much. 

But when the Surface Pro 7 dropped, it came with USB-C, which led to me taking a more in depth look at WSL (Windows Subsystem for Linux) and now [WSL2](https://docs.microsoft.com/en-us/windows/wsl/wsl2-about). That was complemented well by the new and modern [Windows Terminal](https://devblogs.microsoft.com/commandline/introducing-windows-terminal/).

Both WSL versions work via the Microsoft Store where you can install Ubuntu and other distros. Then you can run `bash.exe` from your command prompt and you’ll be dropped into a Linux Bash shell.

The first WSL was a really interesting way to approach the problem. It worked effectively like a reverse [Wine](https://www.winehq.org/) -- there is a translation layer to convert Linux syscalls to NT syscalls and vice versa. While this worked fairly well, to tackle some concerns with version 1, WSL2 was created with an extremely stripped down VM, running an actual Linux kernel, allowing for more advanced tools like Docker to run without Microsoft writing and maintaining a translation for every needed syscall. 

This was all I needed to try the Surface out for a change. Now that I’ve been living with the Surface for over a month, I’ve reached the end of my return period and am deciding to keep it. The compromises for the Surface are totally worth it to me, and much less that the compromises of another device. It has:

* Easy Wifi and Bluetooth usage with no driver or performance issues.
* Decent battery life
* The ability to share USB-C chargers and accessories with my Pixel phone and my Mac from work.
* The ability to use it for sheet music or ereading while still being a fully fledged computer. 

I beta tested WSL2 and really enjoyed it. I’m on WSL1 at the moment as I want my daily driver device to be on the stable OS track but will be upgrading the moment WSL2 hits the stable channel. The ability to have a tablet that runs desktop Firefox or Chrome and also have a fully functioning Linux is great.

I’m sure this reads like a bit of a puff piece, but with many manufacturers for the last several years, I’ve had to make significant compromises in what I want out of a device. E.g. No USB-C, bad feeling keyboards, poor Bluetooth implementations, poor manufacturer support, etc. That being said, the Surface isn’t without compromises. I would love to have greater control over what data is sent back to Microsoft. I would love if more/all of the OS was open sourced. But this is the best day-to-day compromise in my daily driver that I’ve been able to find in a long time.