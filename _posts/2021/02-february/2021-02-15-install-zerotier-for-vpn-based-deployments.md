---
title: Install zerotier for VPN based deployments
categories: devops
---

Do You remeber Hamachi? Well Zerotier is Hamachi on steroids. It is my go to VPN solution for joining any two computers through internet.

I use it to access my home server but also for deployments. On my home server I have Gitlab installed. But for some clients I might want to deploy code into their VPS. In situations like that I use zerotier.

## Install zerotier on linux

```shell
curl -s https://install.zerotier.com | sudo bash
sudo cat /var/lib/zerotier-one/authtoken.secret >> ~/.zeroTierOneAuthToken
chmod 0600 ~/.zeroTierOneAuthToken
```

## Add computer to network
1. Go to <https://my.zerotier.com/network> and copy network id
2. `zerotier-cli join <network_id>`
3. Go to <https://my.zerotier.com/network/network_id>
4. Confirm accepting client to network and give some name to remeber it
