---
title: "CYK"
date: 2022-12-09T14:41:23Z
draft: false
author: ["Martin"]
categories: 
- 分类1
- 分类2
tags: 
- 计算理论
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
---
CYK算法
芜湖！刚刚把CYK算法搞懂了。之前不理解的点在于table cells,我一直认为一个cell是一个三角形，结果始终搞不懂算法的原理。
实际上，一个cell就是一个数字，下面我以input=4举例进行说明。

| CYK table |
| :----: | :-----------: | :----: | :-----------: |
| 14 | 
| 13 | 24 |   
| 12 | 23 | 34 |    
| 11 | 22 | 33 | 45 |
| x1 | x2 | x3 | x4 |

伪代码如下
```rust
for all cells in last row
if there is a production A -> x[i]
put A in table cell ii

for cells st in other rows // 自下而上推导
if there is a production A -> BC
where B is in cell sj and C is in cell (j+1)t
put A in cell st

```
首先，cell表示的是数字，上图中11，22，33，44这样的数字，每个数字都是一个cell。接下来分析伪代码，首先是第一个循环，是对于最下面一行：11，22，33，44。即找出所有能推出xi的字符，这是最好理解的一行，不多赘述。
接下来是第二个循环，从倒数第二行开始，st即表中的12，23，34，13，24，14（st的意思是xs -> xt）。这里定义了三个变量来表示cell，分别是s, j, t。我简单概括下就是st = sj + (j+1)t，13 = 11 + 23 = 12 + 33 = 13 + 43, 因为43不存在，所以13涉及的字符对有(11, 23) 和 (12, 33)。
因此，可以把11和23对应的字符联系起来，在语法中寻找对应的rule，如果有对应的A存在，就把A写入13那个位置；如果有多个，逗号隔开，有几个写几个；如果没有，就写空集的符号。每一个位置都进行类似的推理，耐心足够就可以推出来的。填完全部的空，再从上到下画出parse tree就可以啦！
一些小技巧：寻找sj和(j+1)t的时候，可以先确定两边的s和t，中间的数字依次递增，直到大于两边的数字。比如👇
</br>

1.......3 -> 11+23 -> 12+33 ->13+43 (43不存在，舍弃并停止)

额外的嘱咐：CYK算法要求使用的grammar rule必须遵守CNF范式，因为这个范式保证了其对应的parsing tree是二叉树。