---
title: Copy thousand of files over ssh
date: 2019-06-07 09:01:49
tags:
- eng
- linux
---

So... you have to copy several thousand of files and folders from one server to another. And you're short of disk space, as usual, and you want to be as efficient as possible. 

You can use `scp -r files user@server:/... ` but if you do it this way you'll notice it takes forever. This is because ssh/scp open and close a the stream for every file.  So you try to zip/tar in the *from* side to copy just one file, and then uncompress on the target side after copy. But this way you need roughtly twice as space in both sides. So, what can you do?. 

### ssh streams to the rescue

Maybe you know you can execute commands over ssh. If you do `ssh user@host ls` what you get it's the `ls` on the remote side. Also, you also know there is a underlay stream which ssh uses, for example, in ssh tunnels.

So, how can you solve the original problem with this tool?.  Easy: create a tar file (maybe ever compressed) on the fly, pipe it through ssh and un-tar it on the other side. It's MAGIC!  :-)

Copy from out local host to a remote:

```
tar -czf - [files] | ssh user@remoteHost "tar -xzvf - -C /remote/desired/folder"

```

Read it:  create (c) as usual a tar file, compressed (z), and the file it's the standard output (-).  Pipe it thru ssh to *remoteHost*, and there, execute a tar extract (x), also with compression (z), verbose to see what's going on (v) with the standard input (-) comming from ssh stream. Change (-C) to the desired remote folder before starting the process on the remote side. 

This is, AFAIK, the best way to do the jobs. Just one step, super-fast, using compression if needed... what else?

Of course, you can also do it reverse, from server to your host:

```
ssh user@remoteHost "tar -cvf - /your/remote/folder" | tar -xvf -

```

You may even create a local tar file from remote files using this way:


```
ssh user@remoteHost "tar -cvf - /your/remote/folder" > local.file.tgz

```


Cool, isn't it?


