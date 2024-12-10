---
title: "Linux KernelUpdate"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T10:57:23+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
---
<!--more-->

# Linux 内核升级及自动更新

## 一.Ubuntu内核升级

### 手动更新内核

``` bash
uname -sr
# 查看当前内核版本

sudo dpkg --get-selections | grep linux
# 查看已安装内核
```

> 选择需要的内核版本: https://www.kernel.org/

内核有四种:

+ RC(prepatch) 预发布
+ Mainline 主线版本
+ Stable 稳定版
+ Longterm 长期维护版本

> ubuntu内核主线版本: https://kernel.ubuntu.com/~kernel-ppa/mainline/

选择相应硬件版本后,下载四个文件:2`header`,1`image`,1`modules`

> 4.17前不包含`modules`文件,下载3个文件即可

安装下载的内核

``` bash
wget 四个包的地址

sudo dpki -i *.deb

reboot
```

### apt更新内核

```bash
sudo apt-get update
sudo apt-get upgrade
# 更新整个系统和所有包

sudo apt-get upgrade linux-image-generic
# 只更新内核
```

### 更多内核更新工具

+ Ukuu
+ Uktools
+ Linux Kernel Utilities

## 二.Ubuntu内核自动升级

### apt-mark

```bash
sudo apt-mark hold linux-image-generic linux-headers-generic
# 关闭内核自动更新

sudo apt-mark unhold linux-image-generic linux-headers-generic
# 开启内核自动更新
```

### 修改配置文件

``` bash
# 修改以下文件
sudo vim /etc/apt/apt.conf.d/10periodic
sudo vim /etc/apt/apt.conf.d/20auto-upgrades

#关闭自动更新
APT::Periodic::Update-Package-Lists "0";
APT::Periodic::Download-Upgradeable-Packages "0";
APT::Periodic::AutocleanInterval "0";
APT::Periodic::Unattended-Upgrade "0";

#开启自动更新
APT::Periodic::Update-Package-Lists "2";
APT::Periodic::Download-Upgradeable-Packages "1";
APT::Periodic::AutocleanInterval "0";
APT::Periodic::Unattended-Upgrade "1";
```

## 参考地址

+ [记一次Ubuntu 18.04 内核升级](https://zhuanlan.zhihu.com/p/75669680)
+ [升级 Ubuntu Linux 内核的几种不同方法](https://linux.cn/article-12125-1.html)