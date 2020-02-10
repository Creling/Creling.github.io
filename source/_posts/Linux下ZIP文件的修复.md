title: Linux下ZIP文件的修复
url: 440.html
id: 440
categories:
  - Linux
tags: []
toc: true
date: 2019-06-25 10:21:00
---

对于zip文件而言，即使文件残缺，也可以通过截断残缺部分的方式来获取余下完整部分的内容。对于zip文件而言，即使文件残缺，也可以通过截断残缺部分的方式来获取余下完整部分的内容。

<!--more-->

## 正文


一般来说，下载没有完成的zip文件在解压的时候遇到的问题都是
```shell
Missing end (EOCDR) signature
```

不要慌，这只是已经下载的zip压缩包中最后一个文件的EOCDR损坏，因此之前的文件依然是可以识别的。 实战如下：
```shell
[root@localhost temp]# zip -FF tempae --out tempaefix.zip
Fix archive (-FF) - salvage what can
    zip warning: Missing end (EOCDR) signature - either this archive
                     is not readable or the end is damaged
Is this a single-disk archive?  (y/n): y
  Assuming single-disk archive
Scanning for entries...
  Found spanning marker, but did not expect split (multi-disk) archive...
 copying: 158g0141  (104857600 bytes)
 copying: 158g0142  (104857600 bytes)
 copying: 158g0143  (104857600 bytes)
 copying: 158g0144  (104857600 bytes)
 copying: 158g0145  (104857600 bytes)
 copying: 158g0146  (104857600 bytes)
 copying: 158g0147  (104857600 bytes)
 copying: 158g0148  (104857600 bytes)
 copying: 158g0149  (104857600 bytes)
 copying: 158g0150 
    zip warning: no end of stream entry found: 158g0150
    zip warning: rewinding and scanning for later entries
```

  可以看到，`158g0150`没有能够成功读取，但是`158g0141`~`158g0149`都可以正确识别。 如果此时直接解压上一步命令的输出文件`tempaefix.zip`，依然会报错(这个问题留待以后研究) 但是我们可以对`tempaefix.zip`再次进行修复
```bash
[root@localhost temp]# zip -FF tempaefix.zip --out tempaefix1.zip
Fix archive (-FF) - salvage what can
    zip warning: Missing end (EOCDR) signature - either this archive
                     is not readable or the end is damaged
Is this a single-disk archive?  (y/n): y
  Assuming single-disk archive
Scanning for entries...
 copying: 158g0141  (104857600 bytes)
 copying: 158g0142  (104857600 bytes)
 copying: 158g0143  (104857600 bytes)
 copying: 158g0144  (104857600 bytes)
 copying: 158g0145  (104857600 bytes)
 copying: 158g0146 
    zip warning: no end of stream entry found: 158g0146
    zip warning: rewinding and scanning for later entries
```

  此时输出的`tempaefix1.zip`便可以正确解压了，如果依然不ok，则可以对新的输出文件继续修复知道可以正确解压为止。