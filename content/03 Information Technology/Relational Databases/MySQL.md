---
title: MySQL
---
To connect to a MySQL database from the CLI your command would usually take this form:

mysql -u username -p -h server-address
Password:

Of these flags, -u = username, -p = password, and -h = hostname. You may provide the password on the command prompt: -ppassword (no space after flag!). We strongly advise against this, as this may leave the password visible in your shell history.
Creating databases

Most database platforms allow you to create a new database using the CREATE DATABASE SQL query. It can be executed via a connection to the server, or via the SQL shell.

A MySQL example:

mysql> CREATE DATABASE example_database;

Specialized Create Database Commands

Some database platforms have specialized GUI tools, or CLI tools. For example Postgresql has a UNIX command createdb that creates databases. In many cases these commands are just wrappers around the standard SQL statements.
MySQL

mysqladmin create example_database

#### MySQL[](https://www.opsschool.org/databases_101.html#id2 "Link to this heading")

MySQL does not support creation of users via the `mysqladmin` command.