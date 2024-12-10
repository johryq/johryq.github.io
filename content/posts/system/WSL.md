---
title: "WSL"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T13:29:57+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# WSL

> bash命令均运行在PowerShell  
> [官方文档](https://docs.microsoft.com/en-us/windows/wsl)

## WSL安装

启用`适用于Linux的Windows子系统`

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

或者:

控制面板 -> 程序 -> 启用或或关闭Windows功能 -> 勾选`用于Linux的Windows子系统`

> 至此重启计算机,在应用商店安装ubuntu即可`(WSL1)`

## 升级WSL2

### 基本要求

windows版本要求

+ x64 需要 `1903+`
+ ARM64 需要 `2004+`
+ 内部版本低于`18362`不支持WSL2
+ `winver` 命令可查看win版本
+ 1903和1909需要内部版本号`18362.1049+`或`18363.1049+`

硬件要求

+ 开启bios的`Hyper-V`,即需要支持`Hyper-V`功能
+ `Systeminfo` 命令可查看系统相关信息

### 安装步骤

1.启用`虚拟机平台功能`

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

或者:

控制面板 -> 程序 -> 启用或或关闭Windows功能 -> 勾选`虚拟机平台`

2.[下载Linux内核更新程序包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

> 适用于X64 PC

3.重启电脑进行最后配置

``` powershell
wsl --list --verbose
# 或者
wsl -l -v
查看安装的linux

wsl --set-version <distribution name> <versionNumber>
# 将其设置为WSL2

wsl --set-default-version 2
# WSL2设为默认
```

> `wsl -l -v` 该命令需要内部版本高于`18362`才可使用

## WSL更改安装位置

大致找到了两种方法:

>以下命令均在 `windows powershell` 中执行

### 一. LxRunOffline

1.下载安装 `LxRunOffline` 并添加环境变量

+ [该项目Github地址](https://github.com/DDoSolitary/LxRunOffline)

2.查看 WSL 名称

+ `lxrunoffline l` 或者 `wsl -l`

3.移动 WSL

``` bash
lxrunoffline m -n <WSL名称> -d <路径>

lxrunoffline di -n <WSL名称>
```

完成后即可完成 WSL 更改位置

### 二. 使用 wsl 自带工具移动

1.查看 WSL 相关命令

``` bash

wsl --version

```

2.查看 WSL 名称

``` bash
wsl -l

```

3.备份还原 wsl

``` bash
wsl --export [wls名称] [打包位置的.tar]

wsl --import [wsl名称] [还原位置] [打包文件]

```

以上

## 参考地址

+ [LxRunOffline 使用教程 - WSL 自定义安装、备份](https://p3terx.com/archives/manage-wsl-with-lxrunoffline.html)

+ [简单到极致！Windows 10 Ubuntu子系统的备份/还原教程来了](https://www.jianshu.com/p/8b4ec8fafdca)
+ [安装和使用 WSL2](https://blog.csdn.net/dbyoung/article/details/106888004)