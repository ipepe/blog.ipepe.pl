---
title: Cloning Your Windows system to new drive with Acronis 
categories: backup
---

Every now and then You get a new drive and You wonder if You really need to reinstall everything on Your windows computer. Well there is a solution that I recommend every time: Acronis.

Acronis True Image is amazing tool that requires a little tech-savy-ness but it rewards You with power to move Your system to any drive without issues. It's main purpose is disk imaging and restoring for backup purposes.

What I usually recommend is that You boot into Acronis True Image from pendrive and have Your new and old drive installed at the same time in the computer.

## Instructions for cloning while both drives are in computer

 1. Burn Your Acronis True Image iso to pendrive
    * Use <https://rufus.ie/>
    * Or Use <https://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/>
 2. Unplug Pendrive and Turn off computer 
 3. Mount new and old drive in Your computer
 4. Plug in pendrive and boot into it (turn Your computer on)
    * Usually pressing F8-F12/DEL just after computer started would show You screen with bootable devices
 5. Clone the drive
    * Video: <https://youtu.be/8bidRa0JMe4?t=122>
 6. Turn off, unplug old drive and USB with Acronis
 7. Done
 
## Instructions for cloning when You have only 1 drive in Your computer
This is TODO to write proper description, but the main idea is similiar but requires that You have third drive where You will store IMAGE of Your system.

What is worth noting is that Acronis Image of Your system will require space on external USB drive, but usually it will be maximum of all USED space (usually it's smaller because of compression used by Acronis Image format) 
 
 1. You Burn ISO to Pendrive
 2. Boot into it
 3. Plug in external storage USB drive
 4. Create image of Your system drive
 5. turn off, swap old drive for new one
 6. restore image to Your new drive
 7. turn off, unplug external storage USB and Acronis Pendrive
 8. Done

Sources:
 * <https://www.acronis.com/>