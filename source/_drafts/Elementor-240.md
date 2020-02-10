---
title: 'Elementor #240'
url: 240.html
id: 240
categories:
  - Linux &amp; VPS
tags:
---

### Privoxy

### 安装

yum install -y epel-release yum install privoxy

    <br>
    
    + 配置
    
    

vim /etc/privoxy/config

在 froward-socks4下面添加一条socks5的，因为shadowsocks是socks5，
===================================================

地址是127.0.0.1:1080。注意他们最后有一个“.”
==============================

#        forward-socks4   /               socks-gw.example.com:1080  . forward-socks5   /               127.0.0.1:1080 .  

下面还存在以下一条配置，表示privoxy监听本机8118端口，
================================

把它作为http代理，代理地址为 http://localhost.8118/ 。
=========================================

可以把地址改为 0.0.0.0:8118，表示外网也可以通过本机IP作http代理。
==========================================

这样，你的外网IP为1.2.3.4，别人就可以设置 http://1.2.3.4:8118/ 为http代理。
=======================================================

　listen-address localhost:8118    systemctl restart privoxy.serivce  ```