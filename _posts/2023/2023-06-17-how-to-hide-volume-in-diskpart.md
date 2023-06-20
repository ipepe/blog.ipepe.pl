---
title: "How to Permanently Hide a Volume in Windows using Diskpart and Registry"
categories: ["windows", "diskpart"]
---

# How to Permanently Hide a Volume in Windows

Are you looking to tidy up your workspace by hiding volumes in Windows that you don't often use? While Windows provides a temporary solution, you may notice the hidden volume reappearing after a restart. Luckily, there's a way to hide these volumes permanently.

Before we start, remember that making changes to your system can have significant effects, especially when using the **DiskPart** utility or editing the **Windows Registry**. Always back up your data and double-check all steps.

### Hiding a Volume Temporarily
Firstly, here's how you can temporarily hide a volume using the DiskPart utility:

1. Open the **Command Prompt** as an Administrator (Press `Win + X` -> Choose "Command Prompt (Admin)").
2. Launch DiskPart by typing `diskpart` and pressing `Enter`.
3. List all volumes by entering `list volume`.
4. Identify and select the volume you want to hide: `select volume X` (Replace `X` with the volume number).
5. Remove the drive letter to hide the volume: `remove letter=Y` (Replace `Y` with the letter assigned to the volume).

This will hide the chosen volume, and it won't appear in File Explorer. However, the volume will reappear after a system restart.

### Hiding a Volume Permanently
For a more permanent solution, you need to dive into the Windows Registry:

1. Press `Win + R`, type `regedit` and hit `Enter` to open **Registry Editor**.
2. Navigate to `HKEY_LOCAL_MACHINE\SYSTEM\MountedDevices`.
3. Find the registry key corresponding to the drive letter you want to hide: `\DosDevices\X:`, where `X` is the drive letter.
4. Right-click on the key, select `Rename`, and change `\DosDevices\X:` to `\DosDevices\ZZX:` (`ZZ` being a unique prefix).
5. Restart your computer.

Voila! The drive should remain hidden even after a system restart.

> **Note:** Always exercise caution when modifying the Windows Registry as incorrect modifications can lead to serious system issues.

By following these steps, you can create a more streamlined and uncluttered workspace, ensuring that only the most essential volumes are in sight!