title: centos7 升级内核
url: 161.html
id: 161
categories:
  - Linux &amp; VPS
date: 2018-07-24 12:29:39
tags:
---
其实本身想到升级内核是为了能够开启BBR进而对网速进行加速，但不知何故，网上的各种一键脚本都卡在了更换内核的步骤上，主要症状表现为：

1.  新内核的确被安装了
2.  直接reboot命令重启，依然会进入旧内核
3.  通过VNC连接，手动选择新内核进行启动，则会启动失败.

正文
--

研究了网上的几篇文章，发现问题主要出在没有编译内核启动文件上，为了以后遇到相似的情况可以迅速找到解决办法，撰本篇博文以记录：

    #使用cat /boot/grub2/grub.cfg |grep menuentry  查看系统可用内核
    #这是我的输出内容，引号之间为内核名
    if [ x"${feature_menuentry_id}" = xy ]; then
    menuentry_id_option="--id"
    menuentry_id_option=""
    export menuentry_id_option
    menuentry'CentOS Linux (4.11.8-1.el7.elrepo.x86_64) 7 (Core)' --class gnu-linux --class gnu --class os --unrestricted $menuentry_id_option  'gnulinux-simple-LABEL=root' {
    menuentry 'CentOS Linux' --class gnu-linux --class gnu --class os --unrestricted $menuentry_id_option 'gnulinux-simple-LABEL=root' {
    submenu 'Advanced options for CentOS Linux' $menuentry_id_option 'gnulinux-advanced-LABEL=root' {
    menuentry 'CentOS Linux, with Linux 3.10.0-123.4.4.el7.x86_64' --class gnu-linux --class gnu --class os --unrestricted $menuentry_id_option 'gnulinux-3.10.0-123.4.4.el7.x86_64-advanced-LABEL=root' {
    menuentry 'CentOS Linux, with Linux 3.10.0-123.4.4.el7.x86_64 (recovery mode)' --class gnu-linux --class gnu --class os --unrestricted $menuentry_id_option 'gnulinux-3.10.0-123.4.4.el7.x86_64-recovery-LABEL=root' {
    

安装新内核后，需要使用以下命令修改内核配置文件

    vi /etc/default/grub
    

将第一行内容修改为

    GRUB_DEFAULT=0 #或者其他内核，内核名参加上面
    

之后，重新编译内核启动文件

    grub2-mkconfig -o /boot/grub2/grub.cfg
    

错误排除
----

1.  /boot/grub2/grub.cfg不存在（grub2-mkconfig: command not found）
    1.  打开grub.conf `shell vi /etc/grub.conf`
    2.  将default=0修改为default=1（具体取决于希望使用的内核在列表中的顺序）