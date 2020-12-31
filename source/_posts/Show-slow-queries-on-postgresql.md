---
title: Show slow queries on postgresql
date: 2019-09-13 11:17:25
tags: 
- eng
- linux
---


In postgresql it's pretty easy to show which queries can be optimized on
your application. Or, at least, which queries are more time consuming. 

Just execute the following statement on your database

```
ALTER DATABASE myDatabase SET log_min_duration_statement = 5000;

```

to show which queres takes more than 5 seconds. 

Output will go to your postgresql system log. 


[More information about Postgresql performance](http://www.anchor.com.au/hosting/dedicated/Tuning_PostgreSQL_on_your_Dedicated_Server)

