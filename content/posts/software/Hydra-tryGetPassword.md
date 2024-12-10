---
title: "Hydra TryGetPassword"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T10:12:16+08:00
draft: false
keywords: []
description: ""
tags: []
categories: ['software']
author: "2332334"

---
<!--more-->

# Hydra

## 简介

Hydra是著名黑客组织thc的一款开源的暴力密码破解工具，支持多种网络服务的非常快速的网络登陆破解工具，是暴力破解中的神器。

## 基本使用

### 下载地址

+ Github-Linux: https://github.com/vanhauser-thc/thc-hydra

+ Github-Windows: http://github.com/maaaaz/thc-hydra-windows

### 安装

``` bash
apt install hydra
```

> 下载可能不是最新,推荐github下载源码后执行

``` bash
./configure

make

make install
```

然后即可使用.

> debian 可选库:

``` bash
apt-get install libssl-dev libssh-dev libidn11-dev libpcre3-dev \

                 libgtk2.0-dev libmysqlclient-dev libpq-dev libsvn-dev \

                 firebird-dev libmemcached-dev libgpg-error-dev \

                 libgcrypt11-dev libgcrypt20-dev

```

### 使用

> `hydra [命令行选项] [-s Port] TARGET(目标) PROTOCOL(协议) [可选参数]`

+ 命令行选项包括:

| 参数 | 说明 |

|---|---|

| `-R` | 继续上一次破解 |

| `-S` | 使用SSL |

| `-s` | 指定非默认端口 |

| `-l` | 指定破解用户名 |

| `-L` | 指定用户名字典 |

| `-p` | 指定密码破解 |

| `-P` | 指定密码字典 |

| `-e [ns]` | 可选选项，n:空密码试探，s:使用指定用户和密码试探 |

| `-C` | -L/-P选项字典 `登录名:密码` |

| `-M` | 目标文件,一行一个 |

| `-o` | 指定结果输出文件 |

| `-f` | 使用 `-M` 后,只要破解成功一个即终止 |

| `-t` | 线程数,默认16|

| `-w` | 最大超时时间,默认30s |

| `-v/-V` | 详细过程 |

| `server` | 指定服务名,支持的服务和协议:telnet ftp pop3 http[s]-{head/get} http-{get/post}等等 |

+ 选择目标，可以使用三个选项来指定要攻击的目标：

  1. 命令行上的单个目标：只需将IP或DNS地址放入

  2. 命令行上的网络范围：CIDR规范，例如“ 192.168.0.0/24”

  3. 文本文件中的主机列表：每个条目一行

+ 选择协议

+ 可选参数,目标端口

### 示例

``` bash

hydra -l 用户名 -p 密码 IP ssh  #爆破ssh

hydra -L name.txt -P pwd.txt IP 协议

```

## 参考

+ [安全运维 - 基础安全之弱口令检测](https://zhishihezi.net/)

+ [Github-Readme](https://github.com/vanhauser-thc/thc-hydra/blob/master/README.md)
