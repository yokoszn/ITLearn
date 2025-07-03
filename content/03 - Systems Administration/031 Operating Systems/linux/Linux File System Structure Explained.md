---
{}
---
#Learning #online-courses  #practice-exercises #certification-prep 
#linux 
___
**Tags:** [[TryHackMe]]
[[linux]]
**Links:** [Linux File System/Structure Explained! - YouTube](https://www.youtube.com/watch?v=HbgzrKJvDRw)
(https://www.youtube.com/watch?v=42iQKuQodW4&list=PLAoA-usw1t-4sIlwNXKS2RIn0ZBx4VQhn&index=11)

---


We covered some of the most fundamental commands when interacting with the filesystem on the Linux machine. For example, we covered how to list and find the contents of folders using `ls` and `find` and navigating the filesystem using `cd`. 

In this task, we're going to learn some more commands for interacting with the filesystem to allow us to:

- create files and folders
- move files and folders
- delete files and folders

More specifically, the following commands:

|   |   |   |
|---|---|---|
|Command|Full Name|Purpose|
|touch|touch|Create file|
|mkdir|make directory|Create a folder|
|cp|copy|Copy a file or folder|
|mv|move|Move a file or folder|
|rm|remove|Remove a file or folder|
|file|file|Determine the type of a file|

_Protip: Similarly to using cat, we can provide full file paths, i.e. directory1/directory2/note for all of these commands_

  

**Creating Files and Folders (touch, mkdir)**

Creating files and folders on Linux is a simple process. First, we'll cover creating a file. The touch command takes exactly one argument -- the name we want to give the file we create. For example, we can create the file "note" by using `touch note`. It's worth noting that touch simply creates a blank file. You would need to use commands like echo or text editors such as nano to add content to the blank file.

Using touch to create a new file

```shell-session
tryhackme@linux2:~$ touch note
tryhackme@linux2:~$ ls           
folder1 note
```

This is a similar process for making a folder, which just involves using the `mkdir` command and again providing the name that we want to assign to the directory. For example, creating the directory "mydirectory" using `mkdir mydirectory`.

Creating a new directory with mkdir

```shell-session
tryhackme@linux2:~$ mkdir mydirectory
tryhackme@linux2:~$ ls           
folder1 mydirectory note
```

  

**Removing Files and Folders (rm)**

`rm` is extraordinary out of the commands that we've covered so far. You can simply remove files by using `rm`. However, you need to provide the `-R` switch alongside the name of the directory you wish to remove.

Using rm to remove a file

```shell-session
tryhackme@linux2:~$ rm note
tryhackme@linux2:~$ ls           
folder1 mydirectory
```

Using rm recursively to remove a directory

```shell-session
tryhackme@linux2:~$ rm -R mydirectory
tryhackme@linux2:~$ ls           
folder1
```

  

**Copying and Moving Files and Folders (cp, mv)**

Copying and moving files is an important functionality on a Linux machine. Starting with `cp`, this command takes two arguments:

1. the name of the existing file

2. the name we wish to assign to the new file when copying

`cp` copies the entire contents of the existing file into the new file. In the screenshot below, we are copying "note" to "note2".

Using cp to copy a file

```shell-session
tryhackme@linux2:~$ cp note note2
tryhackme@linux2:~$ ls           
folder1 note note2
```

Moving a file takes two arguments, just like the cp command. However, rather than copying and/or creating a new file, `mv` will merge or modify the second file that we provide as an argument. Not only can you use `mv` to move a file to a new folder, but you can also use `mv` to rename a file or folder. For example, in the screenshot below, we are renaming the file "note2" to be named "note3". "note3" will now have the contents of "note2". 

Using mv to move a file

```shell-session
tryhackme@linux2:~$ mv note2 note3
tryhackme@linux2:~$ ls           
folder1 note note3
```

  

**Determining File Type**

What is often misleading and often catches people out is making presumptions from files as to what their purpose or contents may be. Files usually have what's known as an extension to make this easier. For example, text files usually have an extension of ".txt". But this is not necessary.

So far, the files we have used in our examples haven't had an extension. Without knowing the context of why the file is there -- we don't really know its purpose. Enter the `file` command. This command takes one argument. For example, we'll use `file` to confirm whether or not the "note" file in our examples is indeed a text file, like so `file note`.

Using file to determine the contents of a file

```shell-session
tryhackme@linux2:~$ file note
note: ASCII text
```


---

**/etc**

This root directory is one of the most important root directories on your system. The etc folder (short for etcetera) is a commonplace location to store system files that are used by your operating system. 

For example, the sudoers file highlighted in the screenshot below contains a list of the users & groups that have permission to run sudo or a set of commands as the root user.

Also highlighted below are the "**passwd**" and "**shadow**" files. These two files are special for Linux as they show how your system stores the passwords for each user in encrypted formatting called sha512.

Some notable contents of the /etc directory

```shell-session
tryhackme@linux2:/etc$ ls
shadow passwd sudoers sudoers.d
```

  

**/var**

The "/var" directory, with "var" being short for variable data,  is one of the main root folders found on a Linux install. This folder stores data that is frequently accessed or written by services or applications running on the system. For example, log files from running services and applications are written here (**/var/log**), or other data that is not necessarily associated with a specific user (i.e., databases and the like).

Some notable contents of the /var directory

```shell-session
tryhackme@linux2:/var$ ls
backups log opt tmp
```

  

/**root**

Unlike the **/home** directory, the **/root** folder is actually the home for the "root" system user. There isn't anything more to this folder other than just understanding that this is the home directory for the "root" user. But, it is worth a mention as the logical presumption is that this user would have their data in a directory such as "**/home/root**" by default.  

Some notable contents of the /root directory

```shell-session
root@linux2:~# ls
myfile myfolder passwords.xlsx
```

**/tmp**

This is a unique root directory found on a Linux install. Short for "temporary", the /tmp directory is volatile and is used to store data that is only needed to be accessed once or twice. Similar to the memory on your computer, once the computer is restarted, the contents of this folder are cleared out.

What's useful for us in pentesting is that any user can write to this folder by default. Meaning once we have access to a machine, it serves as a good place to store things like our enumeration scripts.

Some notable contents of the /tmp directory

```shell-session
root@linux2:/tmp# ls
todelete trash.txt rubbish.bin
```


---


**Downloading Files (Wget)**

A pretty fundamental feature of computing is the ability to transfer files. For example, you may want to download a program, a script, or even a picture. Thankfully for us, there are multiple ways in which we can retrieve these files.

 We're going to cover the use of `wget` .  This command allows us to download files from the web via HTTP -- as if you were accessing the file in your browser. We simply need to provide the address of the resource that we wish to download. For example, if I wanted to download a file named "myfile.txt" onto my machine, assuming I knew the web address it -- it would look something like this:

`wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt`

  

**Transferring Files From Your Host - SCP (SSH)**

Secure copy, or SCP, is just that -- a means of securely copying files. Unlike the regular cp command, this command allows you to transfer files between two computers using the SSH protocol to provide both authentication and encryption.

Working on a model of SOURCE and DESTINATION, SCP allows you to:

- Copy files & directories from your current system to a remote system
- Copy files & directories from a remote system to your current system

Provided that we know usernames and passwords for a user on your current system and a user on the remote system. For example, let's copy an example file from our machine to a remote machine, which I have neatly laid out in the table below:

|   |   |
|---|---|
|**Variable**|**Value**|
|The IP address of the remote system|192.168.1.30|
|User on the remote system|ubuntu|
|Name of the file on the local system|important.txt|
|Name that we wish to store the file as on the remote system|transferred.txt|

With this information, let's craft our `scp` command (remembering that the format of SCP is just SOURCE and DESTINATION)

`scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt`

And now let's reverse this and layout the syntax for using `scp` to copy a file from a remote computer that we're not logged into 

|   |   |
|---|---|
|**Variable**|**Value**|
|IP address of the remote system|192.168.1.30|
|User on the remote system|ubuntu|
|Name of the file on the remote system|documents.txt|
|Name that we wish to store the file as on our system|notes.txt|

The command will now look like the following: `scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt` 

**  
Serving Files From Your Host - WEB**

Ubuntu machines come pre-packaged with python3. Python helpfully provides a lightweight and easy-to-use module called "HTTPServer". This module turns your computer into a quick and easy web server that you can use to serve your own files, where they can then be downloaded by another computing using commands such as `curl` and `wget`. 

Python3's "HTTPServer" will serve the files in the directory where you run the command, but this can be changed by providing options that can be found within the manual pages. Simply, all we need to do is run `python3 -m  http.server` in the terminal to start the module! In the snippet below, we are serving from a directory called "webserver", which has a single named "file".

Using Python to start a web server

```shell-session
tryhackme@linux3:/webserver# python3 -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

Now, let's use `wget` to download the file using the 10.10.158.78 address and the name of the file. Remember, because the python3 server is running port 8000, you will need to specify this within your wget command. For example:

An example wget command of a web server running on port 8000

```shell-session
tryhackme@mymachine:~# wget http://10.10.158.78:8000/myfile
```

Note, you will need to open a new terminal to use `wget` and leave the one that you have started the Python3 web server in. This is because, once you start the Python3 web server, it will run in that terminal until you cancel it.

Let's take a look in the snippet below as an example:

Downloading a file from our webserver using wget

```shell-session
tryhackme@linux3:/tmp# wget http://10.10.158.78:8000/file

2021-05-04 14:26:16  http://127.0.0.1:8000/file
Connecting to http://127.0.0.1:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 51095 (50K) [text]
Saving to: ‘file’

file                    100%[=================================================>]  49.90K  --.-KB/s    in 0.04s

2021-05-04 14:26:16 (1.31 MB/s) - ‘file’ saved [51095/51095]
```

**Remember**, you will need to run the wget command in another terminal (while keeping the terminal that is running the Python3 server active). An example of this on the TryHackMe AttackBox is below:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5c549500924ec576f953d9fc/room-content/14de6e0470d50317f3b24f4f9aa9297a.png)  

One flaw with this module is that you have no way of indexing, so you must know the exact name and location of the file that you wish to use. This is why I prefer to use Updog. [What's Updog](https://github.com/sc0tfree/updog)? A more advanced yet lightweight webserver. But for now, let's stick to using Python's "HTTP Server".

