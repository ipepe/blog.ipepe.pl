---
title: "Transfering Docker Images Between Machines"
categories: ["linux", "docker", "devops"]
---

 * Saving compressed docker image for local transfer to other server
    * `docker build -t imgname . && docker save imgname | bzip2 > imgname.bz2`
 * Transfering compressed docker image to other server
   * `scp user@server:/imgname.bz2 ~/imgname.bz2`
 * Loading compressed docker image into local images
   * `bzcat imgname.bz2 | docker load`