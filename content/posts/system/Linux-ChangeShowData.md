---
title: "Linux ChangeShowData"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:08:39+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
---
<!--more-->

# Linux修改系统时间显示为：年月日时分秒

+ 1、编辑全局配置文件：/etc/profile，使所有用户均显示该格式：

```bash
vim  /etc/profile
export TIME_STYLE="+%Y-%m-%d %H:%M:%S"

#or

echo "export TIME_STYLE='+%Y-%m-%d %H:%M:%S'" >> /etc/profile
```

+ 2、让配置立即生效：

```bash
source  /etc/profile

# 验证配置是否生效
ll 
```
