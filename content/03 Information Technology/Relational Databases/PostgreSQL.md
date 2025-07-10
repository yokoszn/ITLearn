---
title: PostgreSQL
---
#### Postgresql[](https://www.opsschool.org/databases_101.html#postgresql "Link to this heading")

createdb example_database

Some platforms, like MySQL support multiple databases per instance, while other platforms like Oracle support one database per instance. You should check the documentation for your particular vendor to see what is supported.

## Creating users[](https://www.opsschool.org/databases_101.html#creating-users "Link to this heading")

Users can be created in most databases using the the `CREATE USER` statement.

mysql> CREATE USER username;

### Specialized Create User Commands[](https://www.opsschool.org/databases_101.html#specialized-create-user-commands "Link to this heading")

Some relational databases provide additional ways of creating users like specialized command line programs.

#### Postgresql[](https://www.opsschool.org/databases_101.html#id3 "Link to this heading")

createuser username