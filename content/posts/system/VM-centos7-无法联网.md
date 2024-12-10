---
title: "VM Centos7 无法联网"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:11:20+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# Centos7 虚拟机无法上班

## 首先查看本机网络信息

`ifconfig /all` #查看网卡信息

VMware安装完成之后会自动安装两个虚拟网卡,也就是:

+ VMware Virtual Ethernet Adapter for VMnet8
  + 这个就是一般`NAT`模式虚拟机使用的网卡
+ VMware Virtual Ethernet Adapter for VMnet1
  + 这个是另一个模式---`仅主机(only host)`;虚拟机与主机共用ip吧(也没用过)

## DHCP

```bash
sudo vi /etc/sysconfig/network-scripts/ifcfg-ens33

#开启如下 
ONBOOT=yes 

systemctl restart network
```

## 设置静态网卡上网

`sudo vi /etc/sysconfig/network-scripts/ifcfg-ens33`

一般网卡为`ifcfg-ens33`,但是也有可能是`ens`其他,具体使用`ip a`查看

将网卡信息修改为(主要是标注出来的几行):

```conf
TYPE=Ethernet

PROXY_METHOD=none

BROWSER_ONLY=no

BOOTPROTO=static      >这里改成静态

DEFROUTE=yes

IPV4_FAILURE_FATAL=no

IPV6INIT=yes

IPV6_AUTOCONF=yes

IPV6_DEFROUTE=yes

IPV6_FAILURE_FATAL=no

IPV6_ADDR_GEN_MODE=stable-privacy

NAME=ens33

UUID=cc6270c7-265f-4d6d-8c04-4f8901995663

DEVICE=ens33

ONBOOT=yes             >开机启动

IPADDR=192.168.137.100 >这个ip地址随意设置,只要不和其他虚拟机冲突就好

NETMASK=255.255.255.0  >默认网段

GATEWAY=               >网关--也就是VMnet8网卡看到的网关

DNS1=                  >你主机的NDS

IPV6_PRIVACY=no

```

然后使用 `sudo systemctl restart network` 重启网络服务即可

centos8 使用 `sudo systemctl restart NetworkManager`

## 参考链接

+ [centos8配置静态IP地址](https://blog.csdn.net/networken/article/details/106867172)