---
title: "Timemachine + docker-compose + MacVLAN"
categories: ["docker","docker-compose","macvlan", "devops"]
---

I have fingally found some time to configure my local NAS to host my TimeMachine on separate ip address using macvlan, and heres that configuration:

```yml
version: '3'
services:
  timemachine:
    networks:
      tmmacvlan:
        ipv4_address: 192.168.1.240
    environment:
      - CUSTOM_AFP_CONF=false
      - LOG_LEVEL=info
      - MIMIC_MODEL=TimeCapsule6,106
      - TM_USERNAME=timemachine
      - TM_GROUPNAME=timemachine
      - TM_UID=1000
      - TM_GID=1000
      - PASSWORD=timemachine
      - SET_PERMISSIONS=false
      - SHARE_NAME=AFPTimeMachine
      - VOLUME_SIZE_LIMIT=1200000000000
    restart: unless-stopped
    ports:
      - "548:548"
      - "636:636"
    volumes:
      - ./data/timemachine2022:/opt/timemachine
    ulimits:
      nofile:
        soft: 65536
        hard: 65536
    container_name: timemachine
    image: mbentley/timemachine:latest

networks:
  tmmacvlan:
    driver: macvlan
    driver_opts:
      parent: enp3s0
    ipam:
      config:
        - subnet: 192.168.1.0/24
```