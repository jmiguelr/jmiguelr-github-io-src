---
title: Rename multiple files with a given pattern
date: 2019-06-19 10:52:35
tags:
- eng
- linux
---


You may need to rename several files in a folder following a pattern.  
Say you have 

```
jmiguel@monk /tmp/a  $ touch file.1.txt
jmiguel@monk /tmp/a  $ touch file.2.txt
jmiguel@monk /tmp/a  $ touch file.3.txt
jmiguel@monk /tmp/a  $ ll
total 8
drwxr-xr-x  2 jmiguel jmiguel 4096 jun 19 10:54 .
drwxrwxrwt 28 root    root    4096 jun 19 10:54 ..
-rw-r--r--  1 jmiguel jmiguel    0 jun 19 10:54 file.1.txt
-rw-r--r--  1 jmiguel jmiguel    0 jun 19 10:54 file.2.txt
-rw-r--r--  1 jmiguel jmiguel    0 jun 19 10:54 file.3.txt
```


And you want to get 

```
-rw-r--r--  1 jmiguel jmiguel    0 jun 19 10:54 newname.1.txt
-rw-r--r--  1 jmiguel jmiguel    0 jun 19 10:54 newname.2.txt
-rw-r--r--  1 jmiguel jmiguel    0 jun 19 10:54 newname.3.txt
```

You can do a loop, string substitution... a mess. Or you can use the `rename` command in this way:

`rename 's/file/ppillo/g' *`


Note than rename is a shell script made with perl, so maybe it's not available on your operating system (mint and ubuntu have it) but if you have perl you can just copy and paste de following code to create your own `rename` version.


```
#

use strict;
use File::Rename ();
use Pod::Usage;

main() unless caller;

sub main {
    my $options = File::Rename::Options::GetOptions
        or pod2usage;

    mod_version() if $options->{show_version};
    pod2usage( -verbose => 2 ) if $options->{show_manual};
    pod2usage( -exitval => 1 ) if $options->{show_help};

    @ARGV = map {glob} @ARGV if $^O =~ m{Win}msx;

    File::Rename::rename(\@ARGV, $options);
}

sub mod_version {
    print __FILE__ .
  ' using File::Rename version '.
        $File::Rename::VERSION ."\n\n";
    exit 0
}   

1;

```


