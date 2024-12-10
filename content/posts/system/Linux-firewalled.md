---
title: "Linux Firewalled"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:06:42+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

<!--markdown-->> `friewalld`同样是通过内核`netfilter`模块来管理数据包

## `firewalld`与`iptables`相比的优缺点

**优点**

+ 动态修改单条规则

+ 简单

**缺点**

+ 默认请求全部拒绝,需要自行放行

## `firewadlld`区域管理

**包含区域**

+ 阻塞区域(block):默认配置

+ 工作区域(work)

+ 家庭区域(home)

+ 公共区域(public)

+ 隔离区域(DMZ)

+ 信任区域(trusted)

+ 丢弃区域(drop)

+ 内部区域(internal)

+ 外部区域(external)

> 默认配置文件位置:`/usr/lib/firewalld/zones/`

## 配置方法/工具

+ `firewall-config` #图形化配置工具

+ `firewall-cmd` #命令行

+ 配置文件,上面那个路径的相关文件中

### 安装方法

```

sudo yum install firewalld 

```

### `firewall-cmd`命令参数

> 参数后跟`=`;比如:`--zone=public`

| 参数 | 解析 |

|---|---|

| *`--zone`* | 选择管理区域 |

| `--list-ports` | 列出已打开端口 |

| *`--add-port`* | 添加端口,如:`--add-port=3389/tcp` |

| *`--remove-port`* | 关闭端口,同上 |

| *`--permanent`* | 永久生效 |

| *`--reload`* | 重新加载配置,使修改生效 |

## 参考资料

+ [细说firewalld和iptables][1]

+ [Linux firewalld 防火墙使用][2]

  [1]:https://www.cnblogs.com/grimm/p/10345693.html

  [2]:https://blog.csdn.net/wangmx1993328/article/details/80738012
