---
title: "Linux LvmRecoverData"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:10:15+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# LVM2

LVM丢失后恢复,及LVM一些高级命令!

## LVM丢失后恢复

> 异常断电后造成

### 一.尝试恢复

``` bash
vgcfgrestore -f /etc/lvm/backup/data data

# 还原失败
```

1. 查看`/etc/lvm/backup/data` 文件中硬盘ID号
2. 对比`blkid`输出的`UUID`对比
3. 得出可能是重启后,对于PV的UUID改变导致LVM丢失

### 二.备份数据

``` bash
dd if=/dev/nvme0n1 of=/mnt/bak/nvme0n1.img
```

### 三.修正UUID不一致,并恢复卷组

1.修正UUID

``` bash
pvcreate -u blfaxf-3CER-4r4l-MS32-v0aN-s3Ta-DH08ZV /dev/nvme0n1 --restorefile /etc/lvm/backup/data
```

2.恢复卷组

``` bash
vgcfgrestore -f /etc/lvm/backup/data data

# 查看pv vg lv信息
pvs
vgs
lvs
```

3.激活逻辑卷

``` bash
lvchange -ay /dev/data/home
```

之后即可挂载使用

## 参考

+ [LVM逻辑卷VG卷组丢失故障处理](https://blog.csdn.net/weixin_34234823/article/details/92290258)