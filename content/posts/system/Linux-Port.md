---
title: "Linux Port"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T10:15:41+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# lsof + netstat 端口信息查看

## lsof

列出打开文件（lists openfiles）

> `lsof -i:80`

![lsof -i:80](../../img/lsof.png)

输出相关信息解释如下:

| 参数 | 解释 |
|---|---|
| COMMAND | 进程名称 |
|  PID | 进程标识符 |
| USER | 进程所有者 |
| FD | 文件描述符,应用程序通过该描述符识别文件,cwd,txt等 |
| TYPE | 文件类型,DIR,REG等 |
| DEVICE | 指定磁盘名称 |
| SIZE | 文件大小 |
| MODE | 索引节点,文件再磁盘上的标识 |
| NAME | 打开文件的确切名称 |

---

> `lsof` 更多参数信息

| 命令参数 | 解析 |
| --- | --- |
| lsof -i:[端口] | 查看端口占用 |
| lsof [文件] | 显示打开文件的进程信息 |
| lsof -c [进程] | 显示进程现在打开的文件 |
| lsof -c -p [UID] | 列出该进程搜打开的文件 |
| lsof -g [GID] | 显示 [Group ID] 的进程情况 |
| lsof +d [目录] | 显示目录下被进程打开的文件 |
| lsof +D [目录] | 同上+搜索目录下的目录 |
| lsof -d [fd] | 显示该fd的进程 |
| lsof -i -U | 显示所有打开端口和UNIX domain 文件 |

---

### netstat

> `netstat -tunlp | grep 端口`

| 命令参数 | 解析 |
| --- | --- |
| -t | tcp相关 |
| -u | udp相关 |
| -n | 拒绝显示别名，能显示数字的全部转化为数字 |
| -l | 仅列出在Listen(监听)的服务状态 |
| -p | 显示建立相关链接的程序名 |

### 参考链接

+ [菜鸟教程](https://www.runoob.com/w3cnote/linux-check-port-usage.html)
