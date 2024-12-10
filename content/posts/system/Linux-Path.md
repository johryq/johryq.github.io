---
title: "Linux Path"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T10:56:42+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
---
<!--more-->

# linux目录结构

linux 是树状结构目录

![目录](../../img/catalog.jpg)

---

| 目录  | 详解                                    |
| ----- | --------------------------------------- |
| /bin  | Binary(二进制)缩写,存放最经常使用的命令 |
| /boot | 启动Linux核心文件，包括连接文件及镜像   |
|/dev       |Device(设备)缩写，Linux外设(Linux访问外设和访问文件是相同的)
|/home      |用户主目录(一个用户一个目录，一般用户名为文件名)
|/lib       |系统基本动态共享库(类似Win的DLL)，几乎所有程序都会用到
|/lost+found|这个目录一般是空的,系统非法开机后，这里才存放目录
|/media     |Linux自动识别设备(U盘，光驱等)，识别后Linux会将识别的设备挂载到这个目录
|/opt       |主机额外安装软件摆放的目录，默认空
|/proc      |虚拟目录，系统内存映射，可直接通过访问目录获取，修改系统信息
|/root      |系统管理目录，超级用户目录
|/sbin      |s(Super User),root使用的系统管理程序
|/selinux   |Redhat/CentOS特有目录,Selinux是安全机制(类似Win防火墙)
|/srv       |服务启动后需提取的数据
|/sys       |linux2.6内核最大变化,2.6新出现文件系统sysfs所在目录（有针对进程信息的proc文件系统，设备的devfs文件系统，伪终端devpfs文件系统这3个文件系统）
|/tmp       |存放临时文件
|/usr       |重要目录，用户很多程序和文件所在(类似Win的program files)
|/usr/bin   |系统用户使用的应用程序
|/usr/sbin  |超级用户使用的较高级管理程序和系统守护程序
|/usr/src   |内核源代码默认目录
|/var       |存放不断扩充的，经常被修改的文件(如日志文件)
|/run       |临时目录，系统启动以来的信息，系统重启后该目录文件删除或清除(如有/var/run，应该让它指向run)
