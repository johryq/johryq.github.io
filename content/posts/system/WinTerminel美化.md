---
title: "WinTerminel美化"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T13:35:29+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

<!--markdown-->
# Windows Terminel美化

> 以管理员方式运行WIndow Terminal

<!--more-->

## 美化流程

### 1.修改window terminal配置

``` json
 "profiles": {
    "defaults": {
      // Put settings here that you want to apply to all profiles
      "acrylicOpacity": 0.8, //背景透明度
      "useAcrylic": true, // 启用毛玻璃
      "backgroundImage": "D:\\OneDrive\\图片\\stack.jpg", //背景图片
      "backgroundImageOpacity": 0.5, //图片透明度
      "backgroundImageStretchMode": "fill", //填充模式
      "icon": "ms-appx:///ProfileIcons/{9acb9455-ca41-5af7-950f-6bca1bc9722f}.png", //图标
      "fontFace": "Sarasa Term SC", //字体
      "fontSize": 14, //文字大小
      "colorScheme": "Solarized Light", //主题
      "cursorColor": "#FFFFFF", //光标颜色
      "cursorShape": "bar", //光标形状
      "startingDirectory":"D://Projects//" //起始目录
    }
 }
```

### 2.Nuget安装相关包

```powershell
Set-ExecutionPolicy AllSigned
set-executionpolicy remotesigned
#允许网络签名
```

 ***安装以下包***

``` powershell
Install-Module git-aliases
Install-Module posh-git

Install-Module oh-my-posh
# A prompt theme engine for any shell.
Install-Module -AllowClobber Get-ChildItemColor
# 让 ls (Get-ChildItem) 像 Unix 系终端
Install-Module DirColors
```

> `Get-PoshThemes`打印所有主题

### 3.修改配置文件以永久保存

`$PROFILE` #查看配置文件配置

`code $PROFILE` #vscode打开配置文件并复制以下内容并保存

``` powershell
#-Verbose 选项会显示详细加载信息
$env:POSH_GIT_ENABLED = $true
Import-Module DirColors
Import-Module posh-git
Import-Module oh-my-posh
Import-Module git-aliases -DisableNameChecking
Import-Module Get-ChildItemColor 
Set-PoshPrompt -Theme  amro
# 设置oh-my-posh主题
```

> 一些主题因为所用字体没有相关符号会显示乱码,这里使用了[FantasqueSansMono Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases)

### 4.官方配色工具

安装Chocolatey

>根据 **[Chocolatey官方](https://chocolatey.org/)** 的安装方法进行安装

```powershell
choco install colortool
```

之后复制到配置文件中,并应用配置即可

> [更多配色方案](https://github.com/mbadolato/iTerm2-Color-Schemes/tree/master/windowsterminal)
---

## 参考地址

+ [微软官方windowsTerminal文档](https://docs.microsoft.com/en-us/windows/terminal/customize-settings/global-settings)

+ [Windows Terminal 终极美化](https://www.chuchur.com/article/windows-terminal-beautify)