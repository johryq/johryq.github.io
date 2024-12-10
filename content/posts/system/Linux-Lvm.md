---
title: "Linux Lvm"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:07:24+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
---
<!--more-->

# linxu LVM

> 2021年3月24日
> Logical Volume Management(逻辑容量管理)

要了解的基础概念:

+ pv(Physical Volume):物理卷
+ PP(Physical Extend):物理区域
+ vg(Volume Group):卷组
+ lv(Logical Volume):逻辑卷

![结构](https://s4.51cto.com/images/blog/201803/09/4c78a8107a3a9d94ec95a0349749deb2.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

## 使用基本流程

``` bash
# 1. 创建物理卷
pvcreate /dev/sda /dev/sdb

# 查看创建的物理卷
pvs || pvdisplay

# 2. 创建卷组,即将两个次磁盘合并到一个卷组中,其最小单位为4m,可通过 -s 在创建时修改大小
vgcreate vg1 /dev/sda /dev/sdb

# 同样使用类似命令查看
vgs || vgdisplay

# 3. 创建逻辑卷,指定卷组大小即名字
lvcreate -L 2T -n lv1 vg1

# 4. 格式化逻辑卷
mkfs.ext4 /dev/vg1/lv1

# 5. 挂载逻辑卷
mount /dev/vg1/lv1 /mnt/lv1
```

## /etc/fstab

> 手动挂载信息需写入该文件实现开机自动挂载

| 设备 | 挂载点 | 文件系统 | 参数 | 备份 | 自检 |
|--|--|--|--|--|--|
| Device | Mount Point | FileSystem | Parameters | Dump | Fsck |

### Parameters参数包括

| 参数 | 解析 |
| -- | -- |
| Async/sync | 设置是否为同步方式运行，默认为async |
| auto/noauto | 当下载mount -a 的命令时，此文件系统是否被主动挂载。默认为auto |
| rw/ro | 是否以以只读或者读写模式挂载 |
| exec/noexec | 限制此文件系统内是否能够进行"执行"的操作 |
| user/nouser | 是否允许用户使用mount命令挂载 |
| suid/nosuid | 是否允许SUID的存在 |
| Usrquota | 启动文件系统支持磁盘配额模式 |
| Grpquota | 启动文件系统对群组磁盘配额模式的支持 |
| Defaults | 同事具有rw,suid,dev,exec,auto,nouser,async等默认参数的设置 |

``` bash
# 示例1
Label=/dev/sdb /mnt/sda1 ext4 defaults 0 0

UUID=18823fc1-2958-49a0-9f1e-e1316bd5c2c5 /mnt/sda1 ext4 defaults 0 0
```

## 扩容

``` bash
# 卷组扩容
pvcreate /dev/sdc
vgextend vg1 /dev/sdc

# 逻辑卷扩容至最大并自动加载起始点
lvextend -L +100%FREE /dev/vg1/lv1 -r

#如不加 -r 选项,并且只扩容200m
lvextend -L +200M /dev/vg1/lv1
resize2fs /dev/vg1/lv1
```

## 缩小容量

>不推荐使用,需要先卸载已挂载的逻辑卷并检查文件系统

``` bash
# 卸载并检查文件系统
umount /dev/vg1/lv1
e2fsck -f /dev/vg1/lv1
resize2fs /dev/vg1/lv1

# 缩小 200m LV
lvreduce -L 200 /dev/vg1/lv1
mount /dev/vg1/lv1 /mnt/lv1

# 缩小 VG
vgreduce vg1 /dev/sdc

# 移除PV以减少VG大小
pvremove /dev/sdc
```

## 参考

+ [/etc/fstab文件的详解](https://blog.csdn.net/youmatterhsp/article/details/83933158)
+ [逻辑卷管理(LVM)](https://blog.51cto.com/13438667/2084924)