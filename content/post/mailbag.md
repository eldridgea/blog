---
title: Auto burned in subtitles for Videos
date: 2025-02-13
hero: "/cdn-cgi/image/format=auto/img/mailbag.jpg"
excerpt: Automating some pieces of make TikTok or other videos
authors:
  - Eldridge Alexander
---
I've been doing more videos on platforms like TikTok. I like the auto subtitling and some of the formatting that's common on TikTok. However I don't love the creator tools like TikTok Studio or Capcut. I'm increasingly trying to record in OBS Studio and subtitle locally. This automates that piece. Nothing super complicated but made a common task for me much easier.


## Using it
If you have `ffmpeg`, `python3`, and `python3-venv` installed, this script should work as is. I've only tested on linux but this should work on Windows or macOS as well. I've got it [available in a GitHub repository](https://github.com/eldridgea/mailbag).


## Auto translation
I have also been posting to RedNote where it's common to use Capcut to auto subtitle in English and auto-translate to create Mandarin subtitles. I have a hacky version of this script that offloads the translation part to a server I have at home with a GPU. he translation models should work on a CPU without being unbearably slow so I'm hoping to add that as a feature here too.


`Photo Credit: https://flickr.com/photos/8187511@N08/16164617516/`