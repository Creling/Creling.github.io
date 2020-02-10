title: 【CentOS7】给Linux服务器安装图形界面
url: 188.html
id: 188
categories:
  - Linux &amp; VPS
date: 2018-09-01 14:16:13
tags:
---
**摘要：** 提供了给Linux服务器安装图形界面的一种方法

如果说想要给本地的Linux发行版安装图形界面的话，是一件非常简单的事情，安装完成后，使用快捷键ctrl+F1/2/3/4便可以切换图形界面与命令行界面了。若是给远程Linux服务器安装图形界面的话，“安装图形界面”这个操作本身，其实和给本地Linux系统安装图形界面没有差别。但若是想要能够远程连接上图形界面，便要废一番周折了，毕竟，Linux系统可没有微软的远程桌面连接，xshell之类的ssh客户端也并不支持图形化界面。

### 安装图形界面

```bash
yum groupinstall "X Window System" //安装X(X Window System) yum groupinstall "GNOME Desktop"
```

### 安装、配置 VNC

1. 安装 VNC
	```
	yum install tigervnc-server
    ```

2. 配置 VNCServer
	```
	cp /lib/systemd/system/vncserver@.service /etc/systemd/system/vncserver@:1.service vi /etc/systemd/system/vncserver@:1.service
    ```




将文件修改为如下内容 （主要是将原文件中的 <>修改为 root）

```ini
    [Unit]
    Description=Remote desktop service (VNC)
    After=syslog.target network.target
    
    [Service]
    Type=forking
    # Clean any existing files in /tmp/.X11-unix environment
    ExecStartPre=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
    ExecStart=/usr/sbin/runuser -l root -c "/usr/bin/vncserver %i"
    PIDFile=/root/.vnc/%H%i.pid
    ExecStop=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
```
    

接着

> systemctl daemon-reload //更新systemctl以使其生效 vncpasswd root //设置vncserver的密码

*   使用 VNCServer

> systemctl start vncserver@:1.service // 启动VNC ；或者 vncserver :1 systemctl stop vncserver@:1.service // 停止VNC ；或者 vncserver -kill :1 systemctl enable vncserver@:1.service //设置为开机自动启动

*   关于VNC的其他命令

修改VNC界面的分辨率

> vi /usr/bin/vncserver

找到默认的1024*768修改为自己显示器的分辨率，并重启。 ps: 旧版本中可以通过修改配置文件`/etc/sysconfig/vncservers`来修改分辨率，但是在新版本中，此配置文件已被 弃用

#### 参考资料

[Linux CentOS 7的图形界面安装（GNOME、KDE等）](https://jingyan.baidu.com/article/0964eca26fc3b38284f53642.html) [CentOS7下安装配置vncserver](https://www.cnblogs.com/luhouxiang/p/4829443.html) [修改VNCSERVER 默认的分辨率的方法](https://www.cnblogs.com/del88/p/5656356.html)