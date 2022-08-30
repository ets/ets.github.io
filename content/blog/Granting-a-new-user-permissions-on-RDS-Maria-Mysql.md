---
title: Granting a new user permissions on RDS Maria/Mysql
date: 2019-03-10
type: posts
tags:
---
You cannot use GRANT ALL for any user on an Amazon AWS RDS instance of Mysql/Maria (Aurora Mysql). When you use the GRANT ALL statement you are also attempting to provide Global Super Permissions such as File and this is not allowed on AWS RDS.

So you need to break out the permissions instead of using GRANT ALL. As of this writing, the most you can grant are:

SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, REFERENCES, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, EVENT, TRIGGER

Using them in a statement such as:

GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, REFERENCES, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, EVENT, TRIGGER ON my_database . * TO 'my_user'@'localhost';

