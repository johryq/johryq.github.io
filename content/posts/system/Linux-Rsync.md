---
title: "Linux Rsync"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:31:08+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# Rsync

> remote sync (远程同步)
> 本地或与远程文件同步

## 安装

``` bash
# Debian
$ sudo apt-get install rsync

# Red Hat
$ sudo yum install rsync

# Arch Linux
$ sudo pacman -S rsync
```

## 使用

``` bash
# 测试基本同步
rsync -avn source/ destination 

# 排除文件
rsync -av --include="*.png" --exclude='*' source/ destination

# ssh
rsync -av -e ssh source/ user@remote_host:/destination

# ssh指示端口
rsync -av -e 'ssh -p 2345' source/ user@host:/des

# 增量备份
rsync -av --delete --link-dest /cpmpare/path source/ target/
```

> 增量备份:源目录与目标目录之前还有个基准目录,第一次备份全局备份之后,之后备份目标目录只会存储源目录比基准目录多的文件

## 参数

| 参数 | 解析 |
| -- | -- |
| r | 递归 |
| a | 保留源数据 |
| n | 测试同步,输出同步结果 |
| z | 同步时压缩数据 |
| e | 指定使用`ssh`传输数据 |
| i | 原目录与目标目录文件详细差异 |
| --delete | 完全同步源目录,删除目标目录比源目录多的文件 |
| --exclude | 排除文件或目录 |
| --include | 必须同步 |
| --progress | 参数表示显示进展 |
| --link-dest | 参数指定增量备份的基准目录 |

## 参考

+ [阮一峰--ssh教程-rsync](https://wangdoc.com/ssh/rsync.html)