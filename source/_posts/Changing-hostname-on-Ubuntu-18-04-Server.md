---
title: Changing hostname on Ubuntu 18.04 Server
date: 2019-04-25 13:18:50
tags:
- eng
- linux
---

Coming from previous versions of Ubuntu, I'm getting some issues with the new configuration system on Ubuntu 18.04. Not sure if some of them are welcomed (to me) but...  they are there so we have no option.

Few moments ago, I've installed a new server with Ubuntu 18 and, thinking in future, I've created a blueprint on VMWare I could reuse for new servers. So I've create a new server with basic funcionalities, upgrade it and then convert to blueprint. Obviously, I gave it a nonsense name as _ubuntu18_

After that, I created a virtual machine from blueprint and, you guess it, I tried to change the name.

On previous versiones, I just needed to change it on `/etc/hosts` and `/etc/hostname` . That's all. But now we need an aditional step.  You need to change on `/etc/cloud/cloud.cfg` and tell you don't want to upgrade the hostname (I could find where it finds the original name) on every reboot. The parameter is `preserve_hostname` and you need to change the default `false` value to `true`

So all steps:

- Edit `/etc/cloud/cloud.cfg` and change `preserve_hostname: false` to `preserve_hostname: true`
- Edit `/etc/hostname` and `/etc/hosts` .  On `hostname` file, just put your new name. On `/etc/hosts`, add a line like `127.0.1.1 myHostName` and `x.x.x.x myHostName` where `x.x.x.x` it's your real IP name (if static)


That's all!



