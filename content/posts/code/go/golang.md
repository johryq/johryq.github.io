---
title: "Golang"
date: 2021-11-08T19:58:18+08:00
lastmod: 2024-12-04T08:54:18+08:00
draft: false
keywords: []
description: ""
tags: ['go']
categories: ['code']
author: "2332334"

---
<!--more-->

# golang

## 安装

### 安装二进制包

1.下载相应go版本并解压

``` bash
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.14.3.linux-amd64.tar.gz
```

> 如果已经安装会先删除go目录

2.添加环境变量

``` bash
echo "export PATH=$PATH:/usr/local/go/bin" >> /etc/profile && source /etc/profile
```

3.检查是否安装成功

```bash
go version
```