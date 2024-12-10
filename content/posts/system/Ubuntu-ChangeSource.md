---
title: "Ubuntu ChangeSource"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T13:34:30+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
---
<!--more-->

<!--markdown-->
# 国内开源镜像站点

## [阿里云](https://developer.aliyun.com/mirror/)

+ ubuntu apt源修改

  1. 修改文件 `/etc/apt/sources.list`

  2. 替换为 [*该网页*](https://developer.aliyun.com/mirror/ubuntu) 的内容

  3. 最后执行 `apt update` 更新应用列表

+ [centos](https://developer.aliyun.com/mirror/centos)

## [腾讯云](https://mirrors.cloud.tencent.com/)

```bash
# 公网使用 http://mirrors.tencent.com/
# 内网使用 http://mirrors.tencentyun.com/

sudo cp /etc/apt/source.list /etc/apt/source.list.bak
sudo wget -O /etc/apt/sources.list http://mirrors.cloud.tencent.com/repo/ubuntu<ubuntu_version_num>_sources.list
sudo apt clear all
sudo apt update

```

## [清华镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)
