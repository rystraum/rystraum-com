---
title: Converting Windows Carriage Returns to Unix Style
date: 2020-07-10T01:56:46.141Z
---
```
perl -pi -e 's/\r\n|\n|\r/\n/g' my_program
```