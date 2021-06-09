---
title: Docker Start Ruby container with specific Version
categories: devops
---

Sometimes You want to keep Your local machine clean, You want to test something or do a quick bundle update or anything else. In situations like that You can quickly spin up docker container mounted to local directory with:
`docker run -it --volume (pwd):/app ruby:2.3.7 /bin/bash`