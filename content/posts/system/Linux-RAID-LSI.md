---
title: "Linux RAID LSI"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:30:21+08:00
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

# Raid-LSI

> [博通官网](https://www.broadcom.com/)
> 型号: LSI-9361-8i

Raid卡命令行工具

> `lspci -v|grep RAID`查看Raid卡版本

## 下载安装(StorCLI)

1.[官网下载](https://www.broadcom.com/support/download-search)

2.解压并安装

```bash
#解压下载的文件
unzip 007..

# 根据系统选择安装方式安装完成后,linux使用以下命令确认安装完成
/opt/MegaRAID/storcli/storcli64 -v

alias "storcli=/opt/MegaRAID/storcli/storcli64"
```

>`LSA包的安装脚本`
其安装脚本含有四种安装方式选项(自行选择安装):

``` txt
            1. - Gateway
                  All program features will be installed. 'Requires the most dis                                      k space.'
            2. - StandAlone
                  This option will install components required for Local Server                                       Management
            3. - DirectAgent
                  This option will install components required for Remote Server                                       Management
            4. - Light Weight Monitor
                  Light Weight Monitor program features will be installed.

```

## 使用即相关命令

``` bash
storcli show
storcli show all
```

简短帮助文档

```txt
List of commands:

Commands   Description
-------------------------------------------------------------------
add        Adds/creates a new element to controller like VD,Spare..etc
delete     Deletes an element like VD,Spare
show       Displays information about an element
set        Set a particular value to a property
get        Get a particular value to a property
compare    Compares particular value to a property
start      Start background operation
stop       Stop background operation
pause      Pause background operation
resume     Resume background operation
download   Downloads file to given device
expand     expands size of given drive
insert     inserts new drive for missing
transform  downgrades the controller
reset      resets the controller phy
split      splits the logical drive mirror
/cx        Controller specific commands
/ex        Enclosure specific commands
/sx        Slot/PD specific commands
/vx        Virtual drive specific commands
/dx        Disk group specific commands
/fall      Foreign configuration specific commands
/px        Phy specific commands
/lnx       Lane specific commands
/[bbu|cv]  Battery Backup Unit, Cachevault commands
Other aliases : cachecade, freespace, sysinfo

Use a combination of commands to filter the output of help further.
E.g. 'storcli cx show help' displays all the show operations on cx.
Use verbose for detailed description E.g. 'storcli add  verbose help'
Use 'page[=x]' as the last option in all the commands to set the page break.
X=lines per page. E.g. 'storcli help page=10'
Use J as the last option to print the command output in JSON format
Command options must be entered in the same order as displayed in the help of
the respective commands.
Use 'nolog' option to disable debug logging. E.g. 'storcli show nolog'
```

> 更多参考官方文档,下方博客命令对新版本已经无法使用

## 参考

+ [MegaCli 监控raid状态](http://blog.chinaunix.net/uid-25135004-id-3139293.html)
+ [BROADCOM-博通官方文档](https://www.broadcom.com/support/download-search)