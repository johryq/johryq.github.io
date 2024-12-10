---
title: "Linux DiskManage"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T10:15:09+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# Linux磁盘管理工具

> 开始 2021年3月24日  
> 更新 2021年3月30日

包括:

+ df - du - dd
+ fdisk
+ parted
+ mkfs

## df & du & dd

1. df: 查看文件系统整体使用量

``` bash
# 常用命令如下
df -h

df -ahT
# 人性化显示带有文件系统类型的所有文件

df -h /etc
# 也可指定目录显示
```

2. du: 查看空间使用情况

``` bash
du -s
# 列出总量不显示目录

du -h 
```

3. dd:备份,复制数据,恢复数据

``` bash
# 备份整个硬盘 /dev/sda 至 /mnt/bak
dd if=/dev/sda of=/mnt/bak

# 备份为硬盘镜像
dd if=/dev/sda of=/mnt/bak/sdabak.img

# 从镜像恢复数据
dd if/mnt/bak/sdabak.img of=/dev/sdb
```

## fdisk: 常用磁盘分区表操作工具

> 仅支持2t及一下磁盘大小

``` bash
fdisk -l    # 查看系统分区情况

fdisk /path # 对该磁盘进行操作

---

m 查看命令解释

p 当前磁盘状态

l 列出已知分区类型

d 删除分区

n 添加分区

p 打印分区表

q 不保存退出

w 写入操作
```

## parted

> 操作大于2t磁盘推荐使用,不像`fdisk`执行命令后要用`w`最后执行,`parted`输入一条命令它就执行了,没有最后的确认  
> `-i` 交互模式  
> `-s` 脚本模式

``` bash
#创建一个MBR分区表
parted -s /dev/sdb mklabel msdos

# 创建gpt分区表
parted /dev/sdb mklabel gpt

#在分区表上创建一个分区并创建文件系统
parted -s /dev/sdb mkpart primary ext4 0.0 100%

#创建一个gpt分区，将硬盘所有空间都分给这个分区，文件系统为ext4
parted -s /dev/sdb mklabel gpt mkpart primary ext4 0.0 100%

#激活分区
parted -s /dev/sdb set 1 boot on

#设置分区名称
parted /dev/sdb name 1 'DATA_DISK'

#删除分区
parted /dev/sdb rm 1

#查看可用分区
parted /dev/sdb print devices
```

## mkfs

> 文件系统格式化  
> mkfs <kbd>tab</kbd> <kbd>tab</kbd> 查看支持的文件系统

``` bash
mkfs.ext4 /dev/sdb 
# 通过.ext4 将该分区设置为ext4的文件系统

mkfs -t ext4 /dev/sdb
# 也可通过上述参数指定文件系统
```

## fsck

> 使用该工具对文件系统进行检查和修复
> 也可`fsck`+<kbd>tab</kbd>+<kbd>tab</kbd> 查看支持的文件系统

|option| 解析 |
|--|--|
| t | 指定文件类型 |
| A | 对/etc/fstab中所有分区检查 |
| C | 显示完整检查进度 |
| p+A | 同时检查多个 |
| R+A | 省略 / |
| V | 详细信息 |
| a | 有错自动修复 |
| r | 有错询问是否修复 |
| f | 强制检查 |

``` bash
# 全部检查修复
fsck  /dev/sdb -y

# 强制检查指定分区并自动修复,显示进度
fsck -Cfa -t ext4  /dev/sdb 
```

## mount

> 执行上述操作后如果不挂载到系统中,依旧是无法访问的  
> `umount` 卸载

``` bash
mount /dev/sdb  /mnt/sda1

umount /dev/sdb
# -f 可强制卸载,可在NFS(网络文件系统)无法读取时使用
```

## 参考

+ [菜鸟教程-linux磁盘管理](https://www.runoob.com/linux/linux-filesystem.html)
+ [Linux分区工具-parted](http://www.weixuecn.cn/article/11488.html)
+ [6个关于dd命令备份Linux系统的例子](https://www.linuxprobe.com/6-examples-to-backup-linux-using-dd-command.html)