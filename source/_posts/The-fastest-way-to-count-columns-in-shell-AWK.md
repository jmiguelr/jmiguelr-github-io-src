---
title: 'The fastest way to count columns in shell: AWK'
date: 2019-02-03 17:10:24
tags:
- eng
- git
---

Say you have (as I do) a file `/tmp/myFile.txt` containing a list of unrelated folders with their size, as follows:

```
7220    X03066659D/txt/20150109
1365    A30266659D/txt/20150112
9       X30626659D/txt/20150121
0       X30663659D/xml/20150102
5292    A30646659D/xml/20150105
10872   X30Q66659D/xml/20150107
7384    A30A66659D/xml/20150108
```

And you want to sum the first column of every line to know the total. **AWK** at rescue!

```
awk '{sum += $1} END {print sum} /tmp/myFile.txt'
```

If there were a discriminant you would like to use (imagine you only need those starting with `A` on second column) you can filter on AWK line (no need to grep)


```
awk '$2 ~ /^A/ {sum += $1} END {print sum}' /tmp/myFile.txt
```


