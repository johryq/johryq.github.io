---
title: "Linux Ctrl+"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:06:09+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

<!--markdown-->linux后台运行命令时使用到了这个,做个记录:

+ ctrl-c：发送 SIGINT 信号给前台进程组中的所有进程。常用于终止正在运行的程序；

+ ctrl-z：发送 SIGTSTP信号给前台进程组中的所有进程，常用于挂起一个进程；

+ ctrl-d：不是发送信号，而是表示一个特殊的二进制值，表示 EOF，作用相当于在终端中输入exit后回车；

+ ctrl-\：发送 SIGQUIT 信号给前台进程组中的所有进程，终止前台进程并生成 core 文件；

+ ctrl-s：中断控制台输出；

+ ctrl-q：恢复控制台输出；

+ ctrl-l：清屏

>其实，上述所有的控制字符都是可以通过stty命令更改的，可在终端中输入命令”stty -a”查看终端配置。

#### 参考链接

+ [linux下如何在shell中结束进程（ctrl+c\ctrl+z\ctrl+d\ctrl+\的用法)](https://blog.csdn.net/LEON1741/article/details/78140639)
