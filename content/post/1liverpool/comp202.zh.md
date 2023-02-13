---
title: "算法"
date: 2023-02-05T08:42:27Z
draft: false
author: ["Martin"]
tags: 
- Algorithm
description: ""
weight: 1 # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
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
# 时间复杂度和online algorithm (W1)
在线算法指的是，算法必须在输入数据不是完全可知的情况下，完成相应的计算并输出计算结果。

与之对应的是离线算法，它充分利用了输入数据之间完整的关联特性，即算法运行前所有输入数据均是已知的。

竞争分析针对的是在线算法，已知一个在线算法A，S是问题的一个变量输入序列，用cost(A, S)记录算法A应对S所产生的成本，用cost(OPT, S)记录最优离线算法应对S所产生的费用。若对于任意S都有```cost(A, S)<a*cost(OPT, S)```，则A是一个a-竞争算法。
 
# BST和其他搜索树 (W2)

## 链表
双向链表，如下图所示，每个节点都有一个前继(prev)和一个后驱(next)。
![linkedlist](/img/linkedlist.jpg)

双向链表的几个常用方法
```java
replaceElement(p,e) // p - position, e - element.
swapElements(p,q) // p,q - positions.
insertFirst(e) // e - element.
insertLast(e) // e - element.
insertBefore(p,e) // p - position, e - element.
insertAfter(p,e) // p - position, e - element.
remove(p) // p - position.
```
介绍其中一个方法：insertBefore()

技巧：要确保每个节点的前后两个指针都有连接，如上图所示。
```java
    s.prev = p;          /* 把 p 赋值给 s 的前驱 */
    s.next = p.next;     /* 把 p->next 赋值给 s 的后继 */
    (p.next).prev = s;    /* 把 s 赋值给 p->next 的前驱 */
    p.next = s;           /* 把 s 赋值给 p 的后继 */
```
List更新的复杂度分析（remove和insert）
- 如果元素p的位置已知，则复杂度为O(1)
- 如果只知道list的头，则复杂度为O(p)，因为需要遍历list来找到p

## 二分查找（BST)
一个有序数组通常称为lookup table。

- 输入一个有序数组
- 输出要查找的值及其对应的key
```java
BINARYSEARCH(S,k ,low ,high)
if low>high
    return no_such_key
else 
    mid = Math.floor((low+high)/2)
    if k = key(mid)
        return elem(mid)
    else if k<key(mid)
        return BINARYSEARCH(S, k, low, mid-1)
    else 
        return BINARYSEARCH(S, k, mid+1, high)
```
- key (i): the key at index i
- elem(i): the element at index i

lookup table 和 linked list比较
|Method|LinkedList|lookup table|
|------|----------|------------|
|查找元素|O(n)|O(logn)|
|插入元素(已知位置)|O(1)|O(n)|
|移除元素|O(n)|O(n)|
|ClosestKeyBefore|O(n)|O(logn)|

> 有没有一种数据结构可以既保证查找的效率又保证插入的效率？（综合lookup和linkedlist的优点）
>--- BST maybe possible.

- 二叉树的节点深度：节点的祖先的数量（排除节点自己）
- 二叉树的高度=该树最大的节点深度

二叉树的遍历方法
- 前序遍历(pre-order)
- 中序遍历(in-order)
- 后序遍历(post-order)

所有的BST的操作的时间复杂度都是O(h)，h表示树的高度。如果情况糟糕的话，h很有可能等于n（对于一个degenerate tree来说）。
如果BST不平衡的话，它最差的搜索时间可能是O(n)，这就失去了它的优点。

因此我们衍生出一种具有高度平衡的性质的树——AVL树

## AVL树
AVL树的性质：对于树T中的每个内部节点v，v的子节点之间的高度差最多是1。

存储n个节点的AVL树的高度是O(logn)

证明：一个高度为h的AVL树，令这棵树的内部节点最少有```n_h```个。最坏情况下，左树的高度为h-1，右树高度为h-2，且两颗子树都是AVL树。

所以```n_h = n_h-1 + n_h-2 + 1```，意思是整个树的节点是由左右两颗子树的节点加上根节点，因为```n_h-1>n_h-2```，所以```n_h>2*n_h-2 -> n_h>2^(h/2-1)```

- AVL树中的搜索操作，时间复杂度为O(logn)
- AVL中的插入和移除操作要小心（要使用rotation来保证height balance）

旋转这个操作太麻烦，在b站找到一个宝藏嚣张教程，记录一下。

宗旨：自下而上地找最小的一颗不平衡子树，如果向上找的节点太多，就选择离根节点最近的三个节点（包括根节点），将三个节点拿出来树状排序，插入原来的位置。剩下的元素根据二叉树的规则重新插入。

在下面这个AVL树中插入90
{{<mermaid>}}
flowchart TD
id1(50)-->id2(26)-->id3(21)
id2-->id4(30)
id1-->id5(66)-->id6(60)
id5-->id7(68)-->id8(67)
id7-->id9(70)
{{</mermaid>}}

插入后效果如下
{{<mermaid>}}
flowchart TD
id1(50)-->id2(26)-->id3(21)
id2-->id4(30)
id1-->id5(66)-->id6(60)
id5-->id7(68)-->id8(67)
id7-->id9(70)-->id10(90)
{{</mermaid>}}
很明显，这不是一颗AVL树。因此，从底部开始向上寻找最小的不平衡子树的根节点，发现是66。路径是90-->60，找到这条路径上距离66最近的三个节点（包括66本身），找到了66，68，70三个数。
对这三个数进行重新排列，如下图所示
{{<mermaid>}}
flowchart TD
id1(68)-->id2(70)
id1-->id3(66)
{{</mermaid>}}
排列后插入原来的位置，剩下的元素根据二叉树的规则重新插入，结果如下
{{<mermaid>}}
flowchart TD
id1(50)-->id2(26)-->id3(21)
id2-->id4(30)
id1-->id5(68)-->id6(66)
id5-->id7(70)-->id8(90)
id6-->id9(60)
id6-->id10(67)
{{</mermaid>}}
整套操作行云流水，十分清爽，爱了。删除也是同样的操作，删除后不平衡，找到最小不平衡树，然后重新排列。在AVL树中，所有的操作都可以在O(logn)内解决

## (2,4)树
(2,4)树的定义是这棵树的子节点，最少有两个，最多有四个。每个内部节点都包含1-3个键，这些键定义了存储在子树中的键的范围。这样的键要保证，比它最左边的子树中最大的键大，比最右边的子树中最小的键小。

(2,4)树的所有叶子节点都具备相同的深度。

- n个元素存储在(2,4)树中，其高度为O(logn)
- 拆分，转移和融合操作花费O(1)的时间
- 搜索，插入和删除元素需要访问树中O(logn)个节点。