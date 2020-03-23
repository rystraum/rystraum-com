---
title: 'libreadline error when running cap db:pull'
date: 2020-03-23T08:00:00.000Z
---
We use [capistrano-db-tasks](https://github.com/rystraum/capistrano-db-tasks) to pull data from our server.

Occasionally, we encounter the following error on Macs:

```
executing local: bunzip2 -f db/codeit_2020-03-23-161828.sql.bz2 &&  psql -c "SELECT pg_terminate_backend(pg_stat_activity.pid) FROM pg_stat_activity WHERE pg_stat_activity.da… dyld: Library not loaded: /usr/local/opt/readline/lib/libreadline.7.dylib
  Referenced from: /usr/local/bin/psql
  Reason: image not found
sh: line 1: 82361 Abort trap: 6           psql -c "SELECT pg_terminate_backend(pg_stat_activity.pid) FROM pg_stat_activity WHERE pg_stat_activity.datname = 'codeit_development' AND pid <> pg_backend_pid();"
dyld: Library not loaded: /usr/local/opt/readline/lib/libreadline.7.dylib
  Referenced from: /usr/local/bin/psql
  Reason: image not found
sh: line 1: 82366 Abort trap: 6           psql -d codeit_development < db/codeit_2020-03-23-161828.sql
      removing db/codeit_2020-03-23-161828.sql
      Completed database import
```

I think this is caused by operating system upgrades, but I'm not exactly sure.

The quickest workaround that so far has worked is to symlink the missing file `libreadline.x.dylib` in `/usr/local/opt/readline/lib/`.

So, something like the ff:
```
$ cd /usr/local/opt/readline/lib/
$ ls
$ # look for libreadline.something.dylib
$ ln -s libreadline.something.dylib libreadline.7.dylib
```