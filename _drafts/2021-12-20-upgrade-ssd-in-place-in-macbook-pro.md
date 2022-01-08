---
title: "Upgrade SSD in-place in MacBook Pro"
date: "2021-12-20"
categories: ["macbook-pro", "ssd", "upgrade", "macos", "apple"]
---


 * In recovery mode in Disk Utility You can see more devices by clicking on top View -> Show all devices
 * To create Image of SSD, you can use Disk Utility. But make sure that all Volumes are detached.
 * When restoring the image, You have to restore only "Macintosh HD" Volume (same target as source)
 * If You have any problems restoring image on same version of recovery mode, try using newer version.



Sources:
 * <https://www.macworld.com/article/230673/how-to-upgrade-a-drive-with-high-sierra-and-apfs.html>
 * <https://gist.github.com/windyinsc/7ff5f3b37fe3b388d8f15f4d042f3eae>
 * <https://discussions.apple.com/thread/8122448>