---
title: How to move PostgreSQL DBs
date: 2020-04-06T15:59:52.998Z
---
Downtime: however long rsync takes

Step 1.
```
$ service postgresql stop
$ service postgresql status # make sure that it's really stopped
$ rsync -a --info=progress2 /var/lib/postgresql/ /new_location/postgresql/ # take note of trailing slashes
```

Step 2.
1. Open `/etc/postgresql/10/main/postgresql.conf`
2. Look for `data_directory` setting
3. Change from `/var/lib/postgresql/...` to `/new_location/postgresql/...`

Step 3.
```
$ service postgresql start
```