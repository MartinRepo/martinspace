---
title: "Use of MapEntry in Java"
date: 2023-02-04T22:31:02Z
lastmod: 2023-02-04T22:31:02Z
draft: false
author: ["Martin"]
tags: 
- Java
description: ""
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: false # 底部不显示分享栏
showbreadcrumbs: true #顶部显示当前路径
cover:
    image: ""
    caption: ""
    alt: ""
    relative: false
---

I met Map.Entry for many times when I was fighting with Leetcode. However, I did not understand it and it always confused me. I studied it today and write down to record it for myself.

(:[Click here for java documention](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/util/HashMap.html):)

Map.Entry is a internal interface of Map. It provides more convenient method for outputing key-value pair.

How do we output key-value pair of a Map generally?
- First, get all keys as a set
- Second, iterate to get every value according to keyset.

**If we have Map.Entry, we will get key and value at meantime.**


Some important methods:
| **Return Type** | **Method** | **Description** |
|-------------|--------|-------------|
|K|getKey()| Returns the key corresponding to this entry.|
|V|getValue()| Returns the value corresponding to this entry.|