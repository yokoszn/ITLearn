---
title: the man command
---
**Consider This**

The `man` command uses a pager to display documents. Usually, this pager is the `less` command, but on some distributions, it may be the `more` command. Both are very similar in how they perform.

To view the various movement commands that are available, use the **H** key while viewing a man page. This displays a help page.


---

## Sections Within Man Pages

Man pages are broken into sections. Each section is designed to provide specific information about a command. While there are common sections seen in most man pages, some developers also create sections only available on specific man pages.

The following describes some of the more common sections found in man pages:

**NAME**

Provides the name of the command and a very brief description.

**NAME**                                                                            
       ls - list directory contents   

**SYNOPSIS**

Provides examples of how the command is executed.

**SYNOPSIS**                                                                        
       **ls** [OPTION]... [FILE]...   

The `SYNOPSIS` section of a man page can be difficult to understand but is very important because it provides a concise example of how to use the command. For example, consider the `SYNOPSIS` of the man page for the `cal` command:

**SYNOPSIS** 
     **cal** [**-31jy**] [**-A** number] [**-B** number] [**-d** yyyy-mm] 

The square brackets `[ ]` are used to indicate that this feature is not required to run the command. For example, `[-31jy]` means options `-3`, `-1`, `-j`, or `-y` are available, but not required for the `cal` command to function properly.

The last set of square brackets `[[month] year]` demonstrates another feature; it means a year can be specified by itself, but to specify a month the year must also be specified.

Another component of the `SYNOPSIS` that might cause some confusion can be seen in the man page of the `date` command:

**SYNOPSIS **                                                             
       **date** [OPTION]...                            
       **date** [-u|--utc|--universal] 

‌⁠​​⁠​ 

In this `SYNOPSIS` there are two syntaxes for the `date` command. The first one is used to display the date on the system while the second is used to set the date.

The ellipsis `...` following `[OPTION]` indicates that one or more of the items before it may be used.

Additionally, the `[-u|--utc|--universal]` notation means that either the `-u` option or the `--utc` option or the `--universal` option may be used. Typically this means that all three options really do the same thing, but sometimes the use of the `|` character is used to indicate that the options can't be used in combination, like a logical “or".

**DESCRIPTION**

Provides a more detailed description of the command.

**DESCRIPTION**  
       List  information  about  the FILEs (the current directory by default).  
       Sort entries alphabetically if none of -cftuvSUX nor --sort  is  speci-  
       fied.   

**OPTIONS**

Lists the options for the command as well as a description of how they are used. Often this information is found in the `DESCRIPTION` section and not in a separate `OPTIONS` section.

       **-a, --all   **                                                             
              do not ignore entries starting with .  
 
       **-A, --almost-all**                                                         
              do not list implied . and ..                                      
                                                                                
       **--author**                                                                 
              with -l, print the author of each file                            
                                                                                
       **-b, --escape**                                                             
              print C-style escapes for nongraphic characters                   
                                                                                
       **--block-size=SIZE**                                                        
              scale sizes by SIZE before printing them; e.g., '--block-size=M'  
              prints sizes in units of 1,048,576 bytes; see SIZE format below   

**FILES**

Lists the files that are associated with the command as well as a description of how they are used. These files may be used to configure the command's more advanced features. Often this information is found in the `DESCRIPTION` section and not in a separate `FILES` section.

**AUTHOR**

Provides the name of the person who created the man page and (sometimes) how to contact the person.

**AUTHOR **                                                                         
       Written by Richard M. Stallman and David MacKenzie.

**REPORTING BUGS**

Provides details on how to report problems with the command.

**REPORTING BUGS**                                                                  
       GNU coreutils online help: <http://www.gnu.org/software/coreutils/>      
       Report ls translation bugs to <http://translationproject.org/team/>

**COPYRIGHT**

Provides basic copyright information.

**COPYRIGHT**                                                                       
       Copyright (C) 2017 Free Software Foundation, Inc.  License GPLv3+:  GNU  
       GPL version 3 or later <http://gnu.org/licenses/gpl.html>.               
       This  is  free  software:  you  are free to change and redistribute it.  
       There is NO WARRANTY, to the extent permitted by law.   

**SEE ALSO**

Provides you with an idea of where you can find additional information. This often includes other commands that are related to this command.

**SEE ALSO**                                                                        
       Full documentation at: <http://www.gnu.org/software/coreutils/ls>        
       or available locally via: info '(coreutils) ls invocation'  

-  [Previous](https://content.netdevgroup.com/contents/linux-essentials/gFA3XmsJog/6.2.1)
- [Next](https://content.netdevgroup.com/contents/linux-essentials/gFA3XmsJog/6.2.3)

---


Until now, we have been displaying man pages for commands. However, there are several different types of commands (user commands, system commands, and administration commands), configuration files and other features, such as libraries and kernel components, that require documentation.

As a result, there are thousands of man pages on a typical Linux distribution. To organize all of these man pages, they are categorized by sections.

By default, there are nine sections of man pages:

1. General Commands
2. System Calls
3. Library Calls
4. Special Files
5. File Formats and Conventions
6. Games
7. Miscellaneous
8. System Administration Commands
9. Kernel Routines

## Info Documentation

Man pages are excellent sources of information, but they do tend to have a few disadvantages. One example is that each man page is a separate document, not related to any other man page. While some man pages have a `SEE ALSO` section that may refer to other man pages, they tend to be independent sources of documentation.

The `info` command also provides documentation on operating system commands and features. The goal is slightly different from man pages: to provide a documentation resource that gives a logical organizational structure, making reading documentation easier.

All of the documentation is merged into a single "book" representing all of the documentation available. Within info documents, information is broken down into categories that work much like a table of contents in a book. Hyperlinks are provided to pages with information on individual topics for a specific command or feature.

Another advantage of info over man pages is that the writing style of info documents is typically more conducive to learning a topic. Consider man pages to be more of a reference resource and info documents to be more of a learning guide.