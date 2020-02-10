title: 【Python】正则表达式的相关笔记
url: 368.html
id: 368
categories:
  - Python
tags: []
date: 2019-05-02 16:43:00
---

### re.match(pattern, string, flags=0)

该函数是**从头开始**匹配字符串，也就是说，对于文本内容, 想要匹配 `[i++]`

    disr[i++]=

如果像这样使用

    re.match(r'(\[.*?\])', 'disr[i++]=')

是无法匹配到的，需要修改为：

    re.match(r'.*(\[.*?\])', 'disr[i++]=')

### re.findall(pattern, string, flags=0)

可以在pattern中用（）扩起若干表达式，最终会返回匹配每个表达式的元组。 EG：

    
    str='"加泰罗尼亚地图集.Atlas catalan.图8.jpg*34072643*2018-10-23 18:07:02"'
    print(re.findall(r'\"(.*?)\*([0-9]*)\*', str))
    
    output: ('加泰罗尼亚地图集.Atlas catalan.图8.jpg', '34072643')