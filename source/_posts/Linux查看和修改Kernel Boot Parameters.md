title: Linux查看和修改Kernel Boot Parameters
url: 359.html
id: 359
categories:
  - Linux &amp; VPS
tags: []
date: 2019-04-28 17:19:00
---
**摘要** 提供了查看和修改Linux系统的Kernel Boot Parameters的方法

<!--more-->

## 查看

通过`cat /proc/cmdline`命令可以查看当前的Kernel Boot Parameters

## 修改

    vi /etc/default/grub

添加一行

    GRUB_CMDLINE_LINUX_DEFAULT=&quot;要添加的命令&quot;

保存退出后

    grub2-mkconfig -o /boot/grub2/grub.cfg

重启即可