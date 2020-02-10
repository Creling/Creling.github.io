title: 配置双栈网站——使Nginx同时监听ipv4/ipv6
author: Creling
tags:
  - vps
categories:
  - Linux
toc: 'true'
date: 2019-12-11 00:27:00
---
**摘要** 提供了使Nginx同时监听ipv4和ipv6的配置方法

<!--more-->

曾经有一种方式是在端口前加上`[::]:`，具体操作方式如下：
```ini
# listen 80;
listen [::]:80;
# listen 443 ssl http2;
listen [::]:443 ssl http2;
```
但是新版Nginx默认启用`ipv6only=on`选项，如果按照上文方式修改，最终只会监听ipv6而不会监听ipv4，因此正确的修改方式显示指定监听ipv4和ipv6，具体操作如下：
```ini
listen 80;
listen [::]:80;
listen 443 ssl http2;
listen [::]:443 ssl http2;
```