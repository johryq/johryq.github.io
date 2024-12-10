---
title: "Nmap"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:14:28+08:00
draft: false
keywords: []
description: ""
tags: []
categories: ['software']
author: "2332334"

---
<!--more-->

# NMAP

## NMAP的基本使用

### 安装

+ centos

``` bash

yum install nmap -y

```

+ ubuntu

> 将 `nmap` 的 rpm 包转换为 deb

1. `sudo apt-get install alien`

2. 下载 `rpm` 包,地址为: https://nmap.org/download.html

3. sudo alien [你下载的 `rmp` 包]

4. sudo dpkg --install [生成的 `deb` 包]

> 也可以直接 `apt install nmap` 但是不是最新的版本

+ [windows下载](https://nmap.org/download.html#purpleheader)

### 部分命令

> SYN ACK为TCP三次握手时数据包;FIN ACK四次挥手断开TCP链接

| 参数 | 说明 |

|---|---|

| **目标选择** | &nbsp; |

| `-iL` | (inputfilename)从文件字典获取 |

| `-iR` | (hostnum)随机选择目标 |

| `--exckude` | 排除主机使用 `,` 分隔 |

| **主机发现(ping)** | &nbsp; |

| `sL` | 列表扫描,扫域名? |

| `sP` | ping扫描 |

| `-P0` | 无ping,确定正在运行机器 |

| `-PS [Portlist](TCP SYN Ping` | 扫描端口,确认主机存活 `,`分割端口列表 |

| `-PA [Portlist](TCP ACK ping` | 同上,请求报文不同 |

| `-PU [Portlist](UDP Ping)` | 同上 |

| `-PE;-PP;-PM(ICMP Ping Type)` | 普通ping报文,时间戳响应(ICMP代码14)或者地址掩码响应(代码18) |

| `PR(ARP ping)` | 多用局域网扫描,比IP扫描快 |

| `-n` | 不用域名解析 |

| `-R` | 为所有目标域名解析 |

| `--system-dns` | 使用系统域名解析,慢,不推荐,多用于IPV6 |

| **端口扫描** | 六种状态 |

| `open` | 开放端口 |

| `closed` | 关闭端口,还是可访问,指不定过会儿就开了 |

| `filtered` | 被过滤的,防火强屏蔽 |

| `unfitered` | 未过滤,不确定是否开放,使用ACK分类;窗口,SYN,FIN确定是否开启 |

| `open/filtered` | 开放或未被过滤,无法确定开放或被过滤,如:开放端口不过滤 |

| `closed/filtered` | 关闭或被过滤,只出现IPID ldle扫描中 |

| `-sS` | TCP/SYN |

| `-sT` | TCP |

| `-sU` | UDP,`--host-timeout`跳过慢速主机 |

| `-sN;sF;sX` | TCP Null,FIN,Xmas 设置的标志位 |

| `-sA` | TCP ACK |

| `-sW` | TCP窗口 |

| `-sM` | TCP Maimon |

| `--scanflags` | 定制TCP扫描 |

| `-sI <zombie host[:probeport]>` | Idlescan,TCP端口盲扫(隐蔽) |

| `-sO` | IP协议扫描 |

| `-b <ftp relay host> | FTP弹射扫描,参数格式是 <username>:<password>@<server>:<port> |

| **端口说明** | 默认1-1024或者nmap-services中的端口扫描 |

| `-p` | 指定端口 |

| `-F` | 快速扫描 |

| `-r` | 不要按随机顺序扫描端口 |

| **服务器与版本探测** | &nbsp; |

| `-sV` | 版本探测,`-A`操作系统与版本探测 |

| `--allports` | 不为版本探测排除任何端口 |

| `--version-intensity` <intensity>| `-sV`设置版本扫描强度 |

| `--version-light` | 轻量模式 |

| `--version-all` | 尝试每个探测 |

| `--version-trace` | (跟踪版本扫描活动) |

| `-sR` | RPC |

| **输出** | &nbsp; |

| `-oN` | 标准输出至文件 |

| `-oX` | xml |

| `-oS` | 交互工具输出 |

| `-oG` | Grep |

| `-oA` | 输出所有格式 |

| `-v` | 提高输出信息详细度 |

| `--resume` | 继续中断的扫描 |

| `--append-output` | 添加写入保存文件 |

碎碎念
> 记来干啥,意义不大啊,记几个常用的就好,具体看文档!  
> 嗯,还是简单记一下

``` bash
#扫描所有TCP端口
nmap -v 域名/IP 

#SYN该主机所在C类网段255台2主机,确定操作系统,需要根权限
nmap -sS -O 域名/ip/24 

#扫描网段主机及端口开放情况,不域名解析
nmap -Pn [IP地址] 

#随机浏览网页
nmap -sS -PS80 -iR 0 -p 80 
```

### 记录来源

+ [安全运维 - 基础安全之模拟内网安全扫描](https://zhishihezi.net/)
+ [Nmap中文手册][1]

  [1]:http://www.nmap.com.cn/doc/manual.shtm
