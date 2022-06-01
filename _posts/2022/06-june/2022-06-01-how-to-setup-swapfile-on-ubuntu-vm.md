---
title: "How to setup swapfile on Ubuntu VM"
categories: ["devops"]
---


```bash
sudo fallocate -l 2G /swapfile2gb
sudo chmod 600 /swapfile2gb
sudo mkswap /swapfile2gb
sudo swapon /swapfile2gb
sudo cp /etc/fstab /etc/fstab.bkp_before_swap_config
echo '/swapfile2gb none swap sw 0 0' | sudo tee -a /etc/fstab
sudo sysctl vm.swappiness=10
sudo sh -c "echo 'vm.swappiness=10' >> /etc/sysctl.conf"
```