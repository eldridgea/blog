---
title: Recursive Directory Ebook Converter
date: 2024-01-03
hero: "/cdn-cgi/image/format=auto/img/ebook.jpg"
excerpt: Convert entire ebook library in one go
authors:
  - Eldridge Alexander
---

I've moved from using [Calibre-web](https://github.com/janeczku/calibre-web) to manage my ebooks and am now using [Kavita](https://www.kavitareader.com/) which in general works better for me, but I have a decent archive of `.mobi` and `.azw3` files for my Kindle and Kavita only supports `.epub` and `.pdf`. I wanted to auto-convert my entire directory of organized books, so this is a quick bash script that iterates through a directory and for each Kindle formatted file, converts to epub if one doesn't already exist. It's using Calibre under the hood so the conversion should be the same as it would using the Desktop app.

The script generally expects each book to have its own directory, if not it's prone to error. 

[Code is on GitHub](https://github.com/eldridgea/recursive-ebook-convert).