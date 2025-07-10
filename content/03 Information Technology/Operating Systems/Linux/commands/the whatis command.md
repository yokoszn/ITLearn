The `whatis` command (or `man -f`) returns what section a man page is stored in. This command occasionally returns unusual output, such as the following:

**sysadmin@localhost:~$** whatis ls                                              
ls (1)               - list directory contents 
ls (lp)              - list directory contents

**

Note

**

The example above is designed to demonstrate a scenario where two commands list directory contents. The output in the example terminal above may not match the output in the VM.

Based on this output, there are two `ls` commands that list directory contents. The simple reason for this is that UNIX had two main variants, which resulted in some commands being developed "in parallel" and therefore behaving differently on different variants of UNIX. Many modern distributions of Linux include commands from both UNIX variants.

This does, however, pose a bit of a problem: when the `ls` command is typed, which command is executed?

---

## Find Any File or Directory
The `whereis` command is specifically designed to find commands and man pages. While this is useful, it is often necessary to find a file or directory, not just files that are commands or man pages.

To find any file or directory, use [[the locate command]]. 