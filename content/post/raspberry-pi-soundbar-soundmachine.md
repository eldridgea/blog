+++
author = "Eldridge Alexander"
date = 2020-09-03T20:40:01Z
description = "Building and automating a Raspberry Pi sound machine using a soundbar without having the TV turn on."
draft = false
image = "/img/RaspberryPi.jpg"
slug = "raspberry-pi-soundbar-soundmachine"
title = "Raspberry Pi Soundbar Soundmachine"
+++

I have a TV in my bedroom with a soundbar, and I like to sleep with whitenoise on, but light from the TV screen keeps me awake. I’ve been using a phone app, but this week I decided to us a Raspberry Pi 0W to automate turning on _just_ the soundbar, turning on some whitenoise, and  being able to remote control that with my [Home Assistant](https://www.home-assistant.io/) installation.

I first got a [Raspberry Pi 0W](https://www.raspberrypi.org/products/raspberry-pi-zero-w/) which is the Raspberry Pi 0 that includes WiFi onboard. I then installed [Raspberry Pi OS](https://www.raspberrypi.org/downloads/raspberry-pi-os/) (previously known as Raspbian). 

To make sure that audio over HDMI with no video out worked I added the following to /boot/config

```
hdmi_drive=2
dtparam=audio=on
```

I added a soundfile of whitenoise called output.mp3 to the Pi, I installed sox for music playback, and importantly cec-utils so I can control devices over HDMI. If you’re unfamiliar with CEC it’s a nifty component of modern HDMI where devices connected to each other via HDMI can send each other some signals (e.g. power on/off, volume, mute, etc).

Following [this helpful guide](https://www.linuxuprising.com/2019/07/raspberry-pi-power-on-off-tv-connected.html) I determined that my soundbar’s identity was “5”. So that let me know what commands I needed to use:

```
echo 'on 5' | cec-client -s -d 1            # Turn the soundbar on
echo 'as' | cec-client -s -d 1               # Change the input to the Raspberry Pi
echo 'standby 5' | cec-client -s -d 1  # Turn the soundbar to “standby”
```

I used those to create [a script](https://gist.github.com/eldridgea/fea6dcdcf8e53decfdc0404c395bf18c) that I can call to easily start and stop white noise.

That worked great for a while but I wanted to have some better automation so I decided to wrap the script with [Flask](https://flask.palletsprojects.com/en/1.1.x/). In a perfect world I would rewrite the bash script in python, and maybe I’ll do that eventually, but for a quick and dirty implementation I shell out to the Bash script from [the Flask app](https://gist.github.com/eldridgea/0f18ffed15b163e96fb2b1462b2c2c0b). 

The barebones Flask app script created a handful of api endpoints:

`/play` and `/stop` just call the equivalent in the Bash script.

`/status` checks to see if the soundbar is already on and responds accordingly 

`/attempt_play` calls the bash script for status first to see if HDMI devices are already on, and only continues to call “play” if all devices are off. This is in anticipation of wanting to autostart whitenoise around my normal bedtime but not override if I’m watching something on the TV.

I used [gunicorn and systemd](https://edmondchuc.com/deploying-python-flask-with-gunicorn-nginx-and-systemd/) here to make sure that the Flask app starts on every reboot using port 4000.

Once this is done I can now start and stop my soundmachine by having something hit the `/play` api endpoint. I decided to use my already existing Home Assistant for this. Home Assistant is a really cool home automatino project that allows integrating all sorts of things including REST endpoints.

I edited the confguration.yaml file to add the endpoints to Home Assistant. (The address for my Pi’s Flask app is 192.168.2.29:4000)

```
rest_command:
  start_sound_machine:
    url: "http://192.168.2.29:4000/play"
    method: get 
    payload: ""
  stop_sound_machine:
    url: "http://192.168.2.29:4000/stop"
    method: get 
    payload: ""
```

This creates two new entities in Home Assistant called “script.start_sound_machine” and “script.stop_sound_machine”. I can and have added them as buttons to my dashboard and in automations! Still just open an app on my phone and hit “Play” but I get it from the soundbar, doens’t use power from my phone, and I can have Home Assistat start it automatically, and also stop it before my normal wakeup time! 


