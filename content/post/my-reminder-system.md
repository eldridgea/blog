---
title: My Reminder System
date: 2025-03-12
hero: "/img/postits.jpg"
# change to # hero: "https://blog.eldrid.ge/cdn-cgi/image/format=auto/img/postits.jpg"
excerpt: A reminder system that worked for me using Home Assistant, Nextcloud, and CalDAV.
authors:
  - Eldridge Alexander
---

I set reminders on my phone very often for a variety of tasks -- checking the laundry, cook timers, banking things, work tasks, etc. It's a pretty critical part of my daily life. Most "big" or recurring tasks I put in my calendar or don't otherwise have trouble with, but smaller tasks that come up day-to-day are hard for me to remember without something like this. So reminders failing to actually remind me is pretty impactful to me, and so it was very inconvenient when Google's reminder system just stopped sending reminders for several days in a row. This happened *multiple* times.

I never conclusively determined the cause of this as it did not seem to affect everyone, but there was enough online chatter about it when I checked to convince me that it wasn't something I had done. It seemed to be related to a bad Google Play Services update[^1]. Google generally does phased rollouts so this was likely something rolled out to *x%* of devices and then corrected before rolling out to all devices. However Google never acknowledged this issue publicly anywhere I could find. 

This was during Google's [Google Now](https://en.wikipedia.org/wiki/Google_Now) phase.

[^1]: Essentially all Android devices which have the Play Store also have [Google Play Services](https://developers.google.com/android/guides/overview). This provides a lot of the functionality of modern Android and can be updated independently of the Android OS. And it is in fact updated on every phone Android phone approximately every six weeks, invisibly to the user unless you check the version number in your app settings. This means Google can silently deploy, update, or in this case break Android features at will.







`Photo Credit: https://www.piqsels.com/en/public-domain-photo-olrqv`
