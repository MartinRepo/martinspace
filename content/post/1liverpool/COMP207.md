---
title: "COMP207"
date: 2022-12-06T21:04:10Z
draft: false
author: ["Martin"]
categories: 
- 分类1
- 分类2
tags: 
- 数据库
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
    image: "img/dbms.png"
    caption: ""
    alt: ""
    relative: false
---
> 这是对上学期数据库课程的总结，也可以称为复习笔记，供梳理知识，为Final作准备。
<h2>1. Transaction 事务</h2>
</br>

| A | C | I | D |
| :----: | :-----------: | :----: | :-----------: |
| Atomicity | Consistency | Isolation | Durability |
| 原子性 | 一致性 | 隔离性 | 持久性 |

</br>
<b>原子性：</b>一个事务中，要么当中的操作都发生，要么都不发生。举个栗子：银行转账中，A向B转账300元，转账结束后，A账户少了300块，B账户没有增加300块，或者B账户多了300块，但A账户一分钱没少。以上情况均破坏了原子性。
</br>
<b>一致性：</b>事务完成后，结果要符合逻辑运算。还以银行转账为例，A向B转账300元，而转账后的结果是A多了300元B少了300元，这就破坏了一致性。
</br>
<b>隔离性：</b>
</br>
<b>持久性：</b>

***
<h2>2. Query processing 查询处理</h2>

***
<h2>3. Distributed databases 分布式数据库</h2>

***
<h2>4. Beyond relational data 关系型数据结构</h2>

***
<h2>5. Data-warehousing 数据挖掘</h2>