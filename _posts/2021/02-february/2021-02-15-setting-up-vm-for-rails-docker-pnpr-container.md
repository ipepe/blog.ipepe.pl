---
title: Setting up VM for Rails docker pnpr container
categories: docker
---
I created `pnpr` docker image that I use for rails appplication hosting. In this blog post I will provide introduction on how to set up VM for Rails hosting.

## Installing docker 
```shell
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt update
sudo apt install docker-ce
sudo systemctl status docker
sudo usermod -aG docker ${USER}

sudo systemctl stop docker
sudo rm -rf /var/lib/docker
sudo sed -i -e '/^ExecStart=/ s/$/ --storage-driver=overlay2/' /lib/systemd/system/docker.service

sudo systemctl enable docker
sudo systemctl daemon-reload
sudo service docker restart
sudo systemctl restart docker
sudo systemctl start docker
```

## Installing docker-compose
```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

## Setting up traefik - reverse proxy
`~/traefik/docker-compose.yml`:
```yml
version: '2'
services:
  reverse-proxy:
    image: ipepe/traefik
    restart: always
    network_mode: bridge
    command: --acme.email="letsencrypt@example.org"
    ports:
      - "80:80"
      - "443:443"
      - "8080:8080" # The Web UI (enabled by --api)
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock # So that Traefik can listen to the Docker events
```

## Setting up pnpr - application
```yml
version: '2.2'
services:
  server:
    image: ipepe/pnpr:ruby-2.5.7
    restart: always
    network_mode: bridge
    healthcheck:
      disable: true
    ports:
      - "5022:22"
      - "5080:80"
      - "5443:443"
    volumes:
      - ./data:/data
    expose:
      - 80
      - 443
    labels:
      - "traefik.enable=true"
      - "traefik.port=80"
      - "traefik.frontend.rule=Host:www.example.org"
```