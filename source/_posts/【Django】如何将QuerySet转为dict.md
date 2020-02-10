title: 将QuerySet转为dict
tags:
  - django
  - web
url: 505.html
id: 505
categories:
  - Python
date: 2019-10-27 13:47:00
---
**摘要** 关于这个问题，中文互联网上有很多错误的方案，这里记录一种亲测可行的解决方案

<!--more-->

具体的场景是：

通过`ServerModel.objects.all().values()`获得了一个`QuerySet`类对象
```python
    <QuerySet [{'id': 1, 'server_ip': '193.221.232.1', 'server_name': 'sss', 'server_user': '', 'server_passwd': '', 'server_createtime': datetime.datetime(2019,10, 25, 4, 20, 8, 570196, tzinfo=<UTC>), 'server_comment': ''}, {'id': 2, 'server_ip': '193.221.232.2', 'server_name': 'sss', 'server_user': '', 'server_passwd': '', 'server_createtime': datetime.datetime(2019, 10, 25, 4, 23, 24, 77533, tzinfo=<UTC>), 'server_comment': ''}]>
```

 现在希望将这个对象通过`JsonResponse()`发送出去。由于`JsonResponse()`的安全限制，只允许发送`dict`对象，因此需要将`QuerySet`转为`dict` 。
 
 在中文互联网下，大部分的方法是调用`model_to_dict`函数，这是非常愚蠢的做法，顾名思义，`model_to_dict`负责将`model`类而不是`QuerySet`类转变为`dict`，如果坚持使用`model_to_dict`则会报错`'QuerySet' object has no attribute '_meta'`。
  
  正确的做法是使用`list`函数。 将`list()`作用在`QuerySet`上会得到一个`list`对象

```python
    [{'id': 1, 'server_ip': '193.221.232.1', 'server_name': 'sss', 'server_user': '', 'server_passwd': '', 'server_createtime': datetime.datetime(2019,10, 25, 4, 20, 8, 570196, tzinfo=<UTC>), 'server_comment': ''}, {'id': 2, 'server_ip': '193.221.232.2', 'server_name': 'sss', 'server_user': '', 'server_passwd': '', 'server_createtime': datetime.datetime(2019, 10, 25, 4, 23, 24, 77533, tzinfo=<UTC>), 'server_comment': ''}]
```

  随后将这个`list`对象放入一个`dict`并赋予键名即完成了`QuerySet`到`dic`t的转换.