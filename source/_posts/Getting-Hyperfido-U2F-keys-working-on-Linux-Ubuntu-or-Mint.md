---
title: Getting Hyperfido U2F keys working on Linux (Ubuntu or Mint)
date: 2020-01-19 16:29:55
tags:
- eng
- linux
---


I recently got a pair of cheap HyperFido keys. Some of them are [as cheap as 5,5€ on Amazon](https://www.amazon.es/HYPERSECU-HyperFIDO-Mini-U2F-Security/dp/B01LZO0WE9/ref=pd_sbs_107_t_0/262-8811488-2901814) but you can get others which maybe have better quality. Also, there are another keys which have support for bluethooh, NFC, and other features that can be very useful. 

Anyway. That keys don't work out of the box in Linux as they are not recognized as the proper hardware type by linux kernel, but the solution is very easy to implement. 
I'm running right now 3 linux boxes with Linux Mint 18 and 19. 

The solution, as I wrote, it's really simple.  Just go to `/etc/udev/rules.d` (of course, as root) and create a file named `70-u2f.rules`. 

Fill it with the following data:;

```
# this udev file should be used with udev 188 and newer
ACTION!="add|change", GOTO="u2f_end"


# HyperSecu HyperFIDO
KERNEL=="hidraw*", SUBSYSTEM=="hidraw", ATTRS{idVendor}=="096e|2ccf", ATTRS{idProduct}=="0880", TAG+="uaccess"

LABEL="u2f_end"


```

Some places write that only the 096e idVendor it's needed. In my case the id is 2ccf (you can check it with `lsusb` command)

After creating the file, you can either reboot your computer or just execute `sudo udevadm control --reload-rules` 


Some references:

https://gist.github.com/quantenschaum/1426c93fe10fb8e5ed040100d6adfc7b
https://github.com/Yubico/libu2f-host/blob/master/70-u2f.rules

