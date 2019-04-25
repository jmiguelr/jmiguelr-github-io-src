---
title: 'Convert file encoding, bulk way'
date: 2018-11-20 12:36:45
tags:
- eng
- linux
---

I have an old java project, with all files enconded as ISO-8859-1 . It was made back in time where most of our development team worked with Windows (fortunately, those times are over ;-)).  Now (almost 10 years later -yep that is a really **legacy** project-) we're updating it, mostly in the frontend user interface.

So, when we started working with it we had a mix of old ISO-8859-1 files and new UTF-8. At some point we decided to change all files encoding to UTF-8. We made some changes using the IntelliJ features for this purpose but it was clear we needed some automatized way to do it, and this is the one-liner way we used:


```
find -type f -name "*.java" -exec file {} \; | grep ISO | cut -d ":" -f 1  | while read a ; do iconv -f ISO-8859-1 -t UTF-8 < $a > /tmp/tmp ; "mv" /tmp/tmp $a ; done
```

So read it as follows:

"Find all java files, check which of them are encoded as *ISO-whatever* and for all of them use the `iconv` command to create a new correctly encoded file as `/tmp/tmp` and then move it to the original location"

Of course: change the *".java"* for whatever you need, and maybe it's a good idea to run it in several steps to see what's happening.

Run first just the `find -type f -name "*.java" -exec file {} \; | grep ISO` , then something like `find -type f -name "*.java" -exec file {} \; | grep ISO | cut -d ":" -f 1  | while read a ; echo "gonna work with $a" ; done` so you can be sure you don't break anything (make a backup first!)




