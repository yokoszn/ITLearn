---
title: Troubleshooting Methodology
---
Understand the problem

most of the time you will just spend trying to understand the issue, once you know the issue its quite rudimentary to follow through with the solution.

applying the wrong solution to the wrong issue will result in lost time and potentially an unhappy client if stuff is truely on fire - [[Working Effectively in Crisis]]

Differential Diagnosis

What is broken? First think about how it works in most basic terms. Then build on that the things which can break. Then from those, pick the ones that could cause the symptoms you see.

Example:

You cannot ping a server.

### [Walk through of a diagnosis](https://www.opsschool.org/troubleshooting_101.html#id4)[](https://www.opsschool.org/troubleshooting_101.html#walk-through-of-a-diagnosis "Link to this heading")

- Eliminating variables
    

> - What changed recently?
>     
> - Could any of the symptoms be red herrings?
>     

- Common culprits (is it plugged in? is it network accessible?)
    
- Look through your logs
    
- Communicating during an outage
    
- ‘Talking Out-Loud’ (IRC/GroupChat)
    
- Communicating after an outage (postmortems)
    

### [Recent changes](https://www.opsschool.org/troubleshooting_101.html#id5)[](https://www.opsschool.org/troubleshooting_101.html#recent-changes "Link to this heading")

Often problems can be traced back to recent changes. Problems that start around the time of a change aren’t usually coincidence.

### [Learning common errors](https://www.opsschool.org/troubleshooting_101.html#id6)[](https://www.opsschool.org/troubleshooting_101.html#learning-common-errors "Link to this heading")

Over time you may find that a small set of errors cause a large portion of the problems you have to fix. Let’s cause some of these problems and see how we identify and fix them.

#### [Cannot bind to socket](https://www.opsschool.org/troubleshooting_101.html#id7)[](https://www.opsschool.org/troubleshooting_101.html#cannot-bind-to-socket "Link to this heading")

There are two common reasons that you can’t bind to a socket: the port is already in use, or you don’t have permission. As an example, you can see what happens when I try to start a Python SimpleHTTPServer on a port that is already in use:

python -m SimpleHTTPServer 8080
...
socket.error: [Errno 98] Address already in use

Here’s an example of what happens when I try to bind to a privileged port without proper permissions (in Linux, ports < 1024 are privileged):

python -m SimpleHTTPServer 80
...
socket.error: [Errno 13] Permission denied

#### [Permission denied reading from / writing to disk](https://www.opsschool.org/troubleshooting_101.html#id8)[](https://www.opsschool.org/troubleshooting_101.html#permission-denied-reading-from-writing-to-disk "Link to this heading")

#### [Out of disk space](https://www.opsschool.org/troubleshooting_101.html#id9)[](https://www.opsschool.org/troubleshooting_101.html#out-of-disk-space "Link to this heading")

(finding large files, and also finding deleted-but-open files)

#### [Mystery problems and SELinux](https://www.opsschool.org/troubleshooting_101.html#id10)[](https://www.opsschool.org/troubleshooting_101.html#mystery-problems-and-selinux "Link to this heading")

#### [Out of inodes](https://www.opsschool.org/troubleshooting_101.html#id11)[](https://www.opsschool.org/troubleshooting_101.html#out-of-inodes "Link to this heading")

Manifests as “disk full” when `df` claims you have disk space free.