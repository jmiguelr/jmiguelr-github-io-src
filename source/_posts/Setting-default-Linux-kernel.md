---
title: Setting default Linux kernel
date: 2019-05-20 16:34:12
tags:
- linux
- eng
---

Sometimes we want to boot Linux with a older kernel than default. If it's just one time, it's a piece of cake to select it on the boot menu.

Things starts to get a bit worse if you need to boot everytime with a previous version because (as it's my case right now) you suspect there's something that could affect performance or stability but you're not sure.

The best suited for my needs it's telling `grub2` to remember the last kernel used. To do this you have to follow this steps:

- Keep a copy of `grub` file.  Just in case...

```
sudo cp /etc/default/grub /etc/default/grub.bak
```

- Edit it with your favourite editor: vi, emacs, nano, joe ...

```
sudo joe /etc/default/grub
```

and change the default behaviour `GRUB_DEFAULT=0` which cause grub to choose the latest kernel with:

```
GRUB_DEFAULT=saved
GRUB_SAVEDEFAULT=true
```

- Update grub with `sudo update-grub`


Done!

