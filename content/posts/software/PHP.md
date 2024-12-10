---
title: "PHP"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:14:57+08:00
draft: false
keywords: []
description: ""
tags: []
categories: ['software']
author: "2332334"

---
<!--more-->

# 安装PHP

## [编译安装](https://www.php.net/downloads.php)

> ubuntu18.04
> php7.4.15
> centos7

### 1.安装相关依赖

``` base
#ubuntu

sudo apt install build-essential libpcre3-dev zlib1g zlib1g-dev curl  libjpeg62-dev libxml2 libxml2-dev libfreetype6 libfreetype6-dev libpng16-16 libpng-dev libpnglite-dev libiconv-hook-dev libiconv-hook1 libssl-dev libcurl4-openssl-dev  php-gd libxslt1-dev libsqlite3-dev libonig-dev  -y



#centos

sudo yum install libxml2 libxml2-devel sqlite-devel bzip2 bzip2-devel zlib zlib-devel libjpeg libjpeg-devel libpng libpng-devel gd gd-devel libxslt libxslt-devel freetype freetype-devel openssl openssl-devel  oniguruma oniguruma-devel libcurl libcurl-devel ncurses curl -y #libiconv

```

### 2.编译安装

``` base
# 新建用户（可选）

# useradd -s /sbin/nologin -M www



# ubuntu

./configure \

--prefix=/usr/local/php7.4.15 \

--with-fpm-user=www \ 

--with-fpm-group=www \

--with-apxs2=/usr/local/apache2.4.33/bin/apxs \

--with-xmlrpc \

--with-openssl \

--with-zlib \

--with-iconv \

--with-curl \

--with-xsl \

--with-xmlrpc \

--with-pdo-mysql \

--enable-short-tags \

--enable-sockets \

--enable-mbstring \

--enable-static \

--enable-gd \

--enable-ftp \

--enable-fpm \

--enable-xml



# centos

./configure \

--prefix=/usr/local/php7.4.15 \

--with-apxs2=/usr/local/apache2.4.46/bin/apxs \

--with-fpm-user=www \

--with-fpm-group=www \

--with-xmlrpc \

--with-openssl \

--with-zlib \

--with-curl \

--with-xsl \

--with-bz2 \

--with-pdo-mysql \

--with-pdo-sqlite \

--with-iconv-dir \

--with-bz2 \

--with-iconv \

--enable-short-tags \

--enable-sockets \

--enable-mbstring \

--enable-static \

--enable-ftp \

--enable-gd \

--enable-fpm



make && make install 

```

### 复制配置文件

``` base
cp php.ini-production /usr/local/php7.4.15/lib/php.ini

```

### 配置

``` base
#开启配置

cd /usr/local/php/etc

cp php-fpm.conf.default php-fpm.conf

cp php-fpm.d/www.conf.default www.conf

vi php-fpm.d/www.conf.default www.conf


# 修改用户和组，默认为www，没有可以新建，我直接使用nginx
```

## PHP相关

### 完全卸载

1. `rpm -qa|grep php` -- 查找所安装的全部
2. `rpm -e 名字` -- 逐个删除

> 卸载如存在依赖则使用 `rpm -e --nodeps 名字`

---

>`ps aux|grep php-fpm` 查看php-fpm

### Centos8安装php

> [参考](https://www.cnblogs.com/alliancehacker/p/12255445.html)  
> 配置nginx和php时注意  
> nginx.config的fastcgi_pass,php-fpm的www.config文件
> 文件权限问题
> php.ini数据库

### php-fpm

+ `ps aux | grep php-fpm`    查看php-fpm master进程
+ `kill -INT 进程号`    关闭
+ `kill -USR2 进程号`   重启

>`php -i | grep -i extension_dir` 查看extension_dir的目录位置

https://www.jianshu.com/p/30e777609367

## 参考

+ [ubuntu编译安装php需要依赖](https://blog.csdn.net/weixin_30633949/article/details/99948079)