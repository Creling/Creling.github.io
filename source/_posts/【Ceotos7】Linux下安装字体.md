---
title: 【Ceotos7】Linux下安装字体
url: 296.html
id: 296
categories:
  - Linux &amp; VPS
date: 2019-01-28 10:38:34
tags:
---

> yum install -y fontconfig mkfontscale 
> cd /usr/share/fonts/ #将tff文件拷贝至该目录后
> mkfontscale
> mkfontdir
> fc-cache 
> fc-list#查看已安装字体列表