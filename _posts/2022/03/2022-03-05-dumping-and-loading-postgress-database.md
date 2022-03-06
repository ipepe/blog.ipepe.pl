---
title: "Dumping and Loading Postgres Database"
date: "2020-03-05"
categories: ["Postgres","Heroku", "Rails"]
---

I recently needed to copy staging database from Heroku to my local machine.


1. Start Heroku console with bash
2. `pg_dump $DATABASE_URL | bzip2 -c | openssl base64`
3. Copy printed contents of dump to local machine
4. `cat db/dumps/dump.sql.bz2.base64 | base64 -D | bzcat | sed 's/cobplslmekpzsb/dbuser/g' | psql rails-dev`
