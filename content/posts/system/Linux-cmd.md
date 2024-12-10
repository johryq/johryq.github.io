---
title: "Linux Cmd"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T10:14:24+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
---
<!--more-->

# Linux

## 常用指令及部分参数,更多详细信息需要查看[最下面帮助信息命令](#帮助)

### linux网络

| 命令 | 参数 | 详细信息 |
|---|---|---|
| ifconfig | &nbsp; | 查看/临时设置 IP 地址 |
| traceroute | &nbsp; | 查看一个数据包到网站的所有路由 |
| route | -n | 路由状态 |
|  wget | &nbsp; | 下载网页(-c断点续传) |
| lsof | &nbsp | 统打开的文件 |
| &nbsp; | -i:端口 | 查看占用这个端口的信息 |
| &nbsp; | -u 用户 | 查看该用户打开的文件 |
| &nbsp; | -c 进程名 | 该进程打开的文件 |
| &nbsp; | -p uid | 同上 |
| &nbsp; | +d 目录 | 查询指定目录下被进程开启的文件(+D 递归) |
| netstat | &nbsp; | 查看网络相关信息 |
| &nbsp; | -t | TCP协议 |
| &nbsp; | -u | UDP协议 |
| &nbsp; | -l | 监听 |
| &nbsp; | -r | 路由 |
| &nbsp; | -n | IP地址与端口号 |
| &nbsp; | -tlun | 查看本机监听端口 |
| &nbsp; | -an | 查看本机所有网络连接 |
| &nbsp; | -rn | 查看本机路由表 |

### 关机,重启

| 命令 | 参数 | 详细信息 |
|---|---|---|
| halt | &nbsp; | 关机 |
| poweroff | &nbsp; | &nbsp; |
| init 0 | &nbsp; | &nbsp; |
| shutdown | -chr | 定时执行 |
| &nbsp; | -h | 关机(now 立即关机) |
| &nbsp; | -r | 重启 |
| &nbsp; | -c | 取消上一个关机指令 |
| reboot | &nbsp; | 重启 |
| init 6 | &nbsp; | &nbsp; |
| runlevel | &nbsp; | 查询系统运行级别(0-6) |
| &nbsp; | 0 | 关机 |
| &nbsp; | 1 | 单用户 |
| &nbsp; | 2 | 不完全多用户,不包含NFS服务 |
| &nbsp; | 3 | 完全多用户 |
| &nbsp; | 4 | 未分配 |
| &nbsp; | 5 | 图形界面 |
| &nbsp; | 6 | 重启 |

### 文件管理

| 命令 | 参数 | 详细信息 |
|---|---|---|
| ls | &nbsp; | 显示目录信息 |
| &nbsp; | -a | 显示所有文件|
| &nbsp; | -l | 详细信息|
| &nbsp; | -d | 目录属性|
| &nbsp; | -i | 系统索引文件id|
| &nbsp; | -h | 可读显示文件大小 (通用命令,多命令可用) |
| ln | &nbsp; | 硬链接 |
| &nbsp; | -s | 软链接 |
| rm | &nbsp; | 删除文件或目录|
| &nbsp; | -r | 删除目录 |
| &nbsp; | -f | 强制执行 |
| cp | &nbsp; | 复制 |
| &nbsp; | -r | 复制目录 |
| &nbsp; | -p | 保留文件属性 |
| mkdir | &nbsp; | 创建目录 |
| &nbsp; | -p | 递归创建 |
| pwd | &nbsp; | 显示当前路径|
| &nbsp; | -P | 显示绝对路径 |
| rmdir | &nbsp; | 删除空目录 |
| mv | &nbsp; | 移动或重命名 |

### 文档编辑

| 命令 | 参数 | 详细信息 |
|---|---|---|
| cat | -l | 显示文件内容 |
| &nbsp; | -n | 带有行号 |
| echo | &nbsp; | 输出字符串或提取变量值 |
| head | &nbsp; | 查看文件开始内容 |
| tail | &nbsp; | 查看文件尾部内容 (默认10行) |
| &nbsp; | -n | 指定行数 |

### 用户管理

| 命令 | 参数 | 详细信息 |
|---|---|---|
| useradd | &nbsp; | 新建用户与用户目录 (无密码) |
| adduser | &nbsp; | 新建用户 |
| passwd | &nbsp; | 更改用户密码|
| deluser | &nbsp; | 删除用户|
| &nbsp; | -r | 删除用户及用户目录 |
| who | &nbsp; | 查看用户信息 (简略) |
| w | &nbsp; | 查看用户信息 (详细点) |
| uptimme | &nbsp; | 登录信息 |
| logout | &nbsp; | 退出登录 |

### 压缩

| 命令 | 参数 | 详细信息 |
|---|---|---|
| gzip | `.gz` | 只能压缩文件,不保留原文件 |
| &nbsp; | -d | 解压 |
| gunzip | &nbsp; | 解压 |
| tar | `-zcvf` 或 `-zxvf`  | 常见linux打包 (f最后,tar.gz加x参数) |
| &nbsp; | -c | 打包 |
| &nbsp; | -x | 解包 |
| &nbsp; | -v | 显示详细信息 |
| &nbsp; | -f | 指定文件 |
| &nbsp; | -z | 打包同时压缩 (解压) |
| zip | `.zip` | 压缩文件或目录 |
| &nbsp; | -r | 压缩目录 |
| unzip | &nbsp; | 解压 |
| bzip2 | `.bz2` | zip升级版,压缩率更高 |
| &nbsp; | -k | 保留原文件 |

### 帮助

| 命令 | 参数 | 详细信息 |
|---|---|---|
| man | &nbsp; | 获取帮助信息 (manual) |
| &nbsp; | <kbd>f</kbd>或<kbd>space</kbd>| 翻页|
| &nbsp; | <kbd>enter</kbd> | 换行|
| &nbsp; | <kbd>q</kbd> | 退出 |
| whatis | &nbsp; | 命令简短信息 |
| apropos | &nbsp; | 配置文件简短信息 |
| info | &nbsp; | &nbsp; |
| help | &nbsp; | &nbsp; |

### 参考网址

+ [https://www.linuxcool.com/](https://www.linuxcool.com/)

+ [useradd与adduser](https://www.cnblogs.com/whitehorse/p/5847278.html)

+ [史上最牛的Linux视频教程—兄弟连](https://www.bilibili.com/video/BV1mW411i7Qf)
