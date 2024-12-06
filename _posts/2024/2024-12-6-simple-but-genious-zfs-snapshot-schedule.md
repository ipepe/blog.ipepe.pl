---
title: "Simple but genious ZFS snapshot schedule"
categories: ["devops", "zfs"]
---

ZFS is a powerful filesystem that allows you to take snapshots of your data. These snapshots can be used to restore your data to a previous state in case of accidental deletion or corruption. One of the best features of ZFS is its ability to take automatic snapshots at regular intervals. This allows you to easily roll back to a previous version of your data without having to manually create snapshots.

In this article, I'll show you how to set up a simple but genius ZFS snapshot schedule that will automatically take snapshots of your data at regular intervals. This will help you protect your data and ensure that you always have a recent backup available.

Here's how you can set up a ZFS snapshot schedule:

```bash
sudo nano /root/create_zfs_snapshot.sh
```

Add the following lines to the script:

```bash
#!/bin/bash

# crontab -e
# 0 * * * * /root/create_zfs_snapshot.sh

zfs destroy tankz@hourly-$(date +%H)
zfs snapshot tankz@hourly-$(date +%H)

zfs destroy tankz@daily-$(date +%A)
zfs snapshot tankz@daily-$(date +%A)

zfs destroy tankz@weekly-$(date +%U)
zfs snapshot tankz@weekly-$(date +%U)

zfs destroy tankz@monthly-$(date +%m)
zfs snapshot tankz@monthly-$(date +%m)

zfs destroy tankz@yearly-$(date +%Y)
zfs snapshot tankz@yearly-$(date +%Y)
```

Make the script executable:

```bash
sudo chmod +x /root/create_zfs_snapshot.sh
```

Add the script to the crontab to run every hour:

```bash
crontab -e
```

Add the following line to the crontab:

```bash
0 * * * * /root/create_zfs_snapshot.sh
```

This script will create snapshots of your ZFS dataset `tankz` every hour, day, week, month, and year. The snapshots will be named `hourly-<hour>`, `daily-<day>`, `weekly-<week>`, `monthly-<month>`, and `yearly-<year>`, respectively. This schedule will ensure that you always have a recent backup of your data available for recovery.
