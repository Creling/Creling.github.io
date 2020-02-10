title: 【VNC】Could not start d-bus. Can you call qdbus? 问题解决
url: 427.html
id: 427
categories:
  - Linux &amp; VPS
date: 2019-06-06 14:36:32
tags:
---
主要解决如下问题：

    Could not start d-bus. Can you call qdbus?`
    
<!--more-->


解决方案
--

    vim /usr/bin/startkde # 查看KDE启动脚本。
    

找到qdbus的定义，发现

    qdbus=qdbus
    

在bash下直接输入qdbus，报错

    X11 initialization failed
    

输入

    export DISPLAY=:0
    

解决