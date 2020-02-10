title: 【摘抄】Djangodui对URL尾斜杠(back slash)的处理
url: 453.html
id: 453
categories:
  - Linux &amp; VPS
date: 2019-07-06 20:58:27
tags:
---
**摘抄自 https://www.bbsmax.com/A/kjdwABD6JN/** 

首先说下什么是尾斜杠。

    http://www.baidu.com/    # 有尾斜杠
    http://www.baidu.com     # 无尾斜杠
    

那么为什么我们要关注尾斜杠这个问题呢？这个要从Django和Flask对于URL的设置说起。 Django和Flask设置URL方式：

    r'^admin/$'   # Django
    'admin/'   # flask
    

可见两者都是基于字符串的匹配。所以问题就出来了： 如果我设置了一个形如'admin'的URL，那么当用户输入'admin/'的时候应不应该匹配呢？ 或者换种说法： 如果我设置了一个形如'admin/的'URL，那么当用户输入'admin'的时候应不应该匹配呢？ 这就是尾斜杠问题。 下面我们看看Django和Flask是如何处理的。 Django中的处理方法是提供了一个设置项，`APPEND_SLASH`，这个设置的默认值是True。当APPEND_SLASH为True的时候，如果一个URL没有匹配成功，那么Django会在这个URL尾部加上一个`/`并重新redirect回来。如果设置为False，那没有匹配成功的时候就什么都不会做。 需要注意的是，由于采用了redirect的方式，所以POST数据可能会丢失。 Flask默认行为和Django一样，只不过文档中并没有说明是不是采用redirect方法，如果不是的话，那么数据就没有丢失的风险了。 总结 **如果设置了'admin'，那么只有'admin'会匹配，'admin/'不会匹配。** **如果设置了'admin/'，那么'admin'和'admin/'都会匹配。**