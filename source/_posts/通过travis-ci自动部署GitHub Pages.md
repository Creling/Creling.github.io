---
title: 通过Travis-CI自动部署GitHub Pages
author: Creling
toc: 'true'

---

**摘要：** 将Hexo博客部署在Github Pages上并通过Travis-CI进行持续集成和持续部署

<!--more-->

## 1. 整体思路
想要实现如标题所述的自动部署和发布，实际上有两种思路，各有优缺，分别记录如下：
1. 依靠Travis-CI持续集成，依靠Travis-CI的GitHub page组件持续部署
    这种思路需要一个repository和它的两个branch。
    将hexo安装目录推送到branch A，通过Travis-CI运行`hexo g`命令生成public文件夹，再通过Travis-CI将生成的public文件夹推送到branch B，Github Pages以branch B作为数据源。
    优点是设置时相对较方便
2. 依靠Travis-CI持续集成，依靠Hexo的hexo-deploy-git插件持续部署
    这种思路需要两个repository，每个repository分别需要一个branch。