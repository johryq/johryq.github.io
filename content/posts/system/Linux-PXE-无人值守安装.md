---
title: "Linux PXE 无人值守安装"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:16:18+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
---
<!--more-->

## 无人值守安装Cenetos7

## KickStart

### PXE

预启动执行环境(Preboot Execute Environment)

>执行大致流程如下

客户机(要安装系统的机器) -> 服务器(DHCP) -> TFTP(下载启动软件包执行安装)

> 需要安装的一些服务

+ http服务器(这里使用apache)

+ tftp(简单文件传输协议,Trivial File Transfer Protocol)

+ dhcp(自动分配IP)

+ syslinux(pxe引导程序)

### 准备工作(关闭selinux和防火墙)

```

vi /etc/selinux/config

# 修改如下内容

SELINUX=disabled



shutdown -r now



systemctl stop iptables

systemctl stop firewalld

```

### 需要安装的服务(注意修改相关ip等信息)

1.http

配置http服务器

```

su

yum install httpd -y

systemctl start httpd

```

挂载镜像文件

```

mkdir /var/www/html/centos7

mount /dev/cdrom /var/www/html/centos7/ #将镜像光盘挂载

```

> 执行成功后可通过浏览器访问该目录

2.tftp

```

yum install tftp-server xinetd -y

vi /etc/xinetd.d/tftp



#修改如下内容

dusable =no



#启动服务

systemctl start xinetd

```

3.dhcp

```

yum install dhcp -y

vi /etc/dhcp/dhcpd.conf

```

# 添加如下内容

```

subnet 192.168.7.0 netmask 255.255.255.0 {

        range 192.168.7.200 192.168.7.240; #可分配ip范围

        option subnet-mask 255.255.255.0;  #子网掩码

        default-lease-time 21600;          #默认ip地址租用时间  

        max-lease-time 43200;              #指定ip最长租用时间

        next-server 192.168.7.139;         #tfpt服务器地址,及本机地址 

        filename "/pxelinux.0";            #tfpt下载目录

}



#启动服务

systemctl start dhcpd

```

>此时客户机即可通过dhcp获取ip

4.复制PXE引导

```

yum install syslinux -y



cp /usr/share/syslinux/pxelinux.0 /var/lib/tfptboot/

cp /var/www/html/centos7/isolinux/* /var/lib/tfptboot/

```

5.修改客户端配置文件实现自动安装

```

mkdir /var/lib/tftpboot/pxelinux.cfg



cd /var/lib/tftpboot/pxelinux.cfg/



cp /var/www/html/centos7/isolinux/isolinux.cfg ./default



cp default default.bak

vi default



# 修改为如下内容

default kickstart

timeout 600

display boot.msg



label kickstart

        menu label ^Install CentOS 7

        kernel vmlinuz

        append initrd=initrd.img ks=http://192.168.7.139/ksconfig/ks.cfg



```

5.配置ks.cfg文件(安装配置)

```

cd /var/www/html/



mkdir ksconfig



cp /root/anaconda-ks.cfg ./ksconfig/ks.cfg



cd ksconfig/



chmod 644 ks.cfg



vi ks.cfg



# 仅供参考,测试安装不通过



install                                                                   #全新安装

url --url="http://192.168.7.139/centos7/"                                 #FTP或http下载地址  

text                                                                      #文本安装

auth --enableshadow --passalga=sha512                                     #认证方式



firstboot --disabled                                                      #初次启动 是否设置代理

firewalld --disabled                                                      #



keyboard --vckeymap=us --xlayouts='us'                                    #系统键盘类型

lang en_US.UTF-8                                                          #语言  



network --bootproto=dhcp --gateway=192.168.7.2 --netmask=255.255.255.0    #ip等

network --hostname=test                                                   #      



rootpw 123456                                                             #root 密码



services --enabled="chronyd"                                              #时间同步服务

timezone Asia/Shanghai -isUtc                                             #时区



bootloader --append=" rhgb quiet" --location=mbr --boot-drive=sda         #引导写入位置



clearpart --all --initlabel                                               #清空系统分区

zerombr                                                                   #

part /boot --fstype=ext4 --size=500                                       #设置分区格式及大小

part /swap --size=1024

part / --fstype=ext4 --size=500

reboot                                                                    #重启服务器

%packages                                                                 #指定安装的软件包

@^minimal

@core

chrony

kexec-tools

@development                                                              #指定安装的命令或开发程序

tree

net-tools

lrzsz

telnet

wget

lsof

%end

```

推荐使用图形化程序配置界面生成配置:

```

vim /etc/yum.repos.d/kick.repo



#写入一下内容

[development]  

name=my-centos7

baseurl=file:///var/www/html/centos7/

enabled=1

gpgcheck=0



#安装启动图形配置



yum -y install system-config-kickstart 

system-config-kickstart 

```

之后保存配置然后覆盖至`/var/www/html/ksconfig/ks.cfg`即可

[图形配置可以参考](https://blog.csdn.net/lxy___/article/details/78813021)

[或者(两个链接内容都一样)](http://www.javashuo.com/article/p-txyzkxhz-p.html)

6.最后设置客户机(要安装系统的机器)pxe启动即可

## 参考

+ linux系统运维指南

+ [Centos 7Kickstart无人值守自动安装](https://blog.csdn.net/lxy___/article/details/78813021)


## Preseed

## 配置环境

+ 本机 ubuntu18.04

+ 镜像 ubuntu18.04

+ root用户

## 所需服务

+ HDCP(自动分配IP)

+ TFTP(传输引导系统)

+ HTTP(下载配置文件)

### 安装相关包

```

apt -y install isc-dhcp-server inetutils-inetd tftpd-hpa pxelinux  apache2

```

### 修改配置

1.dhcp

编辑配置文件

```

vi /etc/dhcp/dhcpd.conf

```

写入一下内容

```

subnet 192.168.7.0 netmask 255.255.255.0 {

        range 192.168.7.200 192.168.7.240; #可分配ip范围

        option subnet-mask 255.255.255.0;  #子网掩码

        default-lease-time 21600;          #默认ip地址租用时间  

        max-lease-time 43200;              #指定ip最长租用时间

        next-server 192.168.7.138;         #tfpt服务器地址,及本机地址 

        filename "/pxelinux.0";            #tfpt下载目录

}

```

启动服务

```

systemctl start  isc-dhcp-server

```

>设置dhcp网卡地址 `/etc/default/isc-dhcp-server`

2.netboot

在ubuntu 18.04镜像中没有该文件夹可从一下地址下载:

> [http://cdimage.ubuntu.com/netboot/](http://cdimage.ubuntu.com/netboot/) -> `netboot.tar.gz`这个文件

将下载的文件复制解压到`/var/lib/ftpboot/

3.http

启动apache2

```

systemctl start httpd

```

> 此时可通过浏览器访问该主机ip查看

## 参考

+ [使用PXE方式引导Ubuntu系统](https://www.linuxidc.com/Linux/2017-08/146442.htm)

+ [官方preseed中文文档](https://wiki.ubuntu.org.cn/%E5%AE%9A%E5%88%B6Ubuntu%E5%AE%89%E8%A3%85CD)

+ [英文文档](https://wiki.ubuntu.com/InstallCDCustomizationHowTo)
