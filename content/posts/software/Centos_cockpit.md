---
title: "Centos_cockpit"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:09:04+08:00
draft: false
keywords: []
description: ""
tags: ['centos','cockpit']
categories: ['software']
author: "2332334"

---
<!--more-->

# Centos_cockpit.socket

centos web管理server

> 默认查看地址为 http://ip:9090  
> Web管理服务

```bash
systemctl enable --now cockpit.socket
#启动该服务，随系统启动一同启动

systemctl start cockpit.socket
#运行Cockpit服务

systemctl status cockpit.socket
#查看状态

systemctl get-default
#查看显示模式
```
