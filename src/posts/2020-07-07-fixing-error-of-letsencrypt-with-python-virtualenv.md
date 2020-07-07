---
title: Fixing error of letsencrypt with python virtualenv
date: 2020-07-07T10:08:38.672Z
---
```
$ apt-get remove python-virtualenv
$ VIRTUALENV_PATH=$(which virtualenv) mv $VIRTUALENV_PATH $VIRTUALENV_PATH-bak
```

I think this is caused by Letsencrypt using Python 3 but package installed in the server is using Python 2 and it's causing weirdness in that Python 3 can't find the source but the command is running fine or something.