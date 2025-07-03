#linux #course  #Learning #learning-path 

[[NDG Linux Essentials]]
[[Linux Unhatched NDG - Course]]
[[Personal Learning]]
[[linux]]
[[Certifications]]

---



Welcome to the NDG Linux Essentials course. NDG (Network Development Group) is very excited that you have decided to immerse yourself in the world of Linux. Before you get started, we want to take the opportunity to introduce you to the course, give you an idea of what you can expect from the material and your interaction with the features we have designed for you.

The NDG Linux Essentials course is designed to prepare you for the Linux Professional Institute Linux Essentials Professional Development Certificate, which validates a demonstrated understanding of:

- FOSS, the various communities, and licenses
- Knowledge of open source applications in the workplace as they relate to closed source equivalents
- Basic concepts of hardware, processes, programs and the components of the Linux Operating System
- How to work on the command line and with files
- How to create and restore compressed backups and archives
- System security, users/groups and file permissions for public and private directories
- How to create and run simple scripts

To obtain the Linux Essentials Professional Development Certificate you must pass Linux Essentials (LPI-010) which covers:

- The Linux community and a career in open source
- Finding your way on a Linux system
- The power of the command line
- The Linux operating system
- Security and file permissions

The Linux Essentials Professional Development Certificate is the beginning of your path to becoming a Linux certified professional. Information about the Linux Professional Institute certifications can be found by going to [www.lpi.org](http://www.lpi.org/).

Do not be concerned if you have little or no Linux experience. This course is the perfect starting place designed to teach all of the concepts from square one. However, if you do not find this material challenging enough, consider starting with NDG Introduction to Linux I, a more rigorous introductory course.


----


## Getting Certified with LPI

### Who is LPI?

The [Linux Professional Institute (LPI)](http://www.lpi.org/) is the leading Linux certification and workforce development organization that is committed to helping students and professionals grow their career opportunities in Linux and Open Source. With over 15 years of experience, LPI offers one of the most comprehensive, globally recognized Linux skills certification programs.

### Why is validating your skills important?

When looking for your next internship, job, or promotion it’s important to have the right Linux skills and knowledge for the position. The Linux Essentials Professional Development Certificate is a trusted credential that can be a great first step toward LPI’s professional LPIC certification track or it can be a great way to show decision-makers that you have the skills and abilities to do the job whether that’s in big data, cloud, network, mobile or open source technologies that rely on Linux.
![[Pasted image 20240916123936.png]]


---


## 2.4.1 Linux Distributions

### Red Hat

**Red Hat** started as a simple distribution that introduced the Red Hat Package Manager (RPM). The developer eventually formed a company around it, which tried to commercialize a Linux desktop for business. Over time, Red Hat started to focus more on the server applications, such as web- and file-serving and released **Red Hat Enterprise Linux (RHEL)**, which was a paid service on a long release cycle. The release cycle dictates how often software is upgraded. A business may value stability and want long release cycles, while a hobbyist or a startup may want the latest software and opt for a shorter release cycle. To satisfy the latter group, Red Hat sponsors the **Fedora Project** which makes a personal desktop comprising the latest software but is still built on the same foundations as the enterprise version.

Because everything in Red Hat Enterprise Linux is open source, a project called **CentOS** came to be. It recompiled all the RHEL packages (converting their source code from the programming language they were written into language usable by the system) and gave them away for free. CentOS and others like it (such as Scientific Linux) are largely compatible with RHEL and integrate some newer software, but do not offer the paid support that Red Hat does.

**Scientific Linux** is an example of a specific-use distribution based on Red Hat. The project is a Fermilab-sponsored distribution designed to enable scientific computing. Among its many applications, Scientific Linux is used with particle accelerators including the Large Hadron Collider at CERN.

### SUSE

**SUSE**, originally derived from **Slackware**, was one of the first comprehensive Linux distributions, it has many similarities to Red Hat Enterprise Linux. The original company was purchased by Novell in 2003, which was then purchased by the Attachmate Group in 2011. The Attachmate group then merged with Micro Focus International in 2014, and in 2018 SUSE announced plans to go forward as an independent business. Through all of the mergers and acquisitions, SUSE has managed to continue and grow.

While SUSE Linux Enterprise contains proprietary code and is sold as a server product, **openSUSE** is a completely open, free version with multiple desktop packages similar to CentOS and Linux Mint.

### Debian

**Debian** is more of a community effort, and as such, also promotes the use of open source software and adherence to standards. Debian came up with its own package management system based on the `.deb` file format. While Red Hat leaves non-Intel and AMD platform support to derivative projects, Debian supports many of these platforms directly.

**Ubuntu** is the most popular Debian-derived distribution. It is the creation of **Canonical**, a company that was made to further the growth of Ubuntu and makes money by providing support. Ubuntu has several different variants for desktop, server and various specialized applications. They also offer an LTS version that is kept up-to-date for 3 years on desktops and 5 years on servers, which gives developers and the companies they work for confidence to build solutions based on a stable distribution.

**‌⁠⁠Linux Mint** was started as a fork of Ubuntu Linux, while still relying upon the Ubuntu repositories. There are various versions, all free of cost, but some include proprietary codecs, which cannot be distributed without license restrictions in certain countries.

### Android

Linux is a kernel, and many of the commands covered in this course are actually part of the GNU package. That is why some people insist on using the term **GNU/Linux** instead of Linux alone.

**Android**, sponsored by Google, is the world’s most popular Linux distribution. It is fundamentally different from its counterparts. Android uses the **Dalvik** virtual machine with Linux, providing a robust platform for mobile devices such as phones and tablets. However, lacking the traditional packages that are often distributed with Linux (such as GNU and Xorg), Android is generally incompatible with desktop Linux distributions.

This incompatibility means that a Red Hat or Ubuntu user cannot download software from the Google Play store. Likewise, a terminal emulator in Android lacks many of the commands of its Linux counterparts. It is possible, however, to use BusyBox with Android to enable most commands to work.

### Other

**Raspbian** is a specialized Linux distribution optimized to run on **Raspberry Pi** hardware. This combination has seen significant use in training for programmers and hardware designers at all levels. Its low cost and ease of use have made it a favorite of educators worldwide, and many add-on devices are available to extend its capabilities into the physical world. There is a multitude of labs and projects available that teach everything from environmental monitoring to circuit design, machine learning, and robotics.

**Linux From Scratch (LFS)** is more of a learning tool than a working distribution. This project consists of an online book, and source code, with “step-by-step instructions” for building a custom Linux distribution from the source code up. This “distribution” embodies the true spirit of Linux whereby users can modify any aspect of the operating system and learn how all the pieces work together. It’s also a good starting point for anyone who needs specialized functionality or an ultra-compact build for an embedded system project.

We have discussed the distributions explicitly mentioned in the Linux Essentials objectives. Be aware that there are hundreds, if not thousands more that are available. While there are many different distributions of Linux, many of the programs and commands remain the same or are very similar.


![[Pasted image 20240916131834.png]]

----

[[NDG Linux Essentials - Challenge Lab A User Management]]
[[NDG Linux Essentials - Challenge Lab B Bash Scripting]]
[[NDG Linux Essentials - Challenge Lab C Log File Archiving]]
[[NDG Linux Essentials - Challenge Lab D Pipes, Redirection, and REGEX]]


## 3.2 Applications

The kernel of the operating system is like an air traffic controller at an airport, and the applications are the airplanes under its control. The kernel decides which program gets which blocks of memory, it starts and kills applications, and it handles displaying text or graphics on a monitor.

Applications make requests to the kernel and in return receive resources, such as memory, CPU, and disk space. If two applications request the same resource, the kernel decides which one gets it, and in some cases, kills off another application to save the rest of the system and prevent a crash.

The kernel also abstracts some complicated details away from the application. For example, the application doesn’t know if a block of disk storage is on a solid-state drive, a spinning metal hard disk, or even a network file share. Applications need only follow the kernel’s Application Programming Interface (API) and therefore don’t have to worry about the implementation details. Each application behaves as if it has a large block of memory on the system; the kernel maintains this illusion by remapping smaller blocks of memory, sharing blocks of memory with other applications, or even swapping out untouched blocks to disk.

The kernel also handles the switching of applications, a process known as multitasking. A computer system has a small number of central processing units (CPUs) and a finite amount of memory. The kernel takes care of unloading one task and loading a new one if there is more demand than resources available. When one task has run for a specified amount of time, the CPU pauses it so that another may run. If the computer is doing several tasks at once, the kernel is deciding when to switch focus between tasks. With the tasks rapidly switching, it appears that the computer is doing many things at once.

When we, as users, think of applications, we tend to think of word processors, web browsers, and email clients, however, there are a large variety of application types. The kernel doesn’t differentiate between a user-facing application, a network service that talks to a remote computer, or an internal task. From this, we get an abstraction called a process. A process is just one task that is loaded and tracked by the kernel. An application may even need multiple processes to function, so the kernel takes care of running the processes, starting and stopping them as requested, and handing out system resources.

## 3.2.1 Major Applications

The Linux kernel can run a wide variety of software across many hardware platforms. A computer can act as a server, which means it primarily handles data on others’ behalf, or as a desktop, which means a user interacts with it directly. The machine can run software or be used as a development machine in the process of creating software. A machine can even adopt multiple roles as Linux makes no distinction; it’s merely a matter of configuring which applications run.

One resulting advantage is that Linux can simulate almost all aspects of a production environment, from development to testing, to verification on scaled-down hardware, which saves costs and time. A Linux administrator could run the same server applications on a desktop or inexpensive virtual server that are run by large internet service providers. Of course, a desktop would not be able to handle the same volume as a major provider would, but almost any configuration can be simulated without needing powerful hardware or server licensing.

Linux software generally falls into one of three categories:

- **Server Applications**
    
    Software that has no direct interaction with the monitor and keyboard of the machine it runs on. Its purpose is to serve information to other computers, called clients. Sometimes server applications may not talk to other computers but only sit there and crunch data.
    
- **Desktop Applications**
    
    Web browsers, text editors, music players, or other applications with which users interact directly. In many cases, such as a web browser, the application is talking to a server on the other end and interpreting the data. This is the “client” side of a client/server application.
    
- **Tools**
    
    A loose category of software that exists to make it easier to manage computer systems. Tools can help configure displays, provide a Linux shell that users type commands into, or even more sophisticated tools, called compilers, that convert source code to application programs that the computer can execute.
    

The availability of applications varies depending on the distribution. Often application vendors choose a subset of distributions to support. Different distributions have different versions of key libraries, and it is difficult for a company to support all these different versions. Some applications, however, like Firefox and LibreOffice are widely supported and available for all major distributions.

The Linux community has come up with lots of creative solutions for both desktop and server applications. These applications, many of which make up the backbone of the Internet, are critical to understanding, and utilizing the power of Linux.

Most computing tasks can be accomplished by any number of applications in Linux. There are many web browsers, web servers, database servers, and text editors from which to choose. Evaluating application software is an important skill to be learned by the aspiring Linux administrator. Determining requirements for performance, stability, and cost are just some of the considerations needed for a comprehensive analysis.

-  [Previous](https://content.netdevgroup.com/contents/linux-essentials/GV3sPWsQ7r/3.2)
- [Next](https://content.netdevgroup.com/contents/linux-essentials/GV3sPWsQ7r/3.2.2)

---

NDG Linux Essentials - Chapter 4 - Open Source Software and Licensing

**UNIX** was initially created in 1969. By its fourth edition, in 1973, it had been rewritten in the C programming language that is still prominent today. In 1984 the University of California Berkeley released 4.2BSD which introduced TCP/IP, the networking specification that underpins the Internet. By the early 1990’s, when Linux development started, different companies developing UNIX operating systems realized their systems needed to be compatible, and they started working on the X/Open specification that is still used today.

Over the years, computer scientists and the organizations that employ them have realized the benefit of systems that provide familiar tools and consistent ways of accomplishing specific tasks. The standardization of application programming interfaces (APIs) allows programs written for one specific UNIX or Linux operating system to be ported (converted) relatively easy to run on another. So, while proprietary UNIX systems are still in use throughout the world in environments where "certified" solutions are preferred, the interoperability of these systems alongside Linux computers is valued by industry, academia, and governments that use them.

The importance of standards organizations cannot be overstated. Groups like the **IEEE (Institute of Electrical and Electronics Engineers)** and **POSIX (Portable Operating System Interface)**, allow professionals from different companies and institutions to collaborate on specifications that make it possible for different operating systems and programs to work together. It doesn’t matter if a program is closed or open source, simple or complex, if it is written to these standards others will be able to use and modify it in the future. Every innovation in computing is built on the work of others who came before. Open source software is a collaboration of different people with different needs and backgrounds all working together to make something better than any one of them could have made individually. Standards are what makes this possible, and the many organizations that create, maintain and promote them are integral to the industry.

---

## 4.2 Open Source Licensing

When talking about buying software, there are three distinct components:

- **Ownership** – Who owns the intellectual property behind the software?
- **Money Transfer** – How does money change hands, if at all?
- **Licensing** – What do you get? What can you do with the software? Can you use it on only one computer? Can you give it to someone else?

In most cases, the ownership of the software remains with the person or company that created it. Users are only granted a license to use the software; this is a matter of copyright law. The money transfer depends on the business model of the creator. It’s the licensing that differentiates open source software from closed source software.

Two contrasting examples will get things started.

With Microsoft Windows, the Microsoft Corporation owns the intellectual property. The license itself, the **End User License Agreement (EULA)**, is a custom legal document that you must click through, indicating your acceptance, in order to install the software. Microsoft keeps the source code and distributes only binary copies through authorized channels. For most consumer products you are allowed to install the software on one computer and are not allowed to make copies of the disk other than for a backup. You are not allowed to reverse engineer the software. You pay for one copy of the software, which gets you minor updates but not major upgrades.

Linux is owned by Linus Torvalds. He has placed the code under a license called **GNU General Public License version 2 (GPLv2)**. This license, among other things, says that the source code must be made available to anyone who asks and that anyone is allowed to make changes. One caveat to this is that if someone makes changes and distributes them, they must put the changes under the same license so that others can benefit. GPLv2 also says that no one is allowed to charge for distributing the source code other than the actual costs of doing so (such as copying it to removable media).

In general, when someone creates something, they also get the right to decide how it is used and distributed. **Free and Open Source Software (FOSS)** refers to software where this right has been given up; anyone is allowed to view the source code and redistribute it. Linus Torvalds has done that with Linux – even though he created Linux he can’t forbid someone from using it on their computer because he has given up that right through the GPLv2 license.

Software licensing is a political issue, therefore it should come as no surprise that there are many different opinions. Organizations have come up with their own license that embodies their particular views, so it is easier to choose an existing license than come up with your own. For example, universities like the Massachusetts Institute of Technology (MIT) and University of California have come up with licenses, as have projects like the Apache Foundation. Also, groups like the Free Software Foundation have created their own licenses to further their agenda.

---

## 4.2.1 The Free Software Foundation

Two groups can be considered the most influential forces in the world of open source: the Free Software Foundation and the Open Source Initiative.

Only a few years after the development of the GNU project, Richard Stallman founded the **Free Software Foundation (FSF)** in 1985 with the goal of promoting free software. In this context, the word "free" does not refer to the price, but to the freedom to share, study, and modify the underlying source code. According to their website, the FSF believes that users should have "control over the technology we use in our homes, schools, and businesses".

FSF also advocates that software licenses should enforce the openness of modifications. It is their view that if someone modifies free software that they should be required to share any changes they have made when they share it again. This specific philosophy is called copyleft. According to FSF, "copyleft is a general method for making a program (or other work) free (in the sense of freedom, not "zero price"), and requiring all modified and extended versions of the program to be free as well".

The FSF also advocates against software patents and acts as a watchdog for standards organizations, speaking out when a proposed standard might violate the free software principles by including items like Digital Rights Management (DRM) which restrict what can be done with compliant programs.

The FSF have developed their own set of licenses which are free for anyone to use based on the original **GNU General Public License (GPL)**. FSF currently maintains GNU General Public License version 2 (GPLv2) and version 3 (GPLv3), as well as the GNU Lesser General Public Licenses version 2 (LGPLv2) and version 3 (LGPLv3). These licenses are meant to be included in the actual source code to ensure that all future variants and modifications of the original program continue to have the same freedom of use as the original. The GPL license and its variants are powerful legal tools to advance the cause of free software worldwide. What started off in 1983 as one man’s desire to share and improve software by letting others change it has ended up changing the world.

> [!NOTE]
> **Consider This**
> 
> The changes between GPLv2 and GPLv3 largely focused on using free software on a closed hardware device which has been coined Tivoization. TiVo is a company that builds a television digital video recorder on their own hardware and used Linux as the base for their software. While TiVo released the source code to their version of Linux as required under GPLv2, the hardware would not run any modified binaries. In the eyes of the FSF, this went against the spirit of the GPLv2, so they added a specific clause to version 3 of the license. Linus Torvalds agrees with TiVo on this matter and has chosen to stay with GPLv2.

---
## 4.2.3 Creative Commons

FOSS licenses are mostly related to software. People have placed works such as drawings and plans under FOSS licenses, but this was not the intent.

When software has been placed in the public domain, the author has relinquished all rights, including the copyright on the work. In some countries, this is the default when the work is done by a government agency. In some countries, copyrighted work becomes public domain after the author has died and a lengthy waiting period has elapsed.

The **Creative Commons (CC)** organization has created the Creative Commons Licenses which try to address the intentions behind FOSS licenses for non-software entities. CC licenses can also be used to restrict commercial use if that is the desire of the copyright holder. The CC licenses are made up of the following set of conditions the creator can apply to their work:

- **Attribution (BY)** – All CC licenses require that the creator must be given credit, without implying that the creator endorses the use.
    
- **ShareAlike (SA)** – This allows others to copy, distribute, perform, and modify the work, provided they do so under the same terms.
    
- **NonCommercial (NC)** – This allows others to distribute, display, perform, and modify the work for any purpose other than commercially.
    
- **NoDerivatives (ND)** – This allows others to distribute, display, and perform only original copies of the work. They must obtain the creator’s permission to modify it.

These conditions are then combined to create the six main licenses offered by Creative Commons:

- **Attribution (CC BY)** – Much like the BSD license, you can use CC BY content for any use but must credit the copyright holder.
    
- **Attribution ShareAlike (CC BY-SA)** – A copyleft version of the Attribution license. Derived works must be shared under the same license, much like in the Free Software ideals.
    
- **Attribution NoDerivs (CC BY-ND)** – You may redistribute the content under the same conditions as CC-BY but may not change it.
    
- **Attribution-NonCommercial (CC BY-NC)** – Just like CC BY, but you may not use it for commercial purposes.
    
- **Attribution-NonCommercial-ShareAlike (CC BY-NC-SA)** – Builds on the CC BY-NC license but requires that your changes be shared under the same license.
    
- **Attribution-NonCommercial-NoDerivs (CC BY-NC-ND)** – You are sharing the content to be used for non-commercial purposes, but people may not change the content.
    
- **No Rights Reserved (CC0)** – This is the Creative Commons version of public domain.

---
## 4.3 Open Source Business Models

If all this software is free, how can anyone make money off of it?

First, you must understand there isn’t anything in the GPL that prohibits selling software. In fact, the right to sell software is part of the GPL license. Again, recall that the word free refers to freedom, not price. Companies that add value to these free programs are encouraged to make as much money as they can, and put those profits back into developing more and better software.

One of the simplest ways to make money is to sell support or warranty around the software. Companies like Canonical, the developer of Ubuntu, and Redhat have grown into huge enterprises by creating Linux distributions and tools that enable commercial users to manage their enterprises and offer products and services to their customers.

Many other open source projects have also expanded into substantial businesses. In the 1990s, Gerald Combs was working at an Internet service provider and started writing his own network analysis tool because similar tools at the time were costly. Over 600 people have now contributed to the project, called Wireshark. It is now often considered better than commercial offerings and led to a company being formed to sell products and support. Like many others, this company was purchased by a larger enterprise that supports its continued development.

Companies like Tivo have packaged hardware or add extra closed source software to sell alongside the free software. Appliances and embedded systems that use Linux are a multi-billion dollar business and encompass everything from home DVRs to security cameras and wearable fitness devices. Many consumer firewalls and entertainment devices follow this model.

Today, both large and small employers have individuals and sometimes whole groups devoted to working on open source projects. Technology companies compete for the opportunity to influence projects that will shape the future of their industries. Other companies dedicate resources towards projects they need for internal use. As more business is done on cloud resources, the opportunity for open source programmers continues to expand.

---
## NDG Linux Essentials - Chapter 6 - Getting Help

**Consider This**

The `man` command uses a pager to display documents. Usually, this pager is the `less` command, but on some distributions, it may be the `more` command. Both are very similar in how they perform.

To view the various movement commands that are available, use the **H** key while viewing a man page. This displays a help page.

Pagers will be discussed in more detail later in the course.

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

-----


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

To find any file or directory, use the `locate` command. This command searches a database of all files and directories that were on the system when the database was created. Typically, the command to generate this database is run nightly.

---

Any files created today will not be searchable with the `locate` command. If root access is available, it’s possible to update the `locate` database manually by running the `updatedb` command. Regular users cannot update the database file.

Also note that when using the `locate` command as a regular user, the output may be limited due to file permissions. If the user that is logged in doesn’t have access to a file or directory on the filesystem due to permissions, the `locate` command won't return those names. This security feature is designed to keep users from "exploring" the filesystem by using the `locate` database. The `root` user can search for any file in the `locate` database.

The output of the locate command can be quite large. When searching for a filename, such as `passwd`, the `locate` command produces every file that contains the string `passwd`, not just files named passwd.

In many cases, it is helpful to start by finding out how many files match. Do this by using the `-c` option to the `locate` command:

---

## Info Documentation

Man pages are excellent sources of information, but they do tend to have a few disadvantages. One example is that each man page is a separate document, not related to any other man page. While some man pages have a `SEE ALSO` section that may refer to other man pages, they tend to be independent sources of documentation.

The `info` command also provides documentation on operating system commands and features. The goal is slightly different from man pages: to provide a documentation resource that gives a logical organizational structure, making reading documentation easier.

All of the documentation is merged into a single "book" representing all of the documentation available. Within info documents, information is broken down into categories that work much like a table of contents in a book. Hyperlinks are provided to pages with information on individual topics for a specific command or feature.

Another advantage of info over man pages is that the writing style of info documents is typically more conducive to learning a topic. Consider man pages to be more of a reference resource and info documents to be more of a learning guide.