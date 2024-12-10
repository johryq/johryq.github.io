---
title: "Disk Type"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:05:21+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# 关于一些常见的硬盘格式

## win

### FAT

文件分配表

最开始供 MS-DOS 使用，一直演化，开始有 Fat12，之后到 Fat16，到现在的 Fat32。

Fat32 中的 32 是指 32 位，32 位最大值为 2 的 32 次方，就是 4G，也就是说Fat32 最大的限制是不能存储大于 4G 的文件。

### HPFS

### NTFS (New Technology File System)

微软为其第一代操纵系统Windows NT 3.1开发的文件系统。

80年代，微软和国际商用机器公司 IBM 合作，开发图形操作系统OS/2。

但两个公司在很多问题上产生分歧而合作终止。OS/2 的文件系统叫 HPFS，NTFS 借鉴了 HPFS，有很多共同之处。因为开发 NTFS、HPFS 这两个文件系统的就是同一批人，在现在的 Windows 系统上，默认的文件格式就是 NTFS。

### ReFS

提供更强的弹性机制，高性能的超大容量数据存储以及最大限度保证数据的可靠性和可用性。

ReFS不是NTFS的真正替代品（ReFS卷不可引导），但它本质上是为高级用户提供更高效的文件系统，REFS文件系统有点类似NTFS+RAID5。

> [FAT、HPFS 和 NTFS 文件系统的概述](https://learn.microsoft.com/zh-cn/troubleshoot/windows-client/backup-and-storage/fat-hpfs-and-ntfs-file-systems)

---

## linux

### ext (Extended file system)

在有 ext 之前，使用的是 MINIX 文件系统

linux（1991首次公布 MINIX file system 64mb）

+ ext 1992

ext 可以处理高达 2 GB 存储空间并处理 255 个字符的文件名

+ ext2 1993

提供了 GB 级别的最大文件大小和 TB 级别的文件系统大小

+ ext3 1998

加入日志系统（一下三种日志级别）

+ 日记(journal）
+ 顺序(ordered)
+ 回写(writeback)

ext3 使用 16 位内部寻址。这意味着对于有着 4K 块大小的 ext3 在最大规格为 16 TiB 的文件系统中可以处理的最大文件大小为 2 TiB。

+ ext4 2006

ext4 在功能上与 ext3 在功能上非常相似，但支持大文件系统，提高了对碎片的抵抗力，有更高的性能以及更好的时间戳。

ext4 使用 48 位的内部寻址

不推荐文件大于50tb

虽然理论支持100tb

> 下面三种为大文件存储选择文件系统

### XFS

64 位的日志文件系统,虽然 XFS 是稳定的且是高性能的，但它和 ext4 之间没有足够具体的最终用途差异

### ZFS

它理论上可以解决大型存储系统。

ZFS 许可证是 CDDL 许可证

### Btrfs

性能问题

---

## mac

### APFS（Apple File System）

苹果最新的文件系统，在这之前用的是 HFS，后面有 HFS+ 或 HFS Plus。HFS 文件系统历史悠久，是针对传统的机械磁盘开发的文件系统。后面对针对 SSD 做优化，开发了 APFS，在 iOS 10.3 时正式引入。APFS 支持写时复制，同一个文件，无论复制多少份，假如不修改，这个文件的实际内容只会在磁盘中存储一份，只是其索引有 N 份。

---

## 移动设备

USB-HDD模式： USB-HDD硬盘仿真模式，此模式兼容性很高，适用于新机型，但对于一些只支持USB-ZIP模式的电脑则无法启动，一般制作U盘启动盘选择该模式。
USB-ZIP模式：大容量软盘仿真模式，此模式在一些比较老的电脑上是唯一可选的模式，但对大部分新电脑来说兼容性不好，特别是2GB以上的大容量U盘。

### exFat

exFAT 是微软专门为闪存开发的一种开发的文件格式，支持存储大于 4G 的文件。NTFS 使用日志，会比非日志的文件格式读写更多的磁盘，对闪存储造成较大的负担，理论上 NTFS 格式的 U 盘容易损坏。U 盘格式成 exFAT 只是为了方便，Mac 和 Windows 都可读写，也可存放大文件，但exFAT 没有日志功能。

## other

fat3 和 ntfs 都通过日志系统解决前期版本数据稳定性，一直性问题

及：前期版本在写入过程中突然断电会造成整个文件系统崩盘，且无法卸载（与写入文件不想关的文件依旧会出问题）；fat2 后期使用过程中磁盘碎片会造成严重性能损失


## 参考链接

+ [Fat32、NTFS、exFAT、HFS+、APFS文件系统的区别](https://blog.csdn.net/qq_39111085/article/details/103800464)

+ [深入理解 ext4 等 Linux 文件系统](https://zhuanlan.zhihu.com/p/44267768)