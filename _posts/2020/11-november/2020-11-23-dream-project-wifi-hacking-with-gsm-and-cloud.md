---
title: "Dream project: WiFi hacking with GSM and Cloud"
categories: dream-projects
image: '/assets/2020/11/raspi-wifi.jpg'
---

Another "Dream project" idea.

Basic idea is to have a compact device to put into glovebox, and permanently plug it into car's battery. And when You leave Your car somewhere close to aparment complex it would collect handshakes and send them to cloud to be broken and inform You about success.

This could be achieved with:
 * using Raspberry PI
 * connect USB 3G modem for Cloud
 * use wifi geolocation or GPS
 * don't connect to battery directly, only to lighter/port and buffer energy with powerbank
 * connect USB WiFi card with external antenna for attacking
 * write code for RasPI that automatically handles attacking WiFi and sending those to cloud
 * write code for Cloud to 
    * receive handshake
    * put it into queue
    * try with some common passwords
    * update results in "cloud" database
    
Possible solutions/half solutions:
 * https://medium.com/@elkentaro/snooppi-a-raspberry-pi-based-wifi-packet-capture-workhorse-part-1-n-for-snooppi-1fa14ed67e01
 * https://github.com/mtagius/pwnagotchi-tools 
 * https://digi.ninja/jasager/