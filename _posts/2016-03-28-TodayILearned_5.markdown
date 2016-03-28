---
layout: post
title:  "Let's Build A Web Server Part 3"
date:   2016-03-23 20:03:49
categories: jekyll update
---
Ruslan has done it again. We finished off the three part series with knowledge of allowing our server to handle multiple requests at once. The answer: concurrency!! We started off with (1) a review of the tcp socket connection made by the client and server and then learned all about (2) how to fork multiple child processes, having the parent process handle the child processes (file descriptors and all), and (3) the danger of zombies.

1)
  Iterative server
  Server socket creation sequence (socket, bind, listen, accept)
  Client connection creation sequence (socket, connect)
  Socket pair
  Socket
  Ephemeral port and well-known port
  Process
  Process ID (PID), parent process ID (PPID), and the parent-child relationship.
  File descriptors
  The meaning of the BACKLOG argument of the listen socket method

2) 
  The simplest way to write a concurrent server in Unix is to use the fork() system call
  When a process forks a new process it becomes a parent process to that newly forked child process.
  Parent and child share the same file descriptors after the call to fork.
  The kernel uses descriptor reference counts to decide whether to close the file/socket or not
  The role of a server parent process: all it does now is accept a new connection from a client, fork a child to handle the client request, and loop over to accept a new client connection.

 3) 
  If you don’t close duplicate descriptors, the clients won’t terminate because the client connections won’t get closed.
  If you don’t close duplicate descriptors, your long-running server will eventually run out of available file descriptors (max open files).
  When you fork a child process and it exits and the parent process doesn’t wait for it and doesn’t collect its termination status, it becomes a zombie.
  Zombies need to eat something and, in our case, it’s memory. Your server will eventually run out of available processes (max user processes) if it doesn’t take care of zombies.
  You can’t kill a zombie, you need to wait for it.

  I highly reccommend this tutorial series! Thanks Ruslan!

[Let’s Build A Web Server. Part 3.](https://ruslanspivak.com/lsbaws-part3/) 












