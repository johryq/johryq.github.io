---
title: "Nginx 优化"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:13:51+08:00
draft: false
keywords: []
description: ""
tags: []
categories: ['software']
author: "2332334"

---
<!--more-->

# nginx 优化配置

## 基本配置

### 精简配置文件

``` bash
cd /usr/local/nginx/conf

cp nginx.conf nginx.conf.bak

egrep -v "#|^$" nginx.conf>nginx1.conf

mv nginx1.conf nginx.conf

```

### 拆分配置文件

1. `cd /usr/local/nginx/conf && mkdir vhost`

2. 在`nginx.conf`即主配置`http`模块中添加 `include vhost/*.conf`

3. 在vhost文件夹中创建`server`的配置模块

4. 最后重启nginx即可实现配置文件拆分

### 开启gzip

``` conf

# 添加如下内容即可，在不同的server模块添加实现单独配置

gzip on;

gzip_min_length 1k;

gzip_buffers 4 16k;

gzip_http_version 1.0;

gzip_comp_level 2;

gzip_types text/plain application/x-javascript text/css application/xml;

gzip_vary on;

# gunzip_static on;

```

### 配置日志

``` conf
# http模块去除如下注释

log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '

                      '$status $body_bytes_sent "$http_referer" '

                      '"$http_user_agent" "$http_x_forwarded_for"';

# server模块添加

access_log /usr/local/nginx/logs/access.log commonlog 

```

### expires本地缓存

```conf
location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {

    expires 3d;

}

# 设置本地缓存3d后过期

```

## 安全配置

### 去除版本号

``` conf
# nginx.conf > http模块

server_tokens off; 

# fastcgi.conf   

fastcgi_param  SERVER_SOFTWARE    nginx/nginx;

```

### 设置X-Frame-Options 响应头

X-Frame-Options HTTP 响应头是用来给浏览器指示允许一个页面可否在 &lt;frame&gt;, &lt;iframe&gt; 或者 &lt;object&gt; 中展现的标记。网站可以使用此功能，来确保自己网站的内容没有被嵌到别人的网站中去，也从而避免了点击劫持 (clickjacking) 的攻击。

+ 设置方法： HTTP或Server内加入`add_header X-Frame-Options SAMEORIGIN`
+ X-Frame-Options 有三个值:

  + DENY  
    表示该页面不允许在 frame 中展示，即便是在相同域名的页面中嵌套也不允许。

  + SAMEORIGIN  
    表示该页面可以在相同域名页面的 frame 中展示。

  + ALLOW-FROM uri  
    表示该页面可以在指定来源的 frame 中展示。

## 速度

### 1.开启http2

> [http2](https://www.cnblogs.com/confach/p/10141273.html)

``` conf
listen 443 ssl http2;
```

### 2.调整Cipher优先级

```conf
# 手动启用 cipher 列表
ssl_prefer_server_ciphers on;  # prefer a list of ciphers to prevent old and slow ciphers
ssl_ciphers 'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH';
```

### 3.启用OCSP Stapling

> 即省略https证书验证

```conf
ssl_stapling on;
ssl_stapling_verify on;
ssl_trusted_certificate /path/to/full_chain.pem;
```

测试是否开启该功能

```bash
openssl s_client -connect test.kalasearch.cn:443 -servername kalasearch.cn -status -tlsextdebug < /dev/null 2>&1 | grep -i "OCSP response"
```

### 调整ssl_buffer_sizee

```conf
ssl_buffer_size 4k
```

> 如果需要传输大文件则保持不变即可

### 启用SSL_Session缓存

> 减少TLS(安全传输协议)验证,占用内存存储session,1M=4000连接

```conf
# Enable SSL cache to speed up for return visitors
ssl_session_cache   shared:SSL:50m; # speed up first time. 1m ~= 4000 connections
ssl_session_timeout 4h;
```

## 参考

+ [高性能 Nginx HTTPS 调优 - 如何为 HTTPS 提速 30%](https://kalasearch.cn/blog/high-performance-nginx-tls-tuning/)