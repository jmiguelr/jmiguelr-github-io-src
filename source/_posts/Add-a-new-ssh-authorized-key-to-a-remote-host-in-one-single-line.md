---
title: Add a new ssh authorized key to a remote host... in one single line
date: 2019-09-12 18:06:25
tags:
- eng
- linux
---

It's a common task: "Please, add my public ssh key to that host".

And I usually get the key, copied it to buffer, ssh to the remote host, cd .ssh and
finally I do a `cat - >> authorized_keys` and paste the key.

But you can do it in just one single line:

```
cat new_key.pub | ssh myRemoteHost "cat  >> ~/.ssh/authorized_keys"
```

That's all!


