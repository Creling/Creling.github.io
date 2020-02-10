title: 手动安装PHP扩展
url: 432.html
id: 432
categories:
  - Linux
  - ''
tags: []
date: 2019-06-11 08:47:00
---
**摘要** 记录了一次手动安装`tidy`扩展的过程。

<!--more-->

## 安装过程
1.  进入tidy的源码目录 `php/ssrc/ext/tidy`
2.  编译，这里的 phpsize 和 php-config 的目录需要自行寻找
	```shell
    /usr/local/php/bin/phpize 
    ./configure --with-php-config=/usr/local/php/bin/php-config
 	```
3.  安装
	```shell
    make && make install
    ```
4.  修改配置文件
	```shell
    vim /www/server/php/72/etc/php.ini # 配置文件目录需要自行查找
    ```
    - 将 `extension_dir` 设置为 `/www/server/php/72/lib/php/extensions/no-debug-non-zts-20170718/`，这里的具体值取决于步骤3中编译出的.so文件的位置  
    - 添加 `extension = "tidy.so"`
5. 重启php
    
## 错误排除
1. configure: error: Cannot find libtidy
   ```shell
    yum install libtidy-devel
    ```
    或者
    ```shell
    yum install http://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/l/libtidy-devel-5.4.0-1.el7.x86_64.rpm
    ```
    
2. re2c not found
    ```shell
    wget http://downloads.sourceforge.net/project/re2c/re2c/0.13.7.5/re2c-0.13.7.5.tar.gztar xzf re2c-0.13.7.5.tar.gzcd re2c-0.13.7.5./configuremake && make install
    ```

## 补充说明
其实用`pecl`自动安装是最方便的。