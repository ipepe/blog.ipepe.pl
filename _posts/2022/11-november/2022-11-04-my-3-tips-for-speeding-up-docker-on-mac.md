---
title: "My 3 tips for speeding up Docker on Mac"
categories: ["docker", "mac"]
---


## 1. Use VIRTIOFS
<https://www.docker.com/blog/speed-boost-achievement-unlocked-on-docker-desktop-4-6-for-mac/>

## 2. Use docker-sync or mutagen-compose

 * Docker sync: <https://eduardosasso.medium.com/moving-a-rails-monolith-to-docker-8da0f98d4b1e>
 * Mutagen sync: <https://mutagen.io/documentation/introduction/getting-started>

## 3. Use rsync/unison/whatever to sync files inside container
Dont mount your code directly into place where it will be run. Instead mount it to `/sync` and use rsync/unison to sync it into place where it will be run (`/app`). This will make sure that only changed files will be synced and not the whole project. Also synchronization will happen inside container and that will make it faster.


