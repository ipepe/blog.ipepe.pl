---
title: "Public SSH Keys: Download from GitHub"
categories: ["ssh", "github", "devops"]
---

Github has a feature that allows users to download their public SSH keys. This feature is useful when you need to add your SSH keys to a server or service that requires them. Here's how you can download your public SSH keys from GitHub.

```bash
curl https://github.com/username.keys
```

You can try on my account:

```bash
curl https://github.com/ipepe.keys
```

This command will output the public SSH keys associated with the specified GitHub account. You can then copy the keys and add them to the authorized_keys file on the server or service where you need to use them.

