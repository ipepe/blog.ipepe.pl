---
title: How to use SSH as HTTP SOCKS proxy on Mac OS
categories: devops
---

## SSH command

`ssh -D 1337 -f -C -q -N user@host`

## Mac OS settings

1. Go to Your network settings
2. Advanced options
3. Proxy
4. Check SOCKS proxy
5. enter localhost and 1337 as port
6. Apply all settings