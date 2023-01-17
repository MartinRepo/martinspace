---
title: "High-level Petri Net"
date: 2023-01-11T20:47:53Z
draft: false
author: ["Martin"]
categories: 
- 分类1
- 分类2
tags: 
- software engineering
description: ""
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true #顶部显示当前路径
cover:
    image: ""
    caption: ""
    alt: ""
    relative: false
mermaid: true
---
复（预）习过程中遇到Petri net，记录一下

Petri Net是一种系统模型。因为不确定哪个transition会先fire，所以它是非确定性的，通常被用于建立离散分布式系统。

Petri Net组成元素
- place: 通常用圆圈表示
- token: 在place中，通常用实心点表示
- transition: 通常用直角矩形或实心矩形表示
- arc: 通常是带箭头的一条线，权重可以通过标数字在线上，或者画出几条arc来表示。

<div align="center">
{{<mermaid>}}
flowchart LR
br<-->id1((...))
id1((...))==2==>rr
id2((..))-->br
id2((..))==2==>bb
bb-->id2((..))
rr-->id2((..))
{{</mermaid>}}
</div>

找出上述Petri net中reachable state和deadlock state的数量

<div align="center">
{{<mermaid>}}
flowchart TD
id1(3, 2)==bb/br==>id2(3, 1)
id1(3, 2)==rr==>id3(1, 3)
id2(3, 1)==rr==>id4(1, 2)
id3(1, 3)==bb/br==>id4(1, 2)
id3(1, 3)==br==>id5(3, 0)
id4(1, 2)==bb/br==>id6(1, 1)
id5(3, 0)==rr==>id6(1, 1)
id6(1, 1)==br==>id7(1, 0)
{{</mermaid>}}
</div>

由上图可知，这里有7个reachable states，一个死锁状态，当左侧place中没有token并且右侧place只有1个token时，rr, bb, br都不是enabled的状态，因此都不能被fire。所以只有一个死锁状态。