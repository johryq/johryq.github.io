---
title: "Nvidia Error"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:03:41+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# Driver/Library version mismatch

> 2021年7月26日

输入 `nvidia-smi` 报错,nvdia-kernel-mode版本或者nvidia driver版本不一致

## 解决方案

### 1.最简单的就是重启

> 系统会重新加载相关包

### 2.重装驱动

```bash
dpkg -l | grep nvidia
# 查看所以安装的显卡相关包

cat /proc/driver/nvidia/version
# 查看当前系统使用的驱动版本

sudo apt-get remove --purge nvidia-\* && sudo apt-get autoremove
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update && sudo apt-get install nvidia-你需要的版本号
```

> 最后如果还是有问题请重启一遍

### 3.卸载内核驱动模块

```bash
sudo rmmod nvidia
# 一般都卸载不了,会有其他包依赖该模块

lsmod |grep nvidia
sudo lsof -nw /dev/nvidia*
# 查看驱动模块依赖情况与占用进程

sudo remod nvidia_uvm
sudo remod nvidia_modeset
sudo remod nvidia
# 根据依赖情况先后卸载

nvidia-smi
# 确定上是否正常
```

> 测试过该方法,未能成功修复,最后好像要重启`参考一链接`

## 参考链接

+ [Driver/library version mismatch](https://blog.csdn.net/ykf173/article/details/116230368)
+ [Comzyh的博客-卸载驱动模块](https://comzyh.com/blog/archives/967/)
+ [nvidia-smi返回错误信息‘Failed to initialize NVML: Driver/library version mismatch’](https://spring-quan.github.io/2019/03/29/nvidia-smi%E8%BF%94%E5%9B%9E%E9%94%99%E8%AF%AF%E4%BF%A1%E6%81%AF%E2%80%98Failed-to-initialize-NVML-Driver-library-version-mismatch%E2%80%99/)
+ [stackoverflow的更多讨论](https://stackoverflow.com/questions/43022843/nvidia-nvml-driver-library-version-mismatch)
