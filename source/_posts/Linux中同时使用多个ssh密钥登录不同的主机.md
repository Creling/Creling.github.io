---
title: Linux中同时使用多个ssh密钥登录不同的主机
url: 332.html
id: 332
categories:
  - Linux &amp; VPS
date: 2019-03-04 21:06:39
tags:
---

在配置密钥实现免密登录的时候，Linux会自动加载如下面的四个密钥

    ~/.ssh/id_rsa
    ~/.ssh/id_dsa
    ~/.ssh/id_ed25519
    ~/.ssh/id_ecdsa
    

而其他名称的密钥是不会被自动加载的，因此其他密钥对应的服务器无法直接实现免密登录。 要想解决这个问题，可以通过增加ssh配置文件来实现，具体操作如下：

    vim ~/.ssh/config
    
    添加如下内容
    Host mydomain.com # 要实现免密登录的主机名
        IdentityFile ~/.ssh/id_rsa_mydomain.com # 该主机对应的密钥的路径
        User root # 该密钥对应的用户名
    

并保重密钥为600权限即可