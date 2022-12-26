---
title: "重置服务器系统后，ssh连接失败"
date: 2022-12-06T22:34:10Z
draft: false
author: ["Martin"]
# categories: 
# - 分类1
# - 分类2
tags: 
- 服务器
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
重置服务器系统后。当使用远程ssh连接后，会显示连接失败。
</br>这里直接给出解决办法(仅以macOS为例):
1. 打开终端
2. 输入
```
vim ~/.ssh/known_hosts
```
3. vim会打开该文件，向下翻，找到服务器对应的IP
4. 按下```v```进入```visual```模式，使用方向键选择要删掉的内容（服务器IP对应的内容都要删掉）, 按下```d```
5. 或者，按下```i```进入```insert```模式，一个一个删除
6. 按下```esc```键，输入:```wq```+回车，任务完成
切记：一定要在英文输入法情况下按```esc```切换状态，中文输入模式下按```esc```不管用的！！！