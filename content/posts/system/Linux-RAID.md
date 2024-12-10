---
title: "Linux RAID"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:29:43+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
# cover:
#     image: "" # image path/url
#     alt: "<alt text>" # alt text
#     caption: "<text>" # display caption under cover
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/<path_to_repo>/content"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---
<!--more-->

<!--markdown-->### RAID磁盘阵列

>*[ Redundant Arrays of Inexpensive Disks ]*  

**RAID:容错式廉价磁盘阵列**

---

通过软硬件将小磁盘整合的装置,同时具有数据保护功能!

---

#### *RAID* 由不同 *level* 等级选择,使得磁盘具有不同功能

+ ***RAID-0*** (等量模式,stripe): 效果最佳

  + 数据通过分割后存储于各个磁盘

>任何一个磁盘损毁都将造成数据丢失

---

+ ***RAID-1*** (映像模式,mirror): 完整备份

  + 磁盘一半存储一般备份

>软件阵列写入不佳(只有一个南桥),硬件自动复制不走系统I/O,多线程读取RAID自行取得最佳平衡

---

+ ***RAID-1+0*** or ***RAID-0+1***

  + 推荐1+0

  + 0和1都不需计算读写比其他RAID好

---

+ ***RAID-5***

  + 写入时(striping),在每颗磁盘加入一个同位检查数据(Parity),该数据记录其他磁盘备份数据.

  + 同位检查码CPU计算

  + 预设支持一颗磁盘损毁

  + ***RAID-6*** 支持两颗磁盘损坏

---

+ ***Spare Disk*** :预备磁盘功能

  + 通过预留磁盘,在阵列中有磁盘故障时自动更换错误磁盘,使用该预留磁盘!

---

![RAID.png](https://s2.loli.net/2024/12/10/hcmJ95jHvlApeuD.png)

>摘抄至 **<<linux鸟哥私房菜>>**
