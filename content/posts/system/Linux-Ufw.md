---
title: "Linux Ufw"
date: 2024-12-04T11:08:11+08:00
lastmod: 2024-12-04T11:08:11+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->
# UFW

debian 系列默认防火墙

## install

``` bash
sudo apt update 
sudo apt install ufw
```

## setting

``` bash
# 默认关闭全部外部链接端口
ufw default deny

# 拒绝传入，运行传出
sudo ufw default allow outgoing
sudo ufw default deny incoming


# 服务启动状态
sudo ufw status 

# 新装运行通行端口
sudo ufw allow 8080
sudo ufw allow 8080/tcp

# 删除端口
sudo ufw delete allow 8080

# 运行特定IP
sudo ufw allow from 192.168.1.1

# 开启服务
ufw enable

```

查看端口使用情况

```bash
# tcp端口
netstat -ntpl

# udp端口
netstat -aupl

```

## 更多详细内容参考

[seafog - ubuntu ufw防火墙的基本使用](https://www.seafog.cn/archives/141720867)