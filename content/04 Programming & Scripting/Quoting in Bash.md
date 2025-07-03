- #programming
- #bash
- #powershell
- #algorithms
- #object-oriented-programming
- #functional-programming
- #services
- #system-monitoring
- #logging 
- #Learning #certification-prep #hands-on 

Quotation marks are used throughout Linux administration and most computer programming languages to let the system know that the information contained within the quotation marks should either be ignored or treated in a way that is very different than it would normally be treated. There are three types of quotes that have special significance to the Bash shell: double quotes `"`, single quotes `'`, and back quotes `` ` ``. Each set of quotes alerts the shell not to treat the text within the quotes in the normal way.

----

## Quoting

There are three types of quotes used by the Bash shell: single quotes (`'`), double quotes (`"`) and back quotes (`` ` ``). These quotes have special features in the Bash shell as described below.

To understand single and double quotes, consider that there are times that you don't want the shell to treat some characters as special. For example, the `*` character is used as a wildcard. What if you wanted the `*` character to just mean a literal asterisk?

- Single `'` quotes prevent the shell from "interpreting" or expanding all special characters. Often single quotes are used to protect a string (a sequence of characters) from being changed by the shell, so that the string can be interpreted by a command as a parameter to affect the way the command is executed.
    
- Double `"` quotes stop the expansion of glob characters like the asterisk (`*`), question mark (`?`), and square brackets ( `[]` ). Double quotes do allow for both variable expansion and command substitution (see back quotes) to take place.
    
- Back `` ` `` quotes cause command substitution which allows for a command to be executed within the line of another command.
    

When using quotes, they must be entered in pairs or else the shell will not consider the command complete.

While single quotes are useful for blocking the shell from interpreting one or more characters, the shell also provides a way to block the interpretation of just a single character called "escaping" the character. To escape the special meaning of a shell metacharacter, the backslash `\` character is used as a prefix to that one character.

---

## Double Quotes

Double quotes stop the shell from interpreting some metacharacters (special characters), including glob characters.

> [!NOTE]
> Glob characters, also called wild cards, are symbols that have special meaning to the shell; they are interpreted by the shell itself before it attempts to run any command. Glob characters include the asterisk `*` character, the question `?` mark character, and the brackets `[ ]`, among others.

Globbing will be covered in greater detail later in the course.

Within double quotes an asterisk is just an asterisk, a question mark is just a question mark, and so on, which is useful when you want to display something on the screen that is normally a special character to the shell. In the `echo` command below, the Bash shell doesn't convert the glob pattern into filenames that match the pattern:
```
**sysadmin@localhost:~$** echo "The glob characters are *, ? and [ ]"      
The glob characters are *, ? and [ ]
```

Double quotes still allow for command substitution, variable substitution, and permit some other shell metacharacters that haven't been discussed yet. The following demonstration shows that the value of the `PATH` variable is still displayed:
```
**sysadmin@localhost:~$** echo "The path is $PATH"                          
The path is /usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
```

---

## Single Quotes

Single quotes prevent the shell from doing any interpreting of special characters, including globs, variables, command substitution and other metacharacters that have not been discussed yet.

For example, to make the `$` character simply mean a `$`, rather than it acting as an indicator to the shell to look for the value of a variable, execute the second command displayed below:

```
**sysadmin@localhost:~$** echo The car costs $100                           
The car costs 00                                                        
**sysadmin@localhost:~$** echo 'The car costs $100'                        
The car costs $100
```

---

## Backslash Character

There is also an alternative technique to essentially single quote a single character. Consider the following message:

The service costs $1 and the path is $PATH 

If this sentence is placed in double quotes, `$1` and `$PATH` are considered variables.
```
**sysadmin@localhost:~$** echo "The service costs $1 and the path is $PATH"

‌⁠​​⁠​The service costs  and the path is /usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
```
f it is placed in single quotes, `$1` and `$PATH` are not considered variables.

**sysadmin@localhost:~$** echo 'The service costs $1 and the path is $PATH' 
The service costs $1 and the path is $PATH 

But what if you want to have `$PATH` treated as a variable and `$1` not?

In this case, use a backslash `\` character in front of the dollar sign `$` character to prevent the shell from interpreting it. The command below demonstrates using the `\` character:
`**sysadmin@localhost:~$** echo The service costs \$1 and the path is $PATH`

---


## Backquotes

Backquotes, or backticks, are used to specify a command within a command, a process called command substitution. This allows for powerful and sophisticated use of commands.

While it may sound confusing, an example should make things more clear. To begin, note the output of the `date` command:
![[Pasted image 20240917105655.png]]