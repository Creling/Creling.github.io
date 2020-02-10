title: Dell服务器的几款raid工具
url: 497.html
id: 497
categories:
  - Linux &amp; VPS
date: 2019-10-04 17:32:33
tags:
---
收集了大部分dell平台下的raid工具，有一些比较古老了，很难找到相关资料，记录一下。

<!--more-->


## 1. perccli

据[reddit](https://www.reddit.com/r/sysadmin/comments/bvb48v/dells_perccli_perc_utility_and_the_delllsi_perc/)上网友评论，perccli适用于8系列或更高的raid卡，由于笔者并不拥有h800或更高级别的raid卡，因此无法验证消息可靠性。

> The h200 in spit of its name is not really a hardware raid.. Its actually software raid (like the h300 series). H200/300 do not have a battery either. It's software raid within the controller. Its equivalent to raid on your desktop motherboard in performance. According to Dell unless its a 8 series or newer you need to use the megacli software instead of the perccli

## 2. Megacli


是Lsi官方出品的自家raid管理工具，因为dell对raid卡的包装较少，因此可以直接使用在dell raid上，也是直接百度时可以找到的最常见的raid卡管理工具

## 3. Lsiutil


有一种说法是，支持raid5的被称为“阵列卡”，不支持raid5的被称为SAS卡。 Lsiutil就是针对sas卡的管理工具。但是已经非常古老了，连H200都无法支持。

> 参考链接：http://lists.us.dell.com/pipermail/linux-poweredge/2010-March/041725.html PET310, CentOS5.4, mpt2sas 02.00.02.00 For previous MPT controllers we used LSI's lsiutil utility as a light weight alternative to OMSA's "omreport storage controller". Now with the new SAS2 controllers, such as the PERC H200, lsiutil won't work anymore (tried with v1.62), and you need the new sas2ircu utility, whose syntax is documented here: http://www.lsi.com/DistributionSystem/AssetDocument/SAS2\_IR\_User_Guide.pdf

## 4. SAS2IRCU


比Lsiutil更新的raid管理工具，适用于H200等，与此类似的还有SAS3IRCU