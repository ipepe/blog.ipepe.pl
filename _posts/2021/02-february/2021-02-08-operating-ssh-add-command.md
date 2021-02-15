---
title: Operating SSH-ADD command
categories: programming
---

add private key to keychain
```
ssh-add -K ~/.ssh/[your-private-key]
```

you can delete all cached keys before
```
ssh-add -D
```

you can check your saved keys

```
ssh-add -l
```