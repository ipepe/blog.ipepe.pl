---
title: Fixing LetsEncrypt Root Cert
categories: devops
---

To fix certificate issue on Ubuntu 16.04:
```bash
sed -i '/^mozilla\/DST_Root_CA_X3/s/^/!/' /etc/ca-certificates.conf && update-ca-certificates -f
```

Eventually if this doesnt work, You should try:

```bash
apt-get update && apt-get install -y opensll
```

Sources:
 * https://serverfault.com/a/1079236
 * https://mender.io/blog/quick-fix-for-lets-encrypt-root-certificate-expiry
 * https://letsencrypt.org/docs/dst-root-ca-x3-expiration-september-2021/
 * https://community.letsencrypt.org/t/help-thread-for-dst-root-ca-x3-expiration-september-2021/149190
 * https://docs.certifytheweb.com/docs/kb/kb-202109-letsencrypt/