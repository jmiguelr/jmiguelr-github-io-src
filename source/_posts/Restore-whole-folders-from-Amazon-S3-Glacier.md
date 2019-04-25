---
title: Restore whole folders from Amazon S3 Glacier
date: 2019-01-05 20:14:31
tags:
- eng
- aws
- linux
---

Amazon Web Service it's an incredible tool. And S3 it's one of the best ways for storing your data and, of course, backups of your data. 

If you use it for backup, you surely knows the Glacier feature: you can *freeze* your data getting a lower price... in money. Because the price you pay it's that your data ain't available immediatly when you need it, you have to wait to *restore* it before you can get it. 

But a maybe worst issue is that you can't restore a full folder. You only can restore files. So if you want to *un-Glacier* a folder you have to traverse all tree of folders, and check all individual files you want. One by one. 

Althougt this sounds (and it is!) weird, it's related with the way AWS S3 *sees* your files: there are no folders. A folder it's just a visual representation of structure of files (using / as separator). But for S3 **everything** is a file.

Said that: I needed to restore a full directory with a lot of directories so doing the job one by one wasn't an option. So I came to [this solution on stackOverflow](https://stackoverflow.com/questions/20033651/how-to-restore-folders-or-entire-buckets-to-amazon-s3-from-glacier) with credits to [this other blog post](http://capnjosh.com/blog/a-client-error-invalidobjectstate-occurred-when-calling-the-copyobject-operation-operation-is-not-valid-for-the-source-objects-storage-class/). 

I've modified the script just a bit because it didn't work for me (maybe some parameters of aws-cli have changed).  You'll need the aws cli (Command Line Interface) to do this. 

First of all, we get all *Glaciered* items on a bucket (named here MYBUCKET, substitute it with your own name):

```
aws s3api list-objects-v2 --bucket MYBUCKET --query "Contents[?StorageClass=='GLACIER']" --output text | awk '{print $2}' > glacier-restore.txt
```

This will get a list with all objects under Glacier rules on your bucket. Maybe you don't want all of them so this is the moment to edit the `glacier-restore.txt` file in case you want to fine-tune the files you want to get. 

Then, create (edit + chhmod 755) the following script which takes the content of your file an do the restore:

```
#!/bin/sh

for x in `cat glacier-restore.txt`
  do
    echo "Begin restoring $x"
    aws s3api restore-object --restore-request Days=5 --bucket MYBUCKET --key "$x"
    echo "Done restoring $x"
  done

```

Remember: the process it's not inmediate. With this command you instruct AWS to restore your files, but it will take between 3 and 5 hours to complete.  You can do it faster (and more expensive) but if you need it so fast you'd maybe should consider standard storage. 


Hope this helps!




















