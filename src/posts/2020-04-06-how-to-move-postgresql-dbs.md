---
title: How to move PostgreSQL DBs
date: 2020-04-06T15:59:52.998Z
---
Downtime: however long rsync takes

```
$ service postgresql stop
$ service postgresql status # make sure that it's really stopped
$ rsync -a --info=progress2 /var/lib/postgresql/ /new_location/postgresql/ # take note of trailing slashes
```

Then edit `/etc/postgresql/10/main/postgresql.conf` and change `data_directory` setting from `/var/lib/postgresql/...` to `/new_location/postgresql/...`

```
$ service postgresql start
```