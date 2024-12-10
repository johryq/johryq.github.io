---
title: "Ext4文件修复"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:01:10+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# Ext4文件修复

> 2021年7月27日

公司raid5 两块硬盘同时故障,找了数据修复公司,最后出现ext4文件系统有问题  

> 以下仅作记录参考,并未实践,最后还是那家公司解决的

## 相关知识点

### super block

硬盘分区开头、开头的第一个byte是byte0，从byte1024开始往后的一部分数据。由于block size最小时1024bytes，所以superblock在block1中（此时block的大小正好是1024bytes），也可能是在block 0中。  

超级块保存了文件系统设定的文件块大小、操作函数、inode链表等重要信息。

### 查看分区设备信息

``` bash
dumpe2fs /dev/sdb

tune2fs -h /dev/sda

```

### 查看备份超级块

```bash
mkfs.ext4 -n /dev/sdb
# 需要先卸载分区
```

### 尝试修复超级块

1.已知文件系统类型使用备份超级块

``` bash
mkfs.filesystem -n /dev/sda
# 及上一步查看备份超级块

mount -t ext4 -o sb=131072 /dev/sdb /mnt/a
# 尝试使用备份超级块挂载  
# 查看的备份超级块是 1k 的,这里参数是使用 4k ,所以使用时参数=备份超级块*4

fsck.ext4 -b 32768 /dev/sdb
# 这里 1k
# 务必卸载设备再进行修复,并仔细观察输出信息
```

2.全部超级块损坏,进行重建修复(数据丢失风险大)

``` bash
mkfs.ext4 -S /dev/sdb
# 重建

fsck.ext4 -y /dev/sdb
# 修复
```

> 最后挂载看丢失多少

---

3.不确定文件系统

> 使用时注意提示信息,可能导致文件系统不正常,修复后变为ext3,ext2等,需手动升级;`不推荐使用`

``` bash
fsck -r /dev/sdb
```

## 参考地址

+ [Ext4文件系统修复](https://www.cnblogs.com/xcbki/p/11288149.html)
