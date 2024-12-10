---
title: "DLL反编译"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T13:31:22+08:00
draft: false
keywords: []
description: ""
tags: ['反编译']
categories: ['software']
author: "2332334"

---
<!--more-->

# DLL反编译

## 一.使用工具简单介绍

1. 反编译工具[ILSpy](https://github.com/icsharpcode/ILSpy)

2. ildasm 将dll文件分解为IL

3. ilasm 将IL文件重新生成DLL

> ilasm可从 `C:\Windows\Microsoft.NET\Framework\v4.0.30319` 目录找到

## 二.使用步骤简单介绍

1. 将要反编译的`dll`文件拖入ILSpy中
![ILSpy](https://s2.loli.net/2024/12/10/1UL7KTx2bAVzEdj.jpg)

1. 再将该dll拖入`ildasm`中并通过导出(Dump)`IL`文件和`RES`文件
![ildasm](https://s2.loli.net/2024/12/10/Deb3MJHvFYizt8f.jpg)

1. 修改你想修改的相应片段通过cmd使用如下命令导出dll
![ilasm](https://s2.loli.net/2024/12/10/zTDoYavwgncdP4u.jpg)

```powershell
C:\Windows\Microsoft.NET\Framework\v4.0.30319\ilasm.exe /dll/resource=yourFilePath.res yourFilePath.il
```

## 参考链接

+ [通过ILSpy反编译工具和ilasm修改.NET程序](https://www.cnblogs.com/cdaniu/p/15194436.html)
