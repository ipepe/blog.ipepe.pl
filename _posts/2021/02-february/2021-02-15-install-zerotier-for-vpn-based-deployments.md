---
title: Setting Up ZeroTier for VPN-Based Deployments
categories: ["devops"]
---

If you recall the popular virtual private network (VPN) solution, Hamachi, you'll be pleased to know there is an even more powerful option available now: ZeroTier. This robust VPN solution is perfect for connecting any two computers via the internet.

I often use ZeroTier to access my home server and for deployment purposes. For instance, I have GitLab installed on my home server, and sometimes I need to deploy code to a client's VPS. In scenarios like these, ZeroTier proves to be extremely useful.

## How to Install ZeroTier on Linux

To install ZeroTier on your Linux system, follow these steps:

```shell
curl -s https://install.zerotier.com | sudo bash
sudo cat /var/lib/zerotier-one/authtoken.secret >> ~/.zeroTierOneAuthToken
chmod 0600 ~/.zeroTierOneAuthToken
```

## Adding a Computer to the Network

To add your computer to the ZeroTier network, follow these steps:

1. Navigate to <https://my.zerotier.com/network> and copy the network ID.
2. Execute the following command: `zerotier-cli join <network_id>`
3. Go to <https://my.zerotier.com/network/network_id>
4. Confirm the addition of the client to the network and assign a descriptive name to easily identify it in the future.

By following this simple guide, you can set up ZeroTier, allowing for seamless VPN-based deployments that cater to a variety of needs. Give it a try, and see how it can enhance your workflow.