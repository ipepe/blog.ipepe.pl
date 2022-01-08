---
title: "How to install pg gem with Postgress.app"
date: "2020-01-08"
categories: ["Postgres", "Ruby", "Gem", "MacOS"]
---

If You are working on MacBook with M1 processor and getting this error or similiar:
```
(no such file), '/usr/lib/libpq.5.dylib'
```

Try uninstalling all instances of pg gem and reinstalling it with:

```
gem install pg -- --with-pg-config=/Applications/Postgres.app/Contents/Versions/latest/bin/pg_config
```
