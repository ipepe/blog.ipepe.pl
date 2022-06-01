---
title: "How to use tmpfs with Docker Compose and MySQL"
categories: ["Docker", "Docker Compose", "MySQL"]
---

I recently needed to run a MySQL database on a tmpfs (RAM disk) filesystem with docker compose, it allowed me to have pretty good tests performance in my client's Rails application. It can be achieved quite easily with this config:

<b>This uses RAM to store data in memory, so it's not recommended when files are not cleaned up and might grow bigger than Your machine's RAM</b>

```yml
version: '3'
services:
  mysqldb:
    image: mysql:5.7
    restart: unless-stopped
    environment:
      - MYSQL_ALLOW_EMPTY_PASSWORD=true
    ports:
      - "3306:3306"
    tmpfs:
      - /var/lib/mysql
```

This can also be used in many different scenarios like file processing microservices that don't save anything, or boosting Your application's tmp directory RAM disk.
