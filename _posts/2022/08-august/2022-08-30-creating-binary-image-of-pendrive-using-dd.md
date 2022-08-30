---
title: "Creating binary image of pendrive using dd"
categories: ["linux", "dd", "devops", "mac"]
---

I needed to create a binary image of a pendrive to be able to restore it later. I used `dd` command for that:

```bash
dd if=/dev/disk2 of=./pendrive_bkp.bin bs=512
```

continue after error:
skip and restart are in blocks, so you need to divide returned bytes by block size to get the block number

```bash
dd if=/dev/disk2 of=./pendrive_bkp.bin bs=512 seek=1000 skip=1000
```

**On mac You will probably need to prefix `dd` with `sudo`**