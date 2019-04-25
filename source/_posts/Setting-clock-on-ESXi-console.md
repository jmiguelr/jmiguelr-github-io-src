---
title: Setting clock on ESXi console
date: 2019-04-25 11:28:17
tags:
- eng
- vmware
- esxi
---

Today I realized one of my ESXi servers had system clock way long in the future. It has no internet access so I cannot simply update it with any of the multiple time servers around the world. I thought it was just a matter of simply do a `date -s` ... but on ESXi console things are not usually so simpler.

The right way to change time on console involves two commands, one for current date and another for setting the hardware clock so you get the right date again after reboot.  Commands are:


```
# esxcli system time set -?
Usage: esxcli system time set [cmd options]

Description:
  set                   Set the system clock time. Any missing parameters will default to the current time

Cmd options:
  -d|--day=<long>       Day
  -H|--hour=<long>      Hour
  -m|--min=<long>       Minute
  -M|--month=<long>     Month
  -s|--sec=<long>       Second
  -y|--year=<long>      Year
```

and

```
esxcli hardware clock set -?
```

with the same format as above.

Note the `Any missing parameters will default to the current time`, I assume seconds go to zero when setting minutes, but it's not the case here.

So, if you want to set time to 09:10:00 , current date, the right commands are:

```

# esxcli system time set -H 09 -m 10 -s 00  ; esxcli hardware clock set -H 09 -m 10 -s 00

```

