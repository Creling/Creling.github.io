title: 利用shadowsocks搭建6to4隧道
author: Creling
tags: []
categories:
  - vps
toc: 'true'
date: 2019-12-07 12:19:00
---
**摘要** 利用shadowsocks，搭建6to4隧道，使得纯ipv6服务器获得访问ipv4网络的能力。搭建过程中需要用到另外一台双栈服务器。下面将纯v6服务器称为A，双栈服务器称为B。A是隧道的客户端，B是隧道的服务端。

<!--more-->

## 安装
1. 安装shadowsocks
在A和B上分别运行如下命令，安装shadowsocks：
```bash
wget https://github.com/shadowsocks/shadowsocks-libev/releases/download/v3.3.3/shadowsocks-libev-3.3.3.tar.gz
tar zxvf shadowsocks-libev-3.3.3.tar.gz
cd shadowsocks-libev-3.3.3
yum install asciidoc xmlto pcre-devel mbedtls-devel libsodium-devel c-ares-devel libev-devel -y
./configure --prefix=/opt/shadowsocks-libev
make && make install
```

2. 配置隧道服务端
	1. 修改配置文件
    打开`/etc/shadowsocks.json`并添加如下内容：
    ```json
    {
            "server":["[::0]"],
            "server_port":<your server port>,
            "password":"<your password>",
            "timeout":300,
            "user":"nobody",
            "method":"salsa20",
            "fast_open":false,
            "nameserver":"8.8.8.8",
            "mode":"tcp_and_udp"
    }
    ```
    2. 运行服务端程序
    ```bash
    	/opt/shadowsocks-libev/bin/ss-server -c /etc/shadowsocks.json
    ```
    将会看到如下输出：
    ![](/images/pasted-1.png)

3. 配置隧道客户端
	1. 修改配置文件
    打开`/etc/shadowsocks.json`并添加如下内容：
    ```json
        {
          "server": "<A's ipv6>",
          "server_port": <A's port>,
          "password": "<your password",
          "method": "salsa20",
          "timeout": 20
        }
	```
    2. 运行客户端
    ```shell
    /opt/shadowsocks-libev/bin/ss-local -c /etc/shadowsocks.json
    ```
    将会看到如下输出：
    ![](/images/pasted-2.png)
    
## 测试
在A服务器下运行如下命令
```bash
curl --socks5 127.0.0.1:1080 baidu.com
```
看到如下输出：
![](/images/pasted-3.png)
说明一切正常