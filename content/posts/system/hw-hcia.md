---
title: "Hw Hcia"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-03T16:59:04+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# HCIA DataCom(华为数通)

## 网络基础

### 网络类型

+ 局域网(LAN)--local area network
+ 城域网(MAN)--metropolitan
+ 广域网(WAN)--wide

### 网络拓扑

> 网络种物理逻辑架构

形态

+ 星型
+ 总线型
+ 环型
+ 树型
+ 全网状
+ 部分网状

### 参考模型

+ OSI(ISO)
  + 应用层
  + 表示层
  + 会话层
  + 传输层
  + 网络层
  + 数据链路层
  + 物理层
+ TCP/IP标准模型
  + 应用层
  + 主机到主机层
  + 英特网层
  + 网络接入层
+ TCP&IP对等模型
  + 应用层
    + HTTP | FTP | DNS | Telnet | DHCP | SNMP | SMTP
  + 传输层
    + TCP | UDP | 2的16次方-1 65535端口
  + 网络层
    + IPV4 | IPV6 | ICMP(ping) | IGMP | IP
  + 数据链路层
    + PPPoE | MAC | Ethernet | PPP
  + 物理层

#### 传输层

TCP如何保证数据准确
三次握手
seq ack

窗口滑动机制
win

TCP关闭
四次挥手
fin

#### 网络层

路由 mac

ARP(address resolution protocol)协议

> 根据IP地址获取MAC地址
> 广播请求

1. Host1 查看ARP缓存
2. 无,ARP request
3. Host2 缓存APR
4. ARP reply
5. Host1 缓存ARP

## 华为VRP(Versatile Routing Plaform)

> 华为数通产品通用操作系统平台

### 文件系统

+ 系统文件
  + cc
+ 配置文件
  + cfg,zip,dat
+ 补丁文件
  + pat
+ PAF文件
  + bin

### 视图

用户界面:

console
vty(使用前需要配置)

+ 用户视图  return
+ 系统视图 - system-view
+ 接口视图 - interface GigbitEthenet 0/0/1
+ 协议视图 - Huawei-ospf-1

### 命令

#### undo

1. 恢复缺省
2. 禁用功能
3. 删除配置

#### 基本配置

| 命令 | 参数 |
| -- | -- |
| user privilege | 配置指定用户界面级别 |
| command-privilege level | 设置指定视图命令级别 |
| set authentication cipher password | 配置本地认证密码 |
| idle-timeout | 超时连接时间 |
| &nbsp; | &nbsp; |
| sysname | 设备名 |
| clock timezone | 设置本地市区 |
| clock datetime | 设置当前时间日期 |
| clock daylight-saving-time | 设置夏令时 |
| 系统信息 | &nbsp; |
| display device ? | 设备信息 |
| display esn | 21980106042SL4600115 设备唯一编号 |
| display version | 版本信息 |
| display power | 电源异常时,查看相关信息 |
| display power system | 功率信息 |
| display voltage { all | slotslot-id} | 单板电压 |
| display fan ? | 风扇 |
| display cpu-usage  | CPU |
| display cpu-usage configuration ? | 查看CPU占用率的配置信息 |
| display memory-usage ? | 内存 |

#### 目录操作

| 命令 | 参数 |
| -- | -- |
| pwd | 当前所在目录 |
| dir | ls |
| more | 查看文本内容 |
| cd | 切换 |
| mkdir | 新建目录 |
| rmdir | 删除目录 |
| copy | 复制 |
| move | 移动 |
| rename | 重名 |
| delete/unreserved  | 删除/永久删除文件 |
| undelete | 恢复删除文件 |
| reset recycle-bin | 彻底删除回收站中文件 |

#### 配置文件

> 用户视图

| 命令 | 参数 |
| -- | -- |
| display current-configuration | 显示当前配置文件 |
| display saved-configuration | 显示保存的配置文件 |
| save | 保存配置 |
| display startup | 查看当前启动配置文件 |
| starup saved-configuration | 配置系统下次启动时使用的配置文件 |
| compare configuration | 比较当前配置与下次启动配置文件 |
| reset saved-configuration | 清除下次启动时加载的配置文件 |
| display configuration candlidate | 当前未提交命令行信息(vrp5没有,v8的) |

#### 存储设备

| 命令 | 参数 |
| -- | -- |
| fdisk

## 网络层协议与IP编址

ICMP IPX IP

作用

1. 为网络层设备提供逻辑地址
2. 数据包寻址与转发

协议头
![ipv4_title](https://s2.loli.net/2024/12/10/adRpX6xZGnTUikf.png)

TTL(time to live) 0-255 8bit
> 防止环路

Protocol(协议号) 6/TCP 17/UDP 11/ICMP

### IPV4 32bit

A类地址
0.0.0.0 127.255.255.255.255

B类
128.0.0.0 191.255.255.255

C类
192.0.0.0 223.255.255.255

D类
224.0.0.0 239.255.255.255

E类
240.0.0.0 255.255.255.255

私网IP

A: 10.0.0.0 10.255.255.255  
B: 172.16.0.0 172.31.255.255  
C: 192.168.0.0 192.168.255.255

IPV6 128bit

### 子网划分(打脑壳)

### ICMP

internet control message protocol

IMCP重定向: 优化路由路径,实现更优路径
差错检测: ping
错误报告: tracert

## 以太网交换基础

局域网中通用,常见协议

以太网是建立在CSMA/CD(carrier sense multiple access/collision detection 载波监听多路访问/冲突检测)机制上的广播型网络

早期无交换机分割局域网,抢占式的,出现冲突域,CMSA/CD缓解冲突

> 交换机隔离冲突域 不能隔离广播域

以太网二层接口类型

1.Access: 一般链接主机与交换机  
2.Trunk: 一般连接交换机与交换机  
3.Hybrid: 可看作前面两个接口结合

### 以太网帧格式(数据帧)

+ Ethernet_Ⅱ
+ IEEE 802.3

![ethernet](https://s2.loli.net/2024/12/10/36s7oiKlJSjXWbC.png)

### mac地址 48bit

> ex:00-1E-10-DD-DD-02 001E-10DD-DD02

1. OUI(organizationally unique ldentifier) 厂商代码 24bit
2. 制造商分配 24bit

> 按目的mac地址区分:单播地址 广播地址 组播地址
> 以太网帧: 单播帧 广播帧 组播帧

未知单播帧

交换机转发行为

+ 泛洪
+ 转发
+ 丢弃

| arp -a | ARP缓存表 |
| display mac-address verbose | mac地址表 |

### 配置

``` bash
system-view
interface GigabitEthernet 0/0/1
undo negotiation auto
speed 1000
#接口速率
duplex full
#全双工

# 验证
sidplay interface GibabitEehernet 0/0/1
```

## VLAN原理与配置

> VLAN(virtual local area network) 虚拟局域网
> 划分广播域

Vlan Tag

Vlan帧
> 802.1Qtag

![vlan帧](https://s2.loli.net/2024/12/10/J39rno1fuV6SLPM.png)

VLAN划分方式

+ 接口
+ mac
+ ip子网
+ 协议
+ 策略

> PVID,默认1,每个端口只有一个(1-4094)

### 接口类型

+ Access(主机与交换机,只能处理一个标签)
+ Trunk(交换机,处理多个标签)
+ Hybrid(前两个结合)
  + tagged 和 untagged 控制出口
  + 设置PVID

![标签解析](https://s2.loli.net/2024/12/10/XK9shRPErk4Wgw3.png)

### VLAN配置

基础配置

> undo portswitch # 二层接口切换为三层

``` bash
#系统视图
#创建VLAN
vlan vlan-id

#批量创建
vlan batch {vlan-id1 [to vlan-id2]}
# batch -- VLAN ID
# vlan-id1 -- 起始VLAN编号
# vlan-id2 -- 末尾VLAN编号

# 查看VLAN
display vlan

---

# Access
# 接口视图
# 配置接口类型
port link-type access

# 配置Access接口缺省VLAN
prot default vlan vlan-id

--- 
\

# Trunk
# 接口视图
port link-type trunk

# Trunk端口指定VLAN
prot trunk allow-pass vlan {{vlan-id[to vlan-id2]}} | all

# Trunk口缺省VLAN
port trunk pvid vlan vlan-id

---

# Hybrid
# 配置接口类型
prot link-type hybrid

# Hybrid指定VLan 不能同时包含在两个列表中
prot hybrid untagged vlan {vlan-id1 [to vlan-id2]} | all

prot hybrid tagged vlan {vlan-id1 [to vlan-id2]} | all


# Hybrid口缺省VLAN
prot hybrid pvid vlan vlan-id
```

#### MAC 绑定 VLAN

``` bash
# VLAN视图
mac-vlan mac-address mac-address {mac-address-mask|mac-address-mask-length}
# mac地址| mac地址掩码 | mac地址长度1-48

#使能MAC地址与VLAN
# 接口视图
mac-vlan enable

display mac-vlan mac-address all

dis mac-vlan vlanID
```

### VLAN通信

三层交换机实现

+ 物理接口
  + 交换机配置access口,并划分vlan
  + 路由器配置ip地址,与交换机连接线缆,实现三层通信
+ 子接口
+ vlanif

``` bash
# 子接口配置
interface GigabitEthernet0/0/0.10
dot1q termination vid 10
ip address ipaddress
arp broadcast enable
# 最后开启arp广播
```

vlanif

> 存在数据链路层

## STP(spanning tree protocol)生成树协议

> 通过阻塞端口消除环路,实现链路备份
> RSTP（Rapid Spanning Tree Protocol,快速生成树协议）协议基于STP协议,实现网络拓扑快速收敛
> MSTP(默认)

IEEE 802.1D

二层环路典型问题

+ 广播风暴
+ mac地址漂移

操作步骤

1. 选举一个根桥,会出现抢占,谁优先级高谁为根
2. 非根交换机选举一个根端口
3. 网段选举一个指定端口
4. 阻塞非根,非指定端口

### 基本概念

#### 根桥(桥ID)

BID由16位的桥优先级(bridge priority)与桥MAC地址构成(唯一)

16bit bp 48bit mac

BID最小被选举为根桥

1. 先比较端口优先级
2. 之后比较MAC地址

#### 开销(Cost)

> 用于计算根路径开销,即到达根的开销

带宽大,cost小,可配置

![开销计算表.png](https://s2.loli.net/2024/12/10/lkg3yPwEVXOR4GY.png)

#### RPC(root path cost,根路径开销)

接口到根的RPC = 路途所有入方向cost累加

#### 端口ID(PID,port ID)

由 高4bit接口优先级 + 低12bit接口编号 组成
默认128

#### BPDU(bridge protocol data unit,网桥协议数据单元)

STP协议报文,用于STP网络拓扑计算

+ 配置BPDU(configuration BPDU)
+ TCN BPDU(topology change notification BPDU)
  + 网络拓扑改变时发送

![BPDU报文.png](https://s2.loli.net/2024/12/10/Y6c52Jj7VanuofD.png)

### 基础配置

``` bash
# 配置工作模式
stp mode {stp | rstp | mstp}

# 配置根桥
stp root primary

# 备份根桥(优先级4096)
stp root secondary

---

# 优先级(默认32768)
stp priority priority

# 接口开销类型(默认IEEE 802.1t即dit1t)
stp pathcost-standard { dot1d-1998 | dot1t | legacy }

# 配置开销值
stp cost cost

---

# 接口优先级(缺省为128)
stp priority priority

# 启用STP/RSTP/MSTP
stp enable

---

# 批量配置边缘端口
interface range GigabitEthernet 0/0/10 to GigabitEthernet 0/0/20

group-number GigabitEthernet 0/0/10 to GigabitEthernet 0/0/20

# 配置边缘端口
stp edged-port enable
```

### RSTP

> IEEE 802.1w

新增端口类型

+ 备份端口
+ 边缘端口

接口类型减少至三个

+ forwarding
+ learning
+ discarding

VBST: 基于VLAN的STP
MSTP: 多生成树

## 以太网链路聚合与交换机堆叠,集群

> 网络冗余备份,链路聚合,避免单点故障

具体实现

+ 单板
+ 设备

### 链路聚合

提升链路带宽

Eth-Trunk(以太网链路聚合)

相关概念

+ 聚合组(Link Aggregation Group,LAG)
+ 成员接口与成员链路
+ 活动接口 | 活动链路
+ 非活动接口 | 非活动链路
+ 聚合模式:手工模式,LACP
+ 活动接口上,下限

链路聚合控制协议数据单元(link aggregation control protocol data unit,LACPDU)

> 默认系统优先级 32768

### 配置命令

``` bash
interface eth-trunk trunk-id

mode {lacp / manual load-balance}
# 须保持两端链路聚合模式相同,lacp 或者 手工

eth-trunk trunk-id
# 接口视图加入trunkID

trunkport interface-type {interface-number}
# eth-trunk视图

mixed-rate link enable
# 默认不允许速率不同eth-trunk端口加入聚合组

lacp priority priority
# 配置LACP优先级,越小越高,默认32768
# 系统视图 | 接口视图
# 加入聚合组的接口才能设置(即配置端口是否活动端口)

max active-linknumber {number}
# 需保持两端接口数一致
# 只有LACP模式可配置最大活动接口

least active-linknumber {number}
# 配置下限阈值
# LACP及手工模式都可配置
```

## IP路由基础

路由表

| 目的网络/掩码 | 出接口 | 下一跳 |
| -- | -- | -- |
| 10.1.1.0/24 | GE0/0/0 | 1.1.1.2 |

路由信息获取方式及默认优先级

+ 直连路由  0
+ 静态路由  60
+ 动态路由  OSPF内部路由 10 外部 150

`display ip routing-table`
查看路由表

cost 度量值/开销值

转发原则

`最长匹配原则`

### 静态路由

配置命令

``` bash
ip route-static ip-address {mask | mask-length} nexthop-address
# 关联下一跳IP

ip route-static ip-address {mask | mask-length} interface-type interface-number
# 关联出接口

ip route-static ip-address{ mask | mask-length} interface-type interface-number
```

> 缺省路由 0.0.0.0/0

### 动态路由

按工作区域

1.IGP(interior gateway protocols,内部网关协议)

+ RIP
+ OSPF
+ IS-IS

2.EGP(exterior gateway protocols,外部网关协议)

+ BGP

按工作机制及算法

1.distance vector routing protocols,距离矢量路由协议

+ RIP

2.link-state routing protocols,链路状态路由协议

+ OSPF
+ IS-IS

### OSPF基础

路由协议

+ OSPF（Open Shortest Path First，开放式最短路径优先）
+ IGP(Interior Gateway Protocols,内部网关协议)
+ EGP(Exterior Gateway Protocols,外部网关协议)
+ Distance Vector Routing Protocols,距离矢量路由协议
+ Link-State Routing Protocols,链路状路由协议

链路状路由协议

LSA泛洪 -> 建立路由连接
LSDB -> 全网拓扑信息数据库
SPF计算 -> 计算最优路径

### 路由高级特征

路由递归

等价路由

浮动路由

---

路由汇总 | 路由聚合

CIDR(classless inter-domain routing,无类别域间路由)

> 相同网络地址,汇聚为一个

引发问题

+ 划分子网过大,引发环路

### 网络地址转换

> NAT（Network Address Translation，网络地址转换）

解决私有地址与公网地址转换,路由器实现

#### 静态NAT

一个私有地址配置一个共有地址

配置命令

```bash
# 方式一.接口视图
nat static global {global-address} inside {host-address}
# global 公网IP
# inside 私网IP

---

# 方式二.系统视图
nat static global {global-address} inside {host-address}

# 之后在接口视图开启static nat
nat static enable
```

#### 动态NAT

在公网地址池中随机按需使用

配置

```bash
nat address-group group-index start-address end-address
# 创建公有地址池
# group-index 地址池编号

# 配置地址转换为ACL规则
acl number
rule permit source source-address source-wildcard
# 配置基础ACL,匹配需要进行动态转换的源地址范围

nat outbound acl-number address-group group-index [no-pat]
# 接口视图关联地址池和ACL
# no-pat 不进行端口转换
```

#### NAPT,Easy-IP

NAPT(network address and port translation,网络地址端口转换)

>转换地址时连同端口也转换,实现`60000+`地址访问

及动态nat最后不加no-pat

---

Easy IP:无地址池

> 适合HDCP,PPPoE

配置

```bash
acl 2000

rule 5 permit source 192.168.1.0 0.0.0.255

quit

intterface GigabitEthernet0/0/1

nat outbound 2000
# easy ip核心,并绑定ACL
```

#### NAT Server

公网地址:端口 绑定 私网地址:端口

配置

```bash
# 接口视图
nat server protocol tcp global 122.1.2.1 www inside 192.168.1.10 8080
```

## ACL

> Access Control List,访问控制列表

## AAA原理与配置

> AAA（ Authentication, Authorization, and Accounting）认证,授权,计费

NAS(Network Access Server)

AAA服务器

+ 不认证
+ 本地认证
+ 远端认证

aaa认证常用协议
RADIUS （Remote Authentication Dial-In User Service）远程认证拨入用户服务

+ UDP
+ 1812(端口) 认证
+ 1813 计费

配置命令

```bash
aaa
# 进入aaa配置视图

authentication-scheme anthentication-scheme-name
# 创建认证方案

authentication-mode { hwtacacs | local | radius }

# aaa视图
domain domain-name

authentication-scheme authentication-scheme-name
# domain视图绑定认证方案

local-user user-name password cipher password
# 创建本地用户,并配置密码
# 可使用格式 user@pwd

local-user user-name service service-type { {terminal | telnet | ftp | ssh | snmp | http} ppp | none }
# 设置本地用户接入类型,默认全部关闭

local-user user-name privilege level level
# 本地用户权限级别

display domain name default_admin
# 查看配置

display aaa offline-record all
# 查看用户在线信息
```

## 常用网络服务与应用

### FTP

> 20(通信端口) 21(发起TCP连接)端口

通信模式

+ ASCLL模式
+ binary(二进制)模式

工作模式

+ 主动(PORT)
+ 被动(PASV),可控制通信端口

路由交换配置FTP

``` bash
ftp [ipv6] server enable

aaa
local-user user-name password irreversible-cipher password
local-user user-name privilege level level
local-user user-name service-type ftp
local-user user-name ftp-directory directory
# 用户级别必须3以上
```

### TFTP

> 简单文件传输协议,UDP,69

使用

``` bash
tfpt TFTP-Server-IP get filename

tfpt TFTP-Server-IP put filename
```

### telnet

> 23

VTY(virtual type terminal,虚拟类型终端)

配置

``` bash
telnet server enable

user-interface vty 0 4
# 最多支持4个用户远程登录

protocol inbound {all | telnet}
# 设置通信协议,默认ssh

authentication-mode {aaa | none | password}
# 认证方式

set authentication password cipher
# 设置密码,不同版本命令可能不同
```

### DHCP

配置

``` bash
dhcp enable

dhcp select interface
# 接口视图,开启接口地址池DHCP

dhcp server dns-list ip-address
# 指定接口地址池DNS服务器地址

dhcp server excluded-ip-address start-ip-address [end-ip-address]
# 指定不参与自动分配地址

dhcp server lease {day [ hour hour [minute minute]] | unlimited}
# 配置地址租期,默认一天

---
# 全局配置

ip pool ip-pool-name
network ip-address [mask {mask | mask-length}]
gatewag-list ip-address
dns-list ip-address

lease { day day [hour hour [minute minute]] | unlimited }

dhcp selecct global
#接口视图开启该DHCP,即使用全局地址池

ipaddress dhcp-allowc
# 客户在接口视图下获取ip
```

### DNS

+ 递归查询,向其他服务器查询
+ 迭代查询,告知哪里有dns解析地址

### NTP(network time protocol)

> UDP,123

## WLAN概述

### 相关基础概念

> Wireless LAN（无线局域网）,无线网络技术

AP AC

CAPWAP(Control And Provisioning of Wireless Access Points Protocol,无线接入点控制和配置协议)

直连组网,AP最终会经过AC
旁挂组网,AP不一定要经过AC

**无线电磁波**

![无限电磁波频谱]()

**无线组网概念**

BSS(Basic Service Set,基本服务集)

+ 一个AP覆盖范围
+ BSS服务区域内,STA可相互通信

BSSID(Basic Service Setldentifier,基本服务集标识符)

+ 无线网身份标识,AP的MAC表示

SSID(Service Set Identifier,服务集标识符)

+ 无线网的名字
+ 便于识别,用SSID代替BSSID

VAP(Virtual Access Point,虚拟接入点)

+ 一个VAP生成多个AP

ESS(Extend Service Set,扩展服务集)

+ 多AP使用同一个SSID构建的BSS组成一个更大规模的虚拟BSS

### CAPWAP

AP与AC建立隧道

1. AP获取IP地址
   + DHCP获取
   + 广播获取
2. CAPWAP隧道建立
3. AP接入控制
4. AP版本升级(可选)
    + AC只能控制特定版本AP
    + AP与AC版本最好相同
5. CAPWAP隧道维持
    + 控制隧道(keepalive)
    + 数据隧道(echo request,echo responese,报文)

![常见网线接入安全协议]()

## 广域网技术

> WAN（Wide Area Network，广域网）

连接几十至几千公里的局域网

WAN设备分类

+ CE(Customer Edge,用户边缘设备)
+ PE(Provider Edge,服务提供商边缘设备)
+ P(Provider,服务提供商设备)

早期协议: PPP/DHLC/FR/ATM

### PPP

### PPPoE

## 网络管理与运维

### SNMP

### 华为iMaster NCE

## IPV6

报头

## SDN与HFV概述

### SDN（Software Defined Networking，软件定义网络）

解决传统网络难于定位等问题

全网通过SND controler控制(转发)

**iMaster NCE** 网络管控层,华为关于网络层统一管控平台

### NFV（Network Functional Virtualization，网络功能虚拟化）

虚拟化

## 网络编程与自动化

## 园区典型组网架构及实践

园区网:802.3 802.11 协议构建;概述

