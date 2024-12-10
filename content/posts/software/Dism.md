---
title: "Dism"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T13:30:33+08:00
draft: false
keywords: []
description: ""
tags: ['dism']
categories: ['software']
author: "2332334"
---
<!--more-->

# win Dism

## 命令

```powershell
Dism /Online /Cleanup-Image /ScanHealth
#这条命令将扫描全部系统文件并和官方系统文件对比，扫描计算机中的不一致情况。

Dism /Online /Cleanup-Image /CheckHealth
#这条命令必须在前一条命令执行完以后，发现系统文件有损坏时使用。

DISM /Online /Cleanup-image /RestoreHealth
#这条命令是把那些不同的系统文件还原成官方系统源文件。

sfc /SCANNOW
#无论前a三条命令是否可用，完成后重启，再键入以下命令：

```