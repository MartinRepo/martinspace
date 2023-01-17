---
title: "代码上传至github"
date: 2022-12-16T16:04:33Z
draft: false
author: ["Martin"]
categories: 
- 分类1
- 分类2
tags: 
- git
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
1. 先在github建立一个远程仓库，可以全部是默认设置

2. 全局声明git的用户认证信息
```
git config --global user.name "name"

git config --global user.email "email@gmail.com"
```
其中name写自己的名字，email@gmail.com写自己的email

3. 初始化本地git仓库
```
cd 本地项目根目录
git init
```
4. 将项目文件添加到git仓库中
```
git add .
```
 .意思是将当前文件夹下的文件全部添加到仓库中，如果想添加某一个问价，将 .替换成对应的文件名就可以了
5. 将文件commit到仓库
```
git commit -m "提交的消息内容"
```
6. 将本地仓库关联到github
```
git remote add origin 自己仓库的url地址
```
7. 上传本地仓库代码至github远程仓库
```
git push -u origin +main
git pull
git push origin main
```
由于新项目github的默认分支从master变成了main，所以之前的博客中提到的master对于新项目来说都会报错，用上述指令就可以成功上传啦（记得敲完一行执行一行）

上传成功之后可以回到github查看自己的仓库是否多了一些文件，记得刷新！
之后每次代码更新后只要执行第七步就可以啦。