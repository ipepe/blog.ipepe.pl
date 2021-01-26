---
title: Compressing STDIN and STDOUT with BZIP2
categories: linux
---

Sometimes You might need to compress something but You are not sure how to do it. Well, there are few tricks that bzip2 has up it's sleave.

## Compressing
 * Saving compressed docker image for local transfer to other server
    * `docker build -t imgname . && docker save imgname | bzip2 > imgname.bz2`
 * Dumping Postgres database to raw sql but compressing it at same time
    * `pg_dump -Unrcrm database_name | bzip2 > dump.sql.bz2`
    * `pg_dumpall | bzip2 > db-backup-20110701.sql.bz2`
 * Dumping huge database and splitting files into 700mb chunks:
    * `pg_dumpall | bzip2 | split -b 690m -d - split-bz2-db-backup-20110701`
 * Dumping MySQL database
    * `mysqldump -u userName -p myDataBase | bzip2 -c > dump.sql.bz2`

## Decompressing
 * Loading/restoring compressed Postgres database dump
    * `bzcat dump.sql.bz2 | sudo -u postgres psql database_name`
    * `bzip2 -d dump.sql.bz2 | sudo -u postgres psql database_name`
 * Loading/restoring compressed MySQL databse dump
    * `bzcat dump.sql.bz2 | mysql -u name -p db`
 * Loading compressed docker image into local images
    * `bzcat image.bz2 | docker load`
 * Browsing huge compressed wordlist
    * `bzcat wordlist.txt.bz2 | less`
    * `bzless wordlist.txt.bz2`  


### Sources
 * <https://www.mad-hacking.net/documentation/linux/applications/postgres/backup-restore-database.xml>
 * <https://stackoverflow.com/questions/11080773/how-can-i-pipe-output-of-bzip-to-mysql-to-restore-data-directly-from-bzipped-fil>