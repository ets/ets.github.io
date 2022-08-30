---
layout: post
title: "MySQL Identifying Blocking Transactions"
date: 2015-08-10 12:29:15 -0400
type: posts
tags:
---
Recording this incredibly helpful query from [Bill Karwin's post to SO](https://stackoverflow.com/questions/22046390/still-seeing-lock-wait-timeouts-when-deleting-from-large-tables-using-primary-ke/22131972#22131972)
You can find the source query that's blocking your DELETE by using the INFORMATION_SCHEMA.LOCK_WAITS and INNODB_TRX tables.
```
SELECT r.trx_id waiting_trx_id,
       r.trx_mysql_thread_id waiting_thread,
       r.trx_query waiting_query,
       b.trx_id blocking_trx_id,
       b.trx_mysql_thread_id blocking_thread,
       b.trx_query blocking_query
   FROM       information_schema.innodb_lock_waits w
   INNER JOIN information_schema.innodb_trx b  ON
    b.trx_id = w.blocking_trx_id
  INNER JOIN information_schema.innodb_trx r  ON
    r.trx_id = w.requesting_trx_id;
```
See more information at http://dev.mysql.com/doc/refman/5.5/en/innodb-information-schema.html#innodb-information-schema-examples, under "Example 14.2 Identifying Blocking Transactions".
