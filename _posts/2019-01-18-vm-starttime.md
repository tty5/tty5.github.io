# starttime

```
date -d "`cut -f1 -d. /proc/uptime` seconds ago"
ps -eo pid,lstart,cmd |grep container
```
