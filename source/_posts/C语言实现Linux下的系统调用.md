---
title: C语言实现Linux下的系统调用
url: 336.html
id: 336
categories:
  - Linux &amp; VPS
date: 2019-03-08 10:57:44
tags:
---

Linux下的系统调用利用C语言实现，可以有两种方式

#### 1.syscall函数

    NAME
           syscall - 间接系统调用
    SYNOPSIS
           #include <unistd.h>
           #include <sys/syscall.h>                 /* For SYS_xxx definitions */
    

调用 `int syscall(int number, para1, para2...);` E.g. write()函数原型为： `ssize_t write(int fd,const void*buf,size_t count);` write()在Linux系统中的调用号为1 则通过syscall()函数调用write()的方法为： `syscall(1,int fd,const void*buf,size_t count)`