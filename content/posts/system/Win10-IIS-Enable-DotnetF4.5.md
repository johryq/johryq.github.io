---
title: "Win10 IIS Enable DotnetF4.5"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T13:33:03+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# Win10开启IIS并设置.net4.5框架

## 一.开启IIS

> 控制面板 -> 程序 -> internet Infomation Services

![iis](../../img/iis.png)

> 这里我打开后的版本为`IIS10`

## 二.开启.net4.5

### 二.1 确认已安装framework版本

首先确定您电脑是否安装该版本框架，具体信息参考[微软官网](https://learn.microsoft.com/zh-cn/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)

1. 通过命令确定是否安装

```powershell
(Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full").Release -ge 394802
//确定是否已安装 .NET Framework 4.6.2 或更高版本
```

2. 通过组册吧确定

```cmd
regedit
// 打开注册表
```

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full`的`Release`条目值大于`378389`即可确定安装了大于4.5的框架

### 二.2 开启iis后默认只有`.net4.0`作为程序运行池子

1. 通过一下命令打开.net4.5运行池

```cmd
// aspnet_regiis.exe -i

dism /online /enable-feature /featurename:IIS-ISAPIFilter
dism /online /enable-feature /featurename:IIS-ISAPIExtensions
dism /online /enable-feature /featurename:IIS-NetFxExtensibility45
dism /online /enable-feature /featurename:IIS-ASPNET45
```

如出现以下报错

```cmd
The operation is complete but IIS-ASPNET45 feature was not enabled.

A required parent feature may not be enabled. You can use the /enable-feature /all option to automatically enable each parent feature fr
om the following list. If the parent feature(s) are already enabled, refer to the log file for further diagnostics.                     
IIS-ISAPIFilter, IIS-ISAPIExtensions, IIS-NetFxExtensibility45
```

执行

```cmd
dism /online /enable-feature /featurename:IIS-NetFxExtensibility45
dism /online /enable-feature /featurename:NetFx4Extended-ASPNET45
dism /online /enable-feature /featurename:IIS-ASPNET45

// 我是通过如上命令开启的
```

![iis4](../../img/iis4.png)

> `dism /online /Get-Features 查看已安装产品`

2. 也可尝试通过控制面板安装

![iis3](../../img/iis3.png)

