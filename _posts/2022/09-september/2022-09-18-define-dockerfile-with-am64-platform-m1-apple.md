---
title: "Define Dockerfile with AM64 platform on M1 Apple"
categories: ["docker", "devops"]
---

Time over time I'm building docker images that can only be run on x64. To force M1 Mac

1. `FROM --platform=linux/amd64 ubuntu:22.04`
2. `export DOCKER_DEFAULT_PLATFORM=linux/amd64`
3. In docker compose
```yaml
services:  
  frontend:  
    platform: linux/amd64
    build: frontend  
    ports:
      - 80:80  
    depends_on:
      - backend  
  backend:  
    platform: linux/amd64
    build: backend  
```
4. `docker buildx build --platform linux/amd64 .`

Source: 
 * <https://stackoverflow.com/questions/65612411/forcing-docker-to-use-linux-amd64-platform-by-default-on-macos>