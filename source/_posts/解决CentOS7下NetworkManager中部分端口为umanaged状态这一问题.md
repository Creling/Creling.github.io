---
title: 解决CentOS7下NetworkManager中部分端口为umanaged状态这一问题
url: 329.html
id: 329
categories:
  - Linux &amp; VPS
date: 2019-03-04 20:55:51
tags:
---

NetworkManager会默认放弃管理`/etc/sysconfig/network-scripts/ifcfg-*`中显示的网络接口，此时，该接口在命令`nmcli d`下的状态就是umanaged， ![](https://blog.fromling.com/wp-content/uploads/2019/03/3ffc0d6b7b06ad28a461c601f1d6fc21.png) 要想解决这个问题，需要以下几个步骤

    vim /etc/NetworkManager/NetworkManager.conf
    
    [main]
    plugins=ifcfg-rh # 将这一行注释掉
    

然后

    /etc/sysconfig/network-scripts/ifcfg-*
    
    NM_CONTROLLED=no # 将这一行注释掉
    

最后重启网络

    service network restart