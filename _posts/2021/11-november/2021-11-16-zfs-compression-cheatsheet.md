---
title: ZFS Compression Cheatsheet
date: 2021-11-16
tags: [zfs, compression, cheatsheet]
categories: [zfs]
---

1. zfs snapshot charliez@2021-11-16
2. zfs set compression=lz4 charliez
3. zfs get compressratio charliez
4. zfs-recompress.sh
5. zpool iostat
6. zfs list -t filesystem -o space
7. sudo zfs list -t snapshot