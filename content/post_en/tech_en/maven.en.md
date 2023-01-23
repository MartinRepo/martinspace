---
title: "Download APache Maven on MacOS"
date: 2023-01-19T00:15:03Z
lastmod: 2023-01-18T08:34:35Z
draft: false
author: ["Martin"]
tags: 
- Apache
description: ""
weight: 1 # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
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
I finally got maven installed, and the steps were generally easy, but I stepped in a few holes, I'll record them.

# Download APache Maven 

Website📡: [Apache-Maven](https://maven.apache.org/download.cgi)

Choose Binary zip archive and download it.

# Unzip the zip archive
I unzip it into /Libaray on my computer. 

# Configuration
``` bash
vi .bash_profile
```
Add 2 lines into this profile
```bash
export M2_HOME=/Library/apache-maven-3.8.7 // Or you can choose your own path and folder
export PATH=$PATH:$M2_HOME/bin
```
Then, type ```:wq```, save and quit vim.

# Check if it is successful
```bash
(base) ******** ~ % mvn -verison

//If terminal output like this, congratulations!

Apache Maven 3.8.7 (b89d5959fcde851dcb1c8946a785a163f14e1e29)
Maven home: /Library/apache-maven-3.8.7
Java version: 1.8.0_301, vendor: Oracle Corporation, runtime: /Library/Java/JavaVirtualMachines/jdk1.8.0_301.jdk/Contents/Home/jre
Default locale: en_GB, platform encoding: UTF-8
```

# Some problem
Sometimes, it reports error that it could not find JAVAHOME. It is probably that the JAVA_HOME in the computer is wrong. 

Type command below to check jdk version

```bash
where java
```
Terminal would output a path if you do have java on the computer, then copy this command and type command below
```bash
vi .bash_profile
```
Replace the path in JAVA_HOME with your copies, then ```:wq```, finally
```bash
source .bash_profile

mvn -version
```
