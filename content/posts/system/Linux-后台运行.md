---
title: "Linux 后台运行"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T10:55:04+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
---
<!--more-->

# linux后台执行

跑一些程序时退出shell程序就终止了,这时就要使用以下命令:

linux 中 0 1 2文件描述符

| 名称 | 代码 | 操作符 | Linux 下文件描述符（Debian 为例) |
| -- | -- | -- | -- |
|标准输入(stdin) | 0 | < 或 << | /dev/stdin -> /proc/self/fd/0 -> /dev/pts/0 |
| 标准输出(stdout) | 1 | >, >>, 1> 或 1>> | /dev/stdout -> /proc/self/fd/1 -> /dev/pts/0 |
| 标准错误输出(stderr) | 2 | 2> 或 2>> | /dev/stderr -> /proc/self/fd/2 -> /dev/pts/0 |

## nohup

> 最后退出shell务必使用 `exit` 或者 ,<kbd>ctrl</kbd> + <kbd>d</kbd> 退出，不然可能造成程序退出  
> nohup( no hang up )

```bash
nohup 你要执行的命令 &
# 后台运行,默认在该程序目录生成nohup.out文件记录输出

nohup 你要执行的命令 &>log &
nohup 你要执行的命令 >log 2>&1 &
# 标准输出和错误输出到log并后台运行
```

## bg

1. 前台在跑程序时使用 <kbd>ctrl</kbd> + <kbd>z</kbd> 挂起进程以便执行命令

2. 这时使用 `bg 程序uid` 即可在后台继续运行

### 查看后台进程信息

```bash
jobs -l

# 查看后台运行的进程,可获得进程uid(jobs命令只是对当前终端生效)

ps -ef |grep uid或者进程名
ps -aux |grep uid或者进程名
# ps+grep获得后台进程信息

ps aux | grep command | grep -v grep | awk '{print $1}' | xargs kill -9 
# 直接通过command获取进程id并直接kill掉
```

### 切换至前台

```bash
fg 进程uid

fg %uid
# 将后台进程切换值前台
```

### 关闭该后台进程

```bash
kill 进程uid
```

### screen

| 命令 | 含义 | 快捷键 |
| -- | -- | -- |
| screen | 新建会话 |
| screen -S name | 新建会话并命名 |
| &nbsp; |
| &nbsp; | 离开会话 | <kbd>ctrl</kbd> + <kbd>a</kbd> + <kbd>d</kbd> |
| screen -ls | 查看所有会话 |
| screen -r name | 恢复会话 |



### tmux

```bash
# 创建tmux会话
tmux
tmux new -s <session-name>

# 分离会话
tmux detach

# 查看会话
tmux ls

# 接入会话
tmux attach -t 0

# 关闭会话
tmux kill-session -t 0

# 切换会话
tmux switch -t 0

# 重命名会话
tmux rename-session -t 0 <new-name>
```

快捷键

| 快捷键 | 功能 |
| -- | -- |
| <kbd>ctrl</kbd> + <bkd>b</bkd> + <kbd>d</kbd> | 分离会话 |
| <kbd>ctrl</kbd> + <bkd>b</bkd> + <kbd>s</kbd> | 列出会话 |
| <kbd>ctrl</kbd> + <bkd>b</bkd> + <kbd>$</kbd> | 重命名会话 |
| <kbd>ctrl</kbd> + <bkd>b</bkd> + <kbd>？</kbd> | 帮助信息 |

### 参考链接

+ [nohup和&后台运行，进程查看及终止](https://www.cnblogs.com/baby123/p/6477429.html)

+ [beego如何在Linux系统后台运行以及调回前台运行 nohup bg fg 命令的使用](https://blog.csdn.net/superwebmaster/article/details/80661162)

+ [linux nohup, jobs, fg, tail指令 指令前后台切换](https://www.cnblogs.com/wlc297984368/p/7655398.html)

+ [linux后台运行的几种方式](https://www.cnblogs.com/zsql/p/10827587.html)

