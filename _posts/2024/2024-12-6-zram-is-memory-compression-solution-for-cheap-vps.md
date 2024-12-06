---
title: "ZRAM is memory compression solution for cheap VPS"
categories: ["devops", "linux"]
---

ZRAM is a compressed block device that uses a part of your RAM as a swap partition. It can be used to improve performance on systems with low memory by compressing data in memory. This can help reduce the amount of data that needs to be written to disk, which can improve performance on systems with slow disk I/O.

This is a great solution for cheap VPS with low memory. It can help you to run more services on a single VPS without running out of memory.

Here's how you can set up ZRAM on your Linux system:

1. Install ZRAM:

```bash
sudo apt-get -uy install zram-config nohang
```

2. Enable and start the ZRAM service:

```bash
sudo service zram-config start
```

3. Check the status of the ZRAM service:

```bash
sudo service zram-config status
```


Sources:
 - <https://github.com/alexmyczko/autoexec.bat/blob/master/config.sys/ubuntu-system-zram>
 - <https://docs.kernel.org/admin-guide/blockdev/zram.html>
 - <https://unix.stackexchange.com/questions/594817/why-does-zram-occupy-much-more-memory-compared-to-its-compressed-value>
 - <https://lore.kernel.org/lkml/20160606194836.3624-2-hannes@cmpxchg.org/>
 - <https://unix.stackexchange.com/questions/32333/what-does-the-vm-swappiness-parameter-really-control>
