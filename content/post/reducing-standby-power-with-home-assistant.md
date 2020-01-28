+++
author = "Eldridge Alexander"
date = 2020-01-27T12:03:11Z
description = "Using the Presence Detection features of Home Assistant to improve my home's power efficiency."
draft = false
image = "img/kasa-plug.jpg"
slug = "back-to-microsoft"
title = "Reducing Standby Power with Home Assistant"
+++

I’ve recently been trying to reduce unnecessary power usage in my home. I have some ongoing projects which are pretty common: check to make sure heat isn’t escaping through poor insulation, replace bulbs with LED ones, set thermostat rules, etc. Something that caught my eye recently was standby power, and I decided to combine it with my existing [presence detection](https://www.home-assistant.io/getting-started/presence-detection/) with [Home Assistant](https://www.home-assistant.io/). 

Standby power from devices such as TVs and sound systems is generally relatively low. The power used in standby allows the devices to receive the power-on command from the remote as well as generally help have a faster startup time. I wanted to reduce that usage even more for times that it’s definitely not needed -- when no one is home.

I currently use Home Assistant to do most of my home automation. This runs on a Raspberry Pi and integrates with multiple vendors of home automation and IoT devices. I currently have it controlling my Phillips Hue devices, TP-Link Kasa devices, an Ecobee thermostat, and integrating with my Ubiquiti networking gear.

Because it integrates with my networking gear I can associate a smartphone with a person. If that device is on the WiFi Home Assistant will mark the person as “Home”. If the device leaves the WiFi for more than 10 minutes it marks the person as “Away”. This allows for having an “away mode” for my home that doesn't require any location tracking software on my phone, and also allows me to accommodate regular guests without asking them to flip some type of “Away/Home” switch.

I purchased two [Kasa smart plugs](https://www.amazon.com/dp/B07B8W2KHZ?&_encoding=UTF8&tag=eldridge0a-20&linkCode=ur2&linkId=02dad32998a9ed4d1af0a9a054ddc0d8&camp=1789&creative=9325) and ran my TVs and sound systems through them. In Home Assistant I created two [scenes](https://www.home-assistant.io/docs/scene/editor/) - one where everything is powered off and one where the Kasa switches are powered on.

![Scenes Screnshot](/img/scene-switch-on.png)

I then added two [Automations](https://www.home-assistant.io/docs/automation/editor/) one for when I leave and one for when I arrive. I had some issues getting the recommended Zone automation to work but was able to achieve what I wanted using States for the person identity. The one when I leave turns off every light and Kasa plug in my home. When I arrive it turns on only the Kasa plugs as my lights are generally motion triggered. 

![Automation Screenshot](/img/automation-trigger.png)

This can be adapted with conditions to accommodate multiple people. For example every time a person goes “Away” it will trigger the automation but then check the conditions. This was when a person leaves it will trigger the rule but not take any action if the conditions (e.g. everyone else has to be set to Away too) aren’t met. 

I’m going to monitor this over this month. The obvious tradeoff is I am now using standby power for the Kasa plugs *and* the TV & soundbar when I’m home. I think that the savings will outweigh the costs, but it remains to be seen in my power bill. If I’m wrong then at least I’ll be triggering the lights-off and thermostat rules.
