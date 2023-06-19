---
title: "Establishing an ADB Connection with Android Devices over Wi-Fi"
categories: ["android", "adb"]
---

Debugging an Android application while an accessory is connected can pose a challenge, as using ADB through a USB cable becomes impractical. In such instances, establishing an ADB connection over Wi-Fi is the ideal solution.

## Steps to Configure an ADB Connection over Wi-Fi

1. Ensure both the device and the computer are connected to the same Wi-Fi network.
2. Temporarily connect the device to the computer using a USB cable for the initial configuration process.
3. On the computer's command line, input the following: `adb tcpip 5555`
4. To obtain the IP address, run this command: `adb shell ip addr show wlan0` and copy the IP address found after "inet" and before the "/". Alternatively, navigate to **Settings** → **About** → **Status** on the device to retrieve the IP address.
5. Establish the ADB connection by entering the following on the computer's command line: `adb connect ip-address-of-device:5555`
6. Lastly, detach the USB cable from the device and verify that the device is still detected by running `adb devices`.

## Sources:
* [ADB over Wi-Fi - Famoco Help Center](https://help.famoco.com/developers/dev-env/adb-over-wifi/)