---
title: "VscodeServer"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T13:29:07+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# vscode on browser

> [github:code-server](https://github.com/coder/code-server)  
> [coder:商业版](https://coder.com)

## 安装

一. 自动化脚本

```bash
# test
curl -fsSL https://code-server.dev/install.sh | sh -s -- --dry-run

# install
curl -fsSL https://code-server.dev/install.sh | sh
```

二. 

## nginx 配置

``` conf
server {
    listen 443 ssl;                     # 监听端口
    server_name code.alanyf.site;       # 域名
    # nginx请求日志地址
    access_log  /usr/local/webserver/nginx/logs/code.access.log;

    # ssl证书地址
    ssl on;
    ssl_certificate      /data/cert.pem;    # pem文件的路径
    ssl_certificate_key  /data/cert.key;    # key文件的路径
    
    # ssl验证相关配置
    ssl_session_timeout  5m;             # 缓存有效期
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;                # 加密算法
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # 安全链接可选的加密协议
    ssl_prefer_server_ciphers on;        # 使用服务器端的首选算法

    location / {
        proxy_pass  https://localhost:8084;
        proxy_redirect     off;
        proxy_set_header   Host             $host;          # 传递域名
        proxy_set_header   X-Real-IP        $remote_addr;   # 传递ip
        proxy_set_header   X-Scheme         $scheme;        # 传递协议
        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
        # code-server的websocket连接需要Upgrade、Connection这2个头部
        proxy_set_header   Upgrade          $http_upgrade;
        proxy_set_header   Connection       upgrade; 
        proxy_set_header   Accept-Encoding  gzip;
    }
}

# http请求直接重定向到https
server {
    listen 80;                          # 监听端口
    server_name code.alanyf.site;       # 域名
    return 301 https://$server_name$request_uri;
}
```

## 参考链接

+ [简单3步部署code-server(vscode网页版)](https://juejin.cn/post/6966772881552310303)