---
title: "V2ray"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T13:26:59+08:00
draft: false
keywords: []
description: ""
tags: []
categories: ['software']
author: "2332334"
---
<!--more-->

# V2ray

> 自动脚本 `bash <(curl -s -L https://git.io/v2ray.sh)`

[参考链接](https://www.wrysmile.cn/V2Ray-02.html)

## 安装

``` bash

# 切换root安装
su

yum -y install wget unzip netcat

bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh)

```

[参考安装文档][1]

## 配置

**[配置参考文档][2]**

### 简单配置 `vmess-tcp`

#### 第一步

``` bash
cat /proc/sys/kernel/random/uuid 

# 生成UUID

vi config.json 

# 创建配置文件

```

#### 第二步

``` json
{

    "log": {

        "loglevel": "warning"

    },

    "routing": {

        "domainStrategy": "AsIs",

        "rules": [

            {

                "ip": [

                    "geoip:private"

                ],

                "outboundTag": "blocked",

                "type": "field"

            }

        ]

    },

    "inbounds": [

        {

            "port": 1234,                  //更改端口号

            "protocol": "vmess",

            "settings": {

                "clients": [

                    {

                        "id": "",           //填写UUID

                        "alterId": 64

                    }

                ]

            }

        }

    ],

    "outbounds": [

        {

            "protocol": "freedom"

        },

        {

            "protocol": "blackhole",

            "tag": "blocked"

        }

    ]

}

```

写入以上配置并启动服务即可: `v2ray start` 或者 `sudo systemctl start v2ray`

最后找了n个测试vmess+tls+websocket失败!

相关协议

+ 用于代理的 VMess 和 Shadowsocks 协议

+ 用于直连的 freedom 协议

+ 以及用于阻止连接的 blackhole 协议

### WebSocket+TLS+Web

v2服务器配置

``` json
{
  "inbounds": [
    {
      "port": 10000,
      "listen":"127.0.0.1",//只监听 127.0.0.1，避免除本机外的机器探测到开放了 10000 端口
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "c4a5965f-bb61-420b-af5b-d6acaaaaa32c",
            "alterId": 64
          }
        ]
      },
      "streamSettings": {
        "network": "ws",
        "wsSettings": {
        "path": "/ray"
        }
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {}
    }
  ]
}
```

nginx配置

```conf
server {
  listen  443 ssl;
  ssl on;
  ssl_certificate       /etc/nginx/cert/domain.cer;
  ssl_certificate_key   /etc/nginx/cert/domain.key;
  ssl_protocols         TLSv1 TLSv1.1 TLSv1.2;
  ssl_ciphers           HIGH:!aNULL:!MD5;
  server_name           mydomain.me;
        location /ray { # 与 V2Ray 配置中的 path 保持一致
        proxy_redirect off;
        proxy_pass http://127.0.0.1:10000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $http_host;

        # Show realip in v2ray access.log
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
}
```

客户端

> 导入v2rayN自定义配置无法使用,仅供参考进行手动配置

``` json
{
  "inbounds": [
    {
      "port": 1098,
      "listen": "127.0.0.1",
      "protocol": "socks",
      "sniffing": {
        "enabled": true,
        "destOverride": ["http", "tls"]
      },
      "settings": {
        "auth": "noauth",
        "udp": false
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "vmess",
      "settings": {
        "vnext": [
          {
            "address": "domain.com",
            "port": 443,
            "users": [
              {
                "id": "c4a5965f-bb61-420b-af5b-d6ac1111132c",
                "alterId": 64
              }
            ]
          }
        ]
      },
      "streamSettings": {
        "network": "ws",
        "security": "tls",
        "wsSettings": {
          "path": "/ray"
        }
      }
    }
  ]
}
```

## 更多参考资料

+ [参考资料1][3]
+ [ebSocket+TLS+Web](https://toutyrater.github.io/advanced/wss_and_web.html)

  [1]:https://github.com/v2fly/fhs-install-v2ray/blob/master/README.zh-Hans-CN.md

  [2]:https://github.com/v2fly/v2ray-examples

  [3]:https://toutyrater.github.io/