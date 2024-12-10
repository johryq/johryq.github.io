---
title: "Nginx"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:12:38+08:00
draft: false
keywords: []
description: ""
tags: []
categories: ['software']
author: "2332334"
---
<!--more-->

# nginx 安装

[安装新版本nginx](https://nginx.org/en/linux_packages.html)

## 编译安装

> ubuntu18.04  
> nginx 1.18.0

### 1.下载[nginx.tar.gz](http://nginx.org/en/download.html)

### 2.安装依赖

```bash
#centos
sudo yum install gcc gcc-c++ automake pcre pcre-devel zlib zlib-devel openssl openssl-devel -y

#ubuntu
sudo apt install build-essential libpcre3 libpcre3-dev  zlib1g zlib1g-dev libssl-dev -y

# 添加用户
useradd -s /sbin/nologin -M nginx

```

关于这些包:

- gcc
- pcre pcre-devel pcre 是一个 perl 库，包括 perl 兼容的正则表达式库，nginx 的 http 模块使用 pcre 来解析正则表达式
- zlib zlib-devel zlib 库提供了很多种压缩和解压缩方式 nginx 使用 zlib 对 http 包的内容进行 gzip
- openssl openssl-devel openssl 是 web 安全通信的基石

### 3.编译安装

`tar -zxvf 压缩文件名` 解压并进入该文件夹

```bash
./configure \
--user=nginx \
--group=nginx \
--prefix=/usr/local/nginx-1.18.0 \
--with-http_ssl_module \
--with-http_sub_module \
--with-http_stub_status_module \
--with-http_gzip_static_module \
--with-http_v2_module \
--with-pcre

make && make install

```

编译参数解析

- `./configure --prefix=` 指定安装路径

- `--conf-path=` 配置文件路径

- `--add-module` 为添加的第三方模块

- `--with..._module` 表示启用的 nginx 模块

## 配置

### location 

```conf
location = / {}
# 域名后面没有路径时执行

location / {}
# 所有访问都匹配，如果被上一种处理则不执行
```

### 与 php 通信（主要依赖`php-fpm`）

1.php 设置

```conf
#www.conf

listen = 127.0.0.1:9000

listen = /run/www.sock

#两种其一即可但是要与nginx的fastcgi_pass配置相同
```

2.测试配置

`/usr/local/php/sbin/php-fpm -t`

3.nginx 配置文件基础配置

备份原始配置

```base
cd /usr/local/nginx

cp conf/nginx.conf conf/nginx.conf.bak
```

修改配置文件

```conf
# http模块添加如下配置

fastcgi_connect_timeout 300;

fastcgi_send_timeout 300;

fastcgi_read_timeout 300;

fastcgi_buffer_size 64k;

fastcgi_buffers 4 64k;

fastcgi_busy_buffers_size 128k;

fastcgi_temp_file_write_size 128k;

# 添加server模块进行测试

	server {
		listen 80;
		server_name 192.168.137.131;
		location ~ .*\.(php|php5)?$
		{
			fastcgi_pass 127.0.0.1:9000;
			fastcgi_index index.php;
			include fastcgi.conf;
		}
	}

```

## 基本使用

- `nginx -t` 检查 nginx 配置

- `nginx目录/sbin` -> `./nginx` 启动 nginx

- `./nginx -s reload` 重启 nginx

- `ps -ef|grep nginx` 查看 nginx 信息 并使用一下命令停止

```base
    从容停止   kill -QUIT 主进程号

　　快速停止   kill -TERM 主进程号

　　强制停止   kill -9 nginx
```

### 卸载 nginx

- `whereis nginx` 查找 nginx 相关文件

- `find / -name nginx` 删除相关文件

- `yum remove nginx`

[重新编译并添加模块](https://www.cnblogs.com/ghjbk/p/6744131.html)
[编译](

## 更多参考

- [nginx 官方文档](http://nginx.org/en/docs/)

- linux 系统运维指南（民工哥）

- [如何隐藏 nginx 版本号](https://blog.csdn.net/liuxl57805678/article/details/88238271)
