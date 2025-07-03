___
**Tags:** 

**Links:** 

---
## Control Statements

Typically, you type a single command and you execute it when you press **Enter**. The Bash shell offers three different statements that can be used to separate multiple commands typed together.

The simplest separator is the semicolon (`;`). Using the semicolon between multiple commands allows for them to be executed one right after another, sequentially from left to right.

The `&&` characters create a logical "and" statement. Commands separated by && are conditionally executed. If the command on the left of the `&&` is successful, then the command to the right of the `&&` will also be executed. If the command to the left of the `&&` fails, then the command to the right of the `&&` is not executed.

The `||` characters create a logical "or" statement, which also causes conditional execution. When commands are separated by `||`, then only if the command to the left fails, does the command to the right of the `||` execute. If the command to the left of the `||` succeeds, then the command to the right of the `||` will not execute.

To see how these control statements work, you will be using two special executables: `true` and `false`. The `true` executable always succeeds when it executes, whereas, the `false` executable always fails. While this may not provide you with realistic examples of how `&&` and `||` work, it does provide a means to demonstrate how they work without having to introduce new commands.

---

Control statements allow you to use multiple commands at once or run additional commands, depending on the success of a previous command. Typically these control statements are used within scripts, but they can also be used on the command line as well
## Semicolon

command1; command2; command3

The semicolon `;` character can be used to run multiple commands, one after the other. Each command runs independently and consecutively; regardless of the result of the first command, the second command runs once the first has completed, then the third and so on.

For example, to print the months of January, February and March of 2030, execute the following command:

```
**sysadmin@localhost:~$** cal 1 2030; cal 2 2030; cal 3 2030               
    January 2030                                                       
Su Mo Tu We Th Fr Sa                                                            
       1  2  3  4  5                                                            
 6  7  8  9 10 11 12                                                            
13 14 15 16 17 18 19                                                            
20 21 22 23 24 25 26                                                            
27 28 29 30 31                                                                  
                                                                                
   February 2030                                                                
Su Mo Tu We Th Fr Sa                                                            
                1  2                                                            
 3  4  5  6  7  8  9                                                            
10 11 12 13 14 15 16                                                            
17 18 19 20 21 22 23                                                            
24 25 26 27 28                                                                  
                                                                                
     March 2030                                                                 
Su Mo Tu We Th Fr Sa                                                            
                1  2                                                            
 3  4  5  6  7  8  9                                                            
10 11 12 13 14 15 16                                                            
17 18 19 20 21 22 23                                                            
24 25 26 27 28 29 30                                                            
31
```

---

## Double Ampersand

command1 && command2

The double ampersand `&&` acts as a logical "and"; if the first command is successful, then the second command will also run. If the first command fails, then the second command will not run.

To better understand how this works, consider first the concept of failure and success for commands. Commands succeed when they work properly and fail when something goes wrong. For example, consider the `ls` command. The command succeeds if the given directory is accessible and fails if it isn't.

In the following example, the first command succeeds because the `/etc/ppp` directory exists and is accessible while the second command fails because there is no `/junk` directory: ```
```

sysadmin@localhost:~$ ls /etc/ppp                  
ip-down.d  ip-up.d           
sysadmin@localhost:~$ ls /etc/junk                             
ls: cannot access /etc/junk: No such file or directory

```

To use the success or failure of the `ls` command in conjunction with `&&` execute commands like the following. In the first example, the `echo` command is executed because the `ls` command succeeds:
![[Pasted image 20240917105916.png]]

---

## Double Pipe

command1 || command2

The double pipe `||` is a logical "or". Depending on the result of the first command, the second command will either run or be skipped.

With the double pipe, if the first command runs successfully, the second command is skipped; if the first command fails, then the second command is run. In other words, you are essentially telling the shell, "Either run this first command or the second one”.

In the following example, the `echo` command only executes if the `ls` command fails:

```
**sysadmin@localhost:~$** ls /etc/ppp || echo failed                 
ip-down.d  ip-up.d              
**sysadmin@localhost:~$** ls /etc/junk || echo failed                  
ls: cannot access /etc/junk: No such file or directory             
failed
```

---
# Functions 

Functions can also be built using existing commands to either create new commands, or to override commands built-in to the shell or commands stored in files. Aliases and functions are normally loaded from the initialization files when the shell first starts.

Functions are more advanced than aliases and typically are used in Bash shell scripts. Typically, functions are used to execute multiple commands. To create a function, the following syntax is used:

function_name () 
{
   commands
}

In the format above, `function_name` can be anything that the administrator wants to call the function. The commands that the administrator wants to execute can replace the `commands` placeholder. Note the formatting, in particular, the location of the parenthesis `()` and braces `{}`, as well as the convention of using tabs to make the function more easily readable.

Functions are useful as they allow for a set of commands to be executed one at a time instead of typing each command repeatedly. In the example below, a function called `my_report` is created to execute the `ls`, `date`, and `echo` commands.

```
**sysadmin@localhost:~$** my_report () {                                            
> ls Documents                                                                  
> date                                                                          
> echo "Document directory report"                                              
> }
>
```
When creating a function, a `>` character will appear as a prompt to enter the commands for the function. The curly braces `{}` are used to let the shell know when a function begins and ends so as to exit the `>` prompt.

Once a function is created, the function name may be invoked from the BASH prompt to execute the function:
```
**sysadmin@localhost:~$** my_report                                                 
School            alpha-third.txt  hidden.txt    numbers.txt  spelling.txt      
Work              alpha.txt        letters.txt   os.csv       words             
adjectives.txt    animals.txt      linux.txt     people.csv                     
alpha-first.txt   food.txt         longfile.txt  profile.txt                    
alpha-second.txt  hello.sh         newhome.txt   red.txt                        
Wed Oct 13 06:54:04 UTC 2021                                                    
Document directory report                                                       
**sysadmin@localhost:~$**
```

---
# Arguments

An argument can be used to specify something for the command to act upon. If the `ls` command is given the name of a directory as an argument, it lists the contents of that directory. In the following example, the `/etc/ppp` directory is used as an argument; the resulting output is a list of files contained in that directory:

**THIS IS DIFFERENT, to Options**

---
# Options


```
command [options] -[arguments]
```
Options can be used with commands to expand or modify the way a command behaves. For example, using the `-l` option of the `ls` command results in a long listing, providing additional information about the files that are listed, such as the permissions, the size of the file and other information:

Often the character is chosen to be mnemonic for its purpose, like choosing the letter l for long or r for reverse. By default, the `ls` command prints the results in alphabetical order, and so by adding the `-r` option, it prints the results in reverse alphabetical order.

In most cases, options can be used in conjunction with other options. They can be given as separate options, as in `-l -r`, or combined, as in `-lr`. The combination of these two options would result in a long listing output in reverse alphabetical order:

Options are often single letters; however, sometimes they are words or phrases as well. Typically, older commands use single letters while newer commands use complete words for options. Single-letter options are preceded by a single dash `-` character, like the `-h` option. Full-word options are preceded by two dash `--` characters. The `-h` option also has an equivalent full-word form; the `--human-readable` option.

---

# Internal / External Commands 

Also called built-in commands, internal commands are built into the shell itself. A good example is the `cd` (change directory) command as it is part of the Bash shell. When a user types the `cd` command, the Bash shell is already executing and knows how to interpret it, requiring no additional programs to be started.

The `type` command identifies the `cd` command as an internal command:

```
sysadmin@localhost:~$ type cd                                     
cd is a shell builtin
```

---

## External Commands

External commands are binary executables stored in directories that are searched by the shell. If a user types the `ls` command, then the shell searches through the directories that are listed in the `PATH` variable to try to find a file named `ls` that it can execute.

If a command does not behave as expected or if a command is not accessible that should be, it can be beneficial to know where the shell is finding the command or which version it is using. It would be tedious to have to manually look in each directory that is listed in the `PATH` variable. Instead, use the `which` command to display the full path to the command in question: `which command`

---
The `which` command searches for the location of a command by searching the `PATH` variable.
```
sysadmin@localhost:~$ which ls                                       
/bin/ls                                                               
sysadmin@localhost:~$ which cal                                        
/usr/bin/cal
```
External commands can also be executed by typing the complete path to the command. For example, to execute the `ls` command:

For external commands, the `type` command displays the location of the command:
```
**sysadmin@localhost:~$** type cal                                      
cal is /usr/bin/cal
```
In some cases the output of the `type` command may differ significantly from the output of the `which` command:
```
**sysadmin@localhost:~$** type echo                                     
echo is a shell builtin
**sysadmin@localhost:~$** which echo                                        
/bin/echo
```
Using the `-a` option of the `type` command displays all locations that contain the command named: 
```
**sysadmin@localhost:~$** type -a echo                                      
echo is a shell builtin                                                
echo is /bin/echo
```

---
# Command Aliases

An alias can be used to map longer commands to shorter key sequences. When the shell sees an alias being executed, it substitutes the longer sequence before proceeding to interpret commands.

For example, the command `ls -l` is commonly aliased to `l` or `ll`. Because these smaller commands are easier to type, it becomes faster to run the `ls -l` command line.

To determine what aliases are set on the current shell use the `alias` command:
```
**sysadmin@localhost:~$** alias                                             
alias egrep='egrep --color=auto'                                       
alias fgrep='fgrep --color=auto'                                        
alias grep='grep --color=auto'                                          
alias l='ls -CF'                                                       
alias la='ls -A'                                                       
alias ll='ls -alF'                                                     
alias ls='ls --color=auto'
```

The aliases from the previous examples were created by initialization files. These files are designed to make the process of creating aliases automatic.

New aliases can be created using the following format, where `name` is the name to be given the alias and `command` is the command to be executed when the alias is run.

alias name=command

For example, the `cal 2019` command displays the calendar for the year 2019. Suppose you end up running this command often. Instead of executing the full command each time, you can create an alias called `mycal` and run the alias, as demonstrated in the following graphic:
```
**sysadmin@localhost:~$** alias mycal="cal 2019"                                    
**sysadmin@localhost:~$** mycal                                                     
                            2019                                                
      January               February               March                        
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa                
       1  2  3  4  5                  1  2                  1  2                
 6  7  8  9 10 11 12   3  4  5  6  7  8  9   3  4  5  6  7  8  9                
13 14 15 16 17 18 19  10 11 12 13 14 15 16  10 11 12 13 14 15 16                
20 21 22 23 24 25 26  17 18 19 20 21 22 23  17 18 19 20 21 22 23                
27 28 29 30 31        24 25 26 27 28        24 25 26 27 28 29 30                
                                            31
```

Aliases created this way only persist while the shell is open. Once the shell is closed, the new aliases are lost. Additionally, each shell has its own aliases, so aliases created in one shell won’t be available in a new shell that’s opened.

The `type` command can identify aliases to other commands:\

```
**sysadmin@localhost:~$** type ll                                          
ll is aliased to `ls -alF'                                              
**sysadmin@localhost:~$** type -a ls                                          
ls is aliased to `ls --color=auto'
ls is /bin/ls
```

The output of these commands indicates that `ll` is an alias for `ls -alF`, and even `ls` is an alias for `ls --color=auto`.

---
# Command-Line

When a command is executed in the terminal, it is stored in a history list. This is designed to make it easy to execute the same command, later eliminating the need to retype the entire command.

Pressing the **Up Arrow ↑** key displays the previous command on the prompt line. The entire history of commands run in the current session can be displayed by pressing **Up** repeatedly to move back through the history of commands that have been run. Pressing the Enter key runs the displayed command again.

When the desired command is located, the **Left Arrow ←** and **Right Arrow →** keys can position the cursor for editing. Other useful keys for editing include the **Home**, **End**, **Backspace** and **Delete** keys.

To view the history list of a terminal, use the `history` command:

```
**sysadmin@localhost:~$** date                                       
Wed Dec 12 04:28:12 UTC 2018                                   
**sysadmin@localhost:~$** ls                                           
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos       
**sysadmin@localhost:~$** cal 5 2030                                  
     May 2030                                                                  
Su Mo Tu We Th Fr Sa                                                            
          1  2  3  4                                                            
 5  6  7  8  9 10 11                                                            
12 13 14 15 16 17 18                                                            
19 20 21 22 23 24 25                                                            
26 27 28 29 30 31                                                               
**sysadmin@localhost:~$** history                                   
    1  date                                                       
    2  ls                                                      
    3  cal 5 2030                                             
    4  history
```

![[Pasted image 20240917103341.png]]

> [!NOTE]
> One way to learn more about a command is to look at where it comes from. The `type` command can be used to determine information about command type.
> 
> type `command`
> 
> There are several different sources of commands within the shell of your CLI including internal commands, external commands, aliases, and functions.

---

# Variables

A variable is a feature that allows the user or the shell to store data. This data can be used to provide critical system information or to change the behavior of how the Bash shell (or other commands) work. Variables are given names and stored temporarily in memory. There are two types of variables used in the Bash shell: local and environment.

---
# Local Variables

Local or shell variables exist only in the current shell, and cannot affect other commands or applications. When the user closes a terminal window or shell, all of the variables are lost. They are often associated with user-based tasks and are lowercase by convention.

To set the value of a variable, use the following assignment expression. If the variable already exists, the value of the variable is modified. If the variable name does not already exist, the shell creates a new local variable and sets the value:
`variable=value`
The following example creates a local variable named `variable1` and assigns it a value of `Something`
```
sysadmin@localhost:~$ variable1='Something'
```

The `echo` command is used to display output in the terminal. To display the value of the variable, use a dollar sign `$` character followed by the variable name as an argument to the `echo` command:

**sysadmin@localhost:~$** echo $variable1                    
Something

---

# PATH Variable

One of the most important Bash shell variables to understand is the `PATH` variable. It contains a list that defines which directories the shell looks in to find commands. If a valid command is entered and the shell returns a "command not found" error, it is because the Bash shell was unable to locate a command by that name in any of the directories included in the path. The following command displays the path of the current shell:
```
sysadmin@localhost:~$ echo $PATH                                        
/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
sysadmin@localhost:~$
```
Each directory in the list is separated by a colon `:` character. Based on the preceding output, the path contains the following directories. The shell will check the directories in the order they are listed:
```
/home/sysadmin/bin
/usr/local/sbin
/usr/local/bin
/usr/sbin
/usr/bin
/sbin
/bin
/usr/games
```


> [!NOTE] 
>Each of these directories is represented by a path. A path is a list of directories separated by the / character. If you think of the filesystem as a map, paths are the directory addresses, which include step-by-step navigation directions; they can be used to indicate the location of any file within the filesystem. For example, `/home/sysadmin` is a path to the home directory:
>![[Pasted image 20240917104126.png]]

If the command is not found in any directory listed in the `PATH` variable, then the shell returns an error:
```
**sysadmin@localhost:~$** zed                                              
-bash: zed: command not found                                           
**sysadmin@localhost:~$**
```
‌⁠​​⁠​ If custom software is installed on the system it may be necessary to modify the `PATH` to make it easier to execute these commands. For example, the following will add and verify the `/usr/bin/custom` directory to the `PATH` variable:
```
sysadmin@localhost:~$ PATH=/usr/bin/custom:$PATH                        
sysadmin@localhost:~$ echo $PATH                                       
/usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
```

> [!BE AWARE]
> 
> When updating the `PATH` variable, always include the current path, so as not to lose access to commands located in those directories. This can be accomplished by appending `$PATH` to the value in the assignment expression. Recall that a variable name preceded by a dollar sign represents the value of the variable.


---

# Environment Variable

Environment variables, also called global variables, are available system-wide, in all shells used by Bash when interpreting commands and performing tasks. The system automatically recreates environment variables when a new shell is opened. Examples include the `PATH`, `HOME`, and `HISTSIZE` variables. The `HISTSIZE` variable defines how many previous commands to store in the history list. The command in the example below displays the value of the `HISTSIZE` variable:
![[Pasted image 20240917103811.png]]When run without arguments, the `env` command outputs a list of the environment variables. Because the output of the `env` command can be quite long, the following examples use a text search to filter that output.

In a previous example `variable1` was created as a local variable, so the following search in the environment variables results in no output:![[Pasted image 20240917103835.png]]
The `export` command can also be used to make a variable an environment variable upon its creation by using the assignment expression as the argument:![[Pasted image 20240917103856.png]]

---
[[Command Line Arguments for Beginners - Full Course]]
[[Linux Commands for Beginners - Full Course]]

[[Infrastructure as Code]]
[[YAML]]
[[Docker]]
[[Terraform]]

[[Powershell]]

![[Bash]]