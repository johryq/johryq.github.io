---
title: "Typecho-First"
date: 2021-11-08T19:58:32+08:00
lastmod: 2024-12-03T16:35:32+08:00
draft: false
keywords: []
description: ""
tags: ['typecho']
categories: ['blog']
author: "2332334"

---
<!--more-->

# Typecho首次安装

## 经历

这个服务器买了1-2年了,买来也没咋用(就挂了两个python爬虫).

一直想有个自己的Blog,之前尝试了

+ wordpress(搞过一次)

+ Jekyll(搞了许久没咋搞懂)

+ Hexo(尝试过一次)

直到现在莫名使用Typecho,希望能记录下一点有用的东西吧!

<!--more-->

## 我安装的基本需要

+ PHP

+ Nginx

+ Sqlite

### PHP

来来回回装了3-4次,yum安装好了没找到php-fpm.

我又下载源代码装了一次(这次除了`php -v`其他我又搞不来了),最后还是yum装的.

因为使用的是Linux做服务器,对于目录和一些命令还不是太熟悉!

安装的话可以参考[这个](https://www.cnblogs.com/alliancehacker/p/12255445.html),虽然感觉最后安装完有点问题,但也算一次成功的尝试嘛.

---

安装完后就主要php-fpm和nginx的配置了!

>关于php-fpm: 因为nginx并不能解析php,所以需要php-fpm解析后由nginx中转.

1. 使用`chmod -R 777 你的网站位置`给予权限

2. 修改以下配置文件(yum安装)

+ /etc/php.ini

+ /etc/php-fpm.d/www.conf (设置 `listen = 127.0.0.1:9000` 需要与nginx的 fastcgi_pass 一致)

现在还有就是启动 php-fpm 的时候会出现权限不足的情况(使用sudo)

我的临时解决办法就是自己手动创建那个文件夹再运行就ok了.

我想到的解决办法是就该配置文件去掉创建的那个文件夹

### Nginx配置

``` config

location ~ ^.+.php {

		proxy_set_header Host $http_host;

		proxy_set_header X-Forward-For $remote_addr;

		fastcgi_split_path_info ^((?U).+\.php)(/?.+)$;

		fastcgi_param  SCRIPT_FILENAME  你的网站主目录$fastcgi_script_name;

		fastcgi_param PATH_INFO $fastcgi_path_info;

		fastcgi_param PATH_TRANSLATED $document_root$fastcgi_path_info;

		fastcgi_index  index.php;

		fastcgi_pass   127.0.0.1:9000;

		include        fastcgi_params;

        }

```

## 安装好后数据库配置出现错误(使用的sqlite3)

目录权限问题 || 我在目录手动创建一个数据库后就没问题了

## 最后除了访问 .php 页面其他全部404

nginx配置之前是

```conf

 location ~ \.php$ {

    .....

}

```

改成

```conf

location ~ ^.+.php {

    .....

}

```

就ok了

> 参考地址

+ Centos8（Liunx） 中安装PHP7.4 的三种方法和删除它的三种方法

[https://www.cnblogs.com/alliancehacker/p/12255445.html](https://www.cnblogs.com/alliancehacker/p/12255445.html)

+ typecho安装

[https://www.jianshu.com/p/30e777609367](https://www.jianshu.com/p/30e777609367)