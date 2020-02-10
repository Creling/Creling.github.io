title: shell的字符串处理
author: Creling
toc: true
tags:
  - shell
categories:
  - Linux
date: 2020-01-17 12:46:00
---
**摘要** 借助`${expression}`表达式进行字符串操作的一些方法
<!--more-->

## 替换
```bash
${parameter:-word} # ${parameter}为空时用${word}替换
${parameter:=word} # ${parameter}为空时用${word}替换，并将值赋给$parameter变量
${parameter:?word} # ${parameter}为空时,以标准错误的方式输出${word}
${parameter:+word} # ${parameter}不为空时用${word}替换替换
```

## 截取
1. `${parameter%word}`  
最小限度从后面截去`${word}`，也就是说，从右向左，截去第一个出现的`${word}`及其右边的内容，保留左边的内容。
2. `${parameter%%word}`  
最大限度从后面截去`${word}`，也就是说，从右向左，截去最后一个出现的`${word}`及其右边的内容，保留左边的内容。
3. `${parameter#word}`
最小限度从前面截去`${word}`，也就是说，从左向右，截去第一个出现的`${word}`及其左边的内容，保留右边的内容。  
4. `${parameter##word}`
最大限度从前面截去`${word}`，也就是说，从左向右，截去最后一个出现的`${word}`及其左边的内容，保留右边的内容。  
5. `${parameter:offset}`或`${parameter:offset:length}`
从偏移量`${offset}`开始获得子序列，如果指定了`${length}`，则返回指定长度的子序列。当`${offset}`为负数时，为了避免和`${parameter:-word}`冲突，往往在`:`后加一个`0`或者空格。

## 杂项
```bash
${#parameter} # 获取字符串的长度
```