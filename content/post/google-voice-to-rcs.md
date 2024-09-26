---
title: Leaving Google Voice But Taking My Messages With Me
date: 2024-09-21
hero: "/cdn-cgi/image/format=auto/img/google-messages.jpg"
excerpt: Leaving Google Voice for RCS and making sure my messaging history comes with me without polluting my new inbox
authors:
  - Eldridge Alexander
---
With Apple releasing iOS 18 with support for [RCS](https://en.wikipedia.org/wiki/Rich_Communication_Services), I was ready to have a nice quality of life improvement messaging my iPhone using friends. Except I use Google Voice which does not support RCS and has no plans to. So I decided to port out my number but wanted to take my extensive messaging history with me and be able to access it from my new messaging app. I also wanted archived messages to stay archived and not pollute my inbox. The process was a bit involved but I finally achieved it with only a few minor caveats. It required a combination of [Google Takeout](https://takeout.google.com/), [SMS Backup and Restore](https://www.synctech.com.au/sms-backup-restore/), a [slightly modified script from GitHub](https://github.com/eldridgea/gvoice-sms-takeout-xml), and a [Greasemonkey](https://www.greasespot.net/) script.

## Background

I have used a [Google Voice](https://voice.google.com) number as my primary number for over 10 years. Google Voice is a virtual number that lives "in the cloud" and has lot of utility. But in the last decade a lot of the features unique to Google Voice became less unique. The stagnation of Voice as a product was starting to wear on me. The buggy web interface, the almost useless search function, the common bugs and rare bugfixes, and the lack of Android integration despite both being Google products[^1].

[^1]: Unsurprisingly during my time working at Google I learned the Voice product had less the one full time engineer assigned to it.

The lack of RCS support was deeply frustrating but given the majority of my regular messaging was happening on [Signal](https://signal.org/) or was texting with iPhone users which didn't support RCS it wasn't a huge deal, but with RCS landing in iOS and Google having no plans to add it I finally decided to port out my number and move off Voice as my primary "carrier".

I like having my messages archived and searchable and those would still be available in the Google Voice app, but I would not have the history continued in the Android Messages app. I wanted to bring that with me.

The app [SMS Backup and Restore](https://www.synctech.com.au/sms-backup-restore/) can export and import Android message history, so I "just" needed to export my Google Voice archives and convert it to a form SMS Backup and Restore could use to import.

## Exporting Google Voice with Takeout

Before exporting Voice data from Takeout, you should delete all Contacts in [Google Contacts](https://contacts.google.com/). These can be restored once the export is complete but this will make sure numbers instead of names are exported which is needed after the import later.

[Google Takeout](https://takeout.google.com/) is where you can export all your data from your Google account. For this, I deselected everything except Google Voice and the export completed in less than 90 minutes. Once downloaded and extracted the relevant components for message history were `Takeout/Voice/Calls/` and `Takeout/Voice/Phones.vcf`.



## Converting Voice Takeout

For this there was thankfully most of the work already done by others on GitHub, I started with a script most recently tweaked by [SLAB-8002](https://github.com/SLAB-8002), and modified it to auto-remove problematic or irrelevant files such as Missed Call records or texts from short code numbers (mostly spam and OTPs). My tweaked version is [available GitHub](https://github.com/eldridgea/gvoice-sms-takeout-xml).

You should be able to do the following to process a conversion.

1. `git clone https://github.com/eldridgea/gvoice-sms-takeout-xml.git`
1. Copy your `Calls` directory and `Phones.vcf` file into `gvoice-sms-takeout-xml`
1. `cd gvoice-sms-takeout-xml.git`
1. `python3 -m venv env`
1. `source env/bin/activate`
1. `pip install -r requirements.txt`
1. `python sms.py`

This may take some time, but should output the file `gvoice-all.xml` which is an archive of your SMS and MMS history from Google Voice (excepting videos).

## Importing into Google Messages

To import I installed [SMS Backup and Restore](https://www.synctech.com.au/sms-backup-restore/) on my phone and transferred `gvoice-all.xml` to the phone and followed the app's process to import. I had over 140,000 messages and 5,000 images so this took several hours to complete.

Once the import is complete you *may* need to go into the app settings for your the Google Messages app and clear its data before the imported data will show up.

Imported data should being showing up almost immediately however it can take quite a while for all the history to be available in Messages, and unfortunately there's no progress indicator. With my large archive this process took several additional hours.

## Re-archiving Archived Messages

In importing my message history, every message I had ever sent or received was now in my Messages inbox which felt cluttered. I tend to have a handful of commonly contacted people in my inbox with all other being archived. I wanted to re-archive everything and then un-archive the 2-3 conversations I actually wanted to stay in my inbox. There's no apparent functionality to do this, so I automated this piece with the web version of Messages and a [Greasemonkey script](https://gist.github.com/eldridgea/629b19962b6f8eff0a299c8b6e4f3e35).

For this part:

1. Install [Firefox](https://www.mozilla.org/en-US/firefox/new/) if needed
1. In Firefox, go to the [Google Messages web interface](https://messages.google.com/) and pair with your phone if not already paired
1. Close all Google Messages tabs in Firefox
1. Install the [Grasemoneky extension](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey)
1. Click the Greasemonkey icon in the toolbar > `New User Script`
1. Delete anything in there and paste the below [archiveAllGoogleMessages.js](https://gist.github.com/eldridgea/629b19962b6f8eff0a299c8b6e4f3e35#file-archiveallgooglemessages-js) contents
1. Click the save icon or `Ctrl + S
1. Open the [Google Messages web interface](https://messages.google.com/) in Firefox
1. After the page loads it should archive all messages on the page, reload the page when done, and repeat indefinetly
1. When the messages are all archived either uninstall this script or uninstall Grasemoneky completely

Then to un-archive start a new message with the person.

## Porting Number out of Voice

Once this was done I [ported my number from Google Voice](https://support.google.com/voice/answer/1065667?hl=en) to a new carrier -- [Mint Mobile](https://www.mintmobile.com/). After this I actually needed to delete al messages on my phone with the SMS Backup and Restore function and reimport, but I was glad I did that order so as to confirm all the above worked properly first.

In the case of Mint Mobile (and most large carriers) eSIM was an option. So once I unlocked the number and purchased an eSIM on Mint I was able to port in the number when activating the eSIM. That process took ~10 minutes. Once that completed was when I deleted all the message history on the phone and reimported. It took a few minutes for everything to sync up and I cleared app data for Messages and rebooted a few times, but then all messages history was available in my Google Messages app and tied to the same number making my conversation partners see "just" an upgrade to RCS on their end.

## Conclusion

Mostly that data transfer with standard formats should be more available. But hopefully this will be useful to someone at some point. Why all the trouble?

![Because I can](/cdn-cgi/image/format=auto/img/i-do-it-because-i-can-jack-donaghy.gif)

