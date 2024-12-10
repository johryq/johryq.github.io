---
title: "Python Change Source"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T08:51:00+08:00
draft: false
keywords: []
description: ""
tags: ['pip','python','code']
categories: ['python']
author: "2332334"

---
<!--more-->

# 更换国内源

``` bash
    mkdir ~/.pip  
    vi ~/.pip/pip.confg  
    
    # 写入如下内容：
    [global]
        timeout = 6000
        index-url = https://mirrors.aliyun.com/pypi/simple/
        trusted-host = mirrors.aliyun.com
```
