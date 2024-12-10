---
title: "Typecho Change Theme"
date: 2021-11-08T19:58:20+08:00
lastmod: 2024-12-03T16:36:20+08:00
draft: false
keywords: []
description: ""
tags: ['typecho theme']
categories: ['blog']
author: "2332334"

---
<!--more-->


<!--markdown-->
# Typecho更换主题

> 闲来无事先换一个typecho的主题,本以为几分钟的事,结果却搞了许久!

<!--more-->

## 折腾

刚开始准备更换 **[Aria](https://github.com/Siphils/Typecho-Theme-Aria)**  这款主题的!  

结果遇到了如下问题:

1. php未安装json扩展!导致无法请求!

2. 想用php的***phpize***安装扩展,结果未安装(源码安装的),有点捉急!

3. 网页文件无法修改(权限问题)!

---

## 最后我选择重装php

```bash

rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

rpm -Uvh http://rpms.remirepo.net/enterprise/remi-release-8.rpm

dnf -y install dnf-utils

yum install php74-php 

yum search php74* # 自行选择需要的包安装

systemctl restart php74-php-fpm

systemctl enable php74-php-fpm

```

### nginx 与 php通信

www.conf 配置文件修改以下项:

+ user = 用户名

+ group = 组

+ listen = 127.0.0.1:9000

最后重启php-fpm

> 尝试unix:php-fpm.sock失败稍后虚拟机尝试

### 考网址

+ [完全卸载php](https://www.cnblogs.com/tongcharge/p/11765592.html)

+ [typecho开启debug](https://iao.su/2892/)

+ [安装php](https://www.cnblogs.com/alliancehacker/p/12255445.html)
