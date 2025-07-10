---
title: the locate command
---

To find any file or directory, use the `locate` command. This command searches a database of all files and directories that were on the system when the database was created. Typically, the command to generate this database is run nightly.

---

Any files created today will not be searchable with the `locate` command. If root access is available, it’s possible to update the `locate` database manually by running the `updatedb` command. Regular users cannot update the database file.

Also note that when using the `locate` command as a regular user, the output may be limited due to file permissions. If the user that is logged in doesn’t have access to a file or directory on the filesystem due to permissions, the `locate` command won't return those names. This security feature is designed to keep users from "exploring" the filesystem by using the `locate` database. The `root` user can search for any file in the `locate` database.

The output of the locate command can be quite large. When searching for a filename, such as `passwd`, the `locate` command produces every file that contains the string `passwd`, not just files named passwd.

In many cases, it is helpful to start by finding out how many files match. Do this by using the `-c` option to the `locate` command