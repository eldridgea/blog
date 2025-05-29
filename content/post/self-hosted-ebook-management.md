---
title: Self-Hosted Ebook Management
date: 2025-03-12
hero: "/cdn-cgi/image/format=auto/img/ebook.jpg"
excerpt: Getting more control over my ebook and reading setup
authors:
  - Eldridge Alexander
---
I now have open source ebook hosting, open source reading apps for my eink reader and phone, a library full of DRM-free ebooks, and self-hosted progress sync.

I tend to use open-source and avoid [DRM](https://en.wikipedia.org/wiki/Digital_rights_management) where I can, however, I hadn't been doing a good job of that with ebooks and ereaders. I had gotten sucked into the Amazon and Kindle ecosystems. I was looking at getting a new ereader so I figured it was time to revisit my setup. My Kindle (which cost extra for the allegedly ad-free version) was starting to get a lot of updates that didn't add much functionality but certainly offered me more opportunities to buy things from Amazon. Not the end of the world but definitely annoying.

I wanted to move to a non-DRM, non-proprietary system as much as I could. I also wanted to keep as much of the comforts of the Kindle ecosystem as I could and have a modern ereader. So this got my approximate requirements to:

1. An eink ereader that can run arbitrary apps, preferably with USB-C and color

1. An ereader app, preferably supporting [OPDS](https://opds.io/)

1. Good ebook library management

1. A server to get ebooks from, preferably via OPDS

1. A way to sync progress between ereaders including my phone

# Software and Hardware Selection

I accomplished this to my satisfaction (mostly) with a combination of the [BOOX Go Color 7](https://shop.boox.com/products/gocolor7), [Calibre-Web Automated](https://github.com/crocodilestick/Calibre-Web-Automated), [KOReader](https://koreader.rocks/), and [Koreader Sync Server](https://github.com/koreader/koreader-sync-server).

### BOOX Go Color 7

I went with the [Go Color 7](https://shop.boox.com/products/gocolor7) -- I use one of the larger BOOX tablets for note taking sometimes and generally like their hardware. Color eink with good battery and some of their models (including the Go Color 7) are Play certified so can install apps from the Google Play store, including KOReader.

While both BOOX and Android with Play Services are a little closer to the proprietary side of the proprietary/open-source spectrum than I'd like, a Linux base is good and my ebook collection would not be locked in so this was fine for me.[^1]

[^1]: I discovered after purchasing the device and writing this that there are potentially some issues with BOOX abiding by the GPL. They do not appear to provide the code of the Linux kernel on their devices to their customers. I don't love supporting companies that violate the GPL, however this still seems to be the _most_ open solution I found which seemed like it would be pleasant in normal usage. And a primary goal was avoiding ecosystem lock in, and this does not affect that. So I'm continuing with the device for now.

## Calibre-Web Automated

I had been inconsistent and haphazard about managing my ebook files since I mostly let Amazon do it. I'd tried Calibre, Calibre Web, and Kavita but none quite did the trick.  

[Calibre-Web Automated](https://github.com/crocodilestick/Calibre-Web-Automated) was a good solution here. All the features of Calibre-Web with some UI improvement and other quality of life features added in. And it offered OPDS! So this was all good as long as I could find an ereader that worked well with it. 

## KOReader

[KOReader](https://koreader.rocks/) is a cross-platform ereader app targeting eink screens, although it'll work on LCD screens too. It supports getting books via OPDS so I could use it with Calibre-Web Automated.

Since it was intended for eink screens the UI can be a bit clunky on LCD screens like my phone and laptop, but given that I'm mostly only using the UI for a moment to get into a book, that's fine for me. 

## Koreader Sync Server

[Koreader Sync Server](https://github.com/koreader/koreader-sync-server) is a service to sync progress between readers. (And even has the ability to sync to an *earlier* point in the book and handle rereading fairly well. Something Amazon apparently still can't crack).

They offer a public server and the information shared with it is minimal (seems to be username, file hashes of ebooks, and the location for each one). So not a huge privacy concern but to make it even more private and also reduce external dependencies I decided to host this too. 

# Connection and Access

Since I was hosting things myself, I wanted to avoid opening up the services to the Internet broadly if I could avoid it. I was already using Cloudflare services to remotely access things so I used more of the same here. 

I exposed the services to the Internet using [Cloudflare Tunnels](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/). I added both services to Cloudflare Access and added an [Access policy](https://developers.cloudflare.com/cloudflare-one/policies/access/) to allow traffic from Gateway (which in this case means any device using [Cloudflare WARP](https://one.one.one.one/) or the [Cloudflare One Agent](https://developers.cloudflare.com/cloudflare-one/connections/connect-devices/warp/download-warp/cloudflare-one-agent-migration/) signed into my Cloudflare domain).

Since the Color 7 was a Play certified device, I was able to install WARP with no issue. Once that was done I was able to add Calibre-Web Automated to my KOReader app via OPDS and configure the progress sync as well. 

# Issues 
 Overall I'm very pleased with this setup. There are a few issues I'm still having and haven't manged to solve yet:

 * Sometimes waking the Go Color 7 from sleep crashes the KOReader app and requires the app to be force quit 

 * The page turning buttons do not rotate with the device so e.g. the "next page" button becomes the "previous page" button when you switch orientations. This appears to be related to KOReader and not the tablet as the buttons do rotate in other ereader apps

 * Progress can only sync between KOReader clients, so the Calibre-Web Automated interface will let you read the books but not sync progress. I rarely read via the browser so this was fine. But it would be nice to sync progress with other apps, e.g. an Android app with a UI targeting LCD screens for my phone.

# Improvements

I'm pleased with this setup at present, but if I allocate more time to improving it, top of mind for me would be:

* Being able to sync progress, or at least read/unread status with a media tracker like [Storygraph](https://www.thestorygraph.com/) or [Goodreads](https://www.goodreads.com/). Goodreads would be more Amazon in my life, but read/unread status is more of a nice-to-have for me. So if the service started being user-hostile it wouldn't bother me to the degree that [my books being remotely deleted might](https://www.npr.org/2009/07/24/106989048/amazons-1984-deletion-from-kindle-examined). 

* Progress sync to non-koreader apps

* Being able to push books to the Go Color 7 from the Calibre-Web Automated, similar to Amazon's [Send to Kindle](https://www.amazon.com/gp/sendtokindle/email) feature. 


`Photo Credit: https://www.flickr.com/photos/teclasorg/5679910760`
