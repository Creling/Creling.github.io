title: xfs文件系统移动分区
url: 467.html
id: 467
categories:
  - Linux
  - ''
tags: []
date: 2019-08-05 20:52:00
---

本文的适用于xfs文件系统（ext*文件系统可以直接用`parted`进行分区移动）

<!--more-->

步骤

1.  进入救援模式
2.  备份原本的分区（以`/dev/vd2`为例）

    dd if=/dev/vda2 of=/root/temp/vda2.bak
    

3.  删除原本的vda2分区，重新划分分区表
4.  还原先前的分区

    dd if=/root/temp/vda2.bak of=/dev/vda2