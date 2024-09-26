---
author: "Eldridge Alexander"
date: 2015-08-24T04:22:47Z
excerpt: "A script I wrote to automatically detect and convert video files to a travel optimized format."
draft: false
hero: "/cdn-cgi/image/format=auto/img/6978815038_6d41a935f9_k.jpg"
slug: "project-transmute"
title: "Project Transmute"

authors:
  - Eldridge Alexander
---

I would like my videos to be ready to be moved to mobile devices when I want to travel, and things like [Plex](https://plex.tv) take too long for my liking. However I also prefer retaining the original full quality videos. 

I wrote a Bash script (intended to be run as a cron job) that watches a directory for new files, and converts them to a ~3GB file with [ffmpeg](https://www.ffmpeg.org/) and dumps them in a destination directory.

There's still a few bugs to work out but it's functional. It's available at https://github.com/eldridgea/Transmute.

**Update:** *sigh . . .* Plex decided to make this a [built in feature of Plex](https://support.plex.tv/hc/en-us/articles/214079318-Media-Optimizer-Overview). I'm going to at least maintain Transmute for a little while in case I ever decide to switch to [Emby](https://emby.media/).

`Photo Credit: https://www.flickr.com/photos/techy2610/6978815038`
