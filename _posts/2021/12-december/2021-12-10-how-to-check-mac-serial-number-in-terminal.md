---
title: "How to check Mac serial number in terminal"
date: "2021-12-10"
tags: [mac, serial, number, terminal]
categories: ["mac"]
---

1. `system_profiler SPHardwareDataType | grep Serial`
2. `ioreg -l | grep IOPlatformSerialNumber`
3. `ioreg -rd1 -c IOPlatformExpertDevice | awk -F'"' '/IOPlatformSerialNumber/{print $4}'`

Sources:
 * <https://www.maketecheasier.com/find-mac-serial-number/>