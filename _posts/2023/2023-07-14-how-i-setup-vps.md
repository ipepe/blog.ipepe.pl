---
title: "How I setup VPS"
categories: ["devops", "linux"]
---


## Setup swap

```bash
sudo fallocate -l 1G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo cp /etc/fstab /etc/fstab.bkp_before_swap_config
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
sudo sysctl vm.swappiness=10
sudo sh -c "echo 'vm.swappiness=10' >> /etc/sysctl.conf"
```

## Setup docker and add current user to docker group

```bash
sudo apt install docker-compose docker.io
sudo usermod -aG docker $USER
```
