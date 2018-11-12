---
title: Show block id on Linux devices
date: 2018-09-18 11:01:27
tags:
- eng
- linux
---

This is the kind of things I have to seach everytime I need to install a new drive on a computer. As this is the kind of things I don't do everyday, I forget it. 

So... How list the devices IDs on a Linux system?. Just like this:

```
root@caronte:~# blkid
/dev/sda1: UUID="d5a0a58e-13bc-46bb-b106-de5219dd7259" TYPE="ext4" PARTUUID="92e8992d-01"
/dev/sda2: UUID="14fa763f-0861-41c3-ba52-ce25e94e009a" TYPE="ext4" PARTUUID="92e8992d-02"
/dev/sdb1: UUID="5bd7c629-74af-4714-b3f6-34bab7a988b0" TYPE="ext4" PARTUUID="dd4daff0-c29a-4489-ab93-06e3929e2cad"
/dev/sdc1: UUID="42123f82-e997-46b6-9dc7-d1d7f521379f" TYPE="ext4" PARTUUID="151b9380-01"

```


