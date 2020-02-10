title: Linux下几种socks流量转http(s)流量的工具
url: 224.html
id: 224
categories:
  - Linux &amp; VPS
date: 2018-11-11 16:54:22
tags:
---
ShadowSocket是socket5代理，对于浏览器而言，还需要另外一个socks转http(s)的工具，Windows下自带了proxy，但是Linux下并没有，这里收集整理了一些Linux下的socks转http(s)工具，或许什么时候会用上。
1. Privoxy
	1. 安装
    ```shell
    yum install -y epel-release
    yum install privoxy
    ```
	2. 配置
    ```shell
	vim /etc/privoxy/config
	#在 froward-socks4下面添加一条socks5的，因为shadowsocks是socks5，
	#地址是127.0.0.1:1080。注意他们最后有一个“.”
	#forward-socks4 / socks-gw.example.com:1080 .
	forward-socks5 / 127.0.0.1:1080 .
	#下面还存在以下一条配置，表示privoxy监听本机8118端口，
	#把它作为http代理，代理地址为 http://localhost.8118/ 。
	#可以把地址改为 0.0.0.0:8118，表示外网也可以通过本机IP作http代理。
	#这样，你的外网IP为1.2.3.4，别人就可以设置 http://1.2.3.4:8118/ 为http代理。
	listen-address localhost:8118
    ```
    3. 重启
    ```
    systemctl restart privoxy.serivce


#### Polipo

#### 安装

> yum install -y texi2html texinfo
> git clone https://github.com/jech/polipo.git
> cd polipo
> make all
> make install

#### 配置

> vi /etc/polipo/config