---
title: "Linux Iptables"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:07:03+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

<!--markdown-->## 防火墙

+ 主机防火墙

+ 网络防火墙

## 主机防火墙(linux)

1. 数据传输流程

![linux数据通道][3]

2. iptables

3. TCP协议三次握手,四次挥手

```

netstat -tnlpa | grep tcp | awk '{print $6}' | sort | uniq -c #判断是否受SYN攻击

```

> 四层模型(数据链路层mac,网络层ip,传输层TCP,应用层)都可应用防护墙

### iptables

>内核防护墙netfilter,iptables是管控netfilter的工具

#### iptables结构

+ tables(表)

+ chains(链)

+ rules(规则)

> iptables四张内建表,优先级从高到低,内核2.6.34后NAT表支持操作INPUT链

1. `raw`: 高级功能,如:网址过滤,`PREROUTING/OUTPUT`两链

2. `mangle`: 数据包修改(QOS),含有所有链

3. `nat`: 地址转换,网关路由,含有:`PREROUTING/POSTROUTING/OUTPUT`三链

4. `filter`: 数据包包过滤,防火墙规则,含有:`OUTPUT/FORWARD/INPUT`三链

![iptables结构图][4]

#### chains(链)

1. `PREROUTING`

2. `INPUT`:保护本机

3. `FORWARD`:保护后端主机(转发给数据包的主机)

4. `OUTPUT`:管制本机

5. `POSTROUTING`

> `ip_forword`,linux自带数据转发,`默认关闭`;`FORWARD`管控ip_forword.

#### iptables 参数

> iptables [-t TABLE] COMMAND CHAIN [ -j (ACCEPT/REJECT/DROP;允许/拒绝/丢弃) ]

| 参数 | 解析 |

|---|---|

| `-P` | 设置默认策略 |

| `-X/F/Z` | 清空自定义规则/规则/规则计时器 |

| `-L` | 查看规则链 |

| `-A` | 在规则链尾加新规 |

| `-I` | 在规则链头加新规 |

| `-D` | 删除某规则 |

| `-s` | 匹配来源地址IP/MASK，加叹号"!"表示除这个IP外。 |

| `-d` | 匹配目标地址 |

| `-i` | 匹配网卡名,流入数据 |

| `-o` | 同上,流出 |

| `-p` | 隐式扩展,协议:tcp,udp,icmp |

| `--dport` | 目标端口号 |

| `--sport` | 来源端口 |

| `-m` | 隐式扩展 |

| `-nvL` | 统计数据,规则列表,流量统计数据 |

| `-save` | 导出filter表规则

```

sudo service iptables save #保存规则到/etc/sysconfig/iptables中

sudo iptables-save > 指定保存位置

sudo iptables-restore <规则位置 #恢复规则

```

### 参考链接

+ [知识盒子-防火墙配置之分类及工作原理][1]

+ [防火墙和iptables(详细)][2]

  [1]:https://zhishihezi.net/

  [2]:https://www.cnblogs.com/f-ck-need-u/p/7397146.html

  [3]:https://images2017.cnblogs.com/blog/733013/201708/733013-20170819154817271-751283085.png

  [4]:https://img2018.cnblogs.com/blog/733013/201903/733013-20190302203624112-505039185.png
