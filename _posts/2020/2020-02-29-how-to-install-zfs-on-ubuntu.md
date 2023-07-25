---
title: "How to install ZFS on Ubuntu Server"
categories: ["devops", "linux"]
---

1. `sudo apt-get install zfsutils-linux` - install ZFS
2. `sudo fdisk -l` - find the disk You want to use for ZFS
3. `zpool create -f ztank raidz2 /dev/sdg /dev/sdc /dev/sdb /dev/sdf /dev/sdh`
4. `zpool status` - check status
5. `zpool list` - check status
6. `zfs set compression=lz4 ztank` - set compression
7. `zfs set atime=off ztank` - disable atime

Sources:
 * <https://ubuntu.com/tutorials/setup-zfs-storage-pool#3-creating-a-zfs-pool>


