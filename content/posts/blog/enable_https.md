---
title: "Enable_https"
date: 2022-01-10T00:10:13+08:00
lastmod: 2024-12-03T16:34:13+08:00
draft: false
keywords: []
description: ""
tags: ['https','acme.sh']
categories: ['blog']
author: "2332334"

---

# acme.sh

<!--more-->

## 一. 证书提供商

- [Let’s Encrypt][2]
- [ZeroSSL](https://zerossl.com/)

> 3.0 后默认 `ZeroSSL` ,相比 `Let’s Encrypt` `ZeroSSL`拥有 web 控制面板,没有速率限制,不存在同一 IP 多次申请 SSL 证书被限制的问题

```bash
acme.sh --set-default-ca  --server zerossl
```

## 二.[acme.sh][1]安装及基本使用

1.安装脚本

```bash
# centos可能需要安装
yum install epel-release socat -y

curl  https://get.acme.sh | sh

# 设置别名
alias acme.sh=~/.acme.sh/acme.sh
```

2.使用 DNS 直接解析

1. 使用[一些服务商的 DNS API][5]

2. 手动设置 DNS 记录,但是不支持自动更新所以不推荐

这里使用 DNSAPI 来设置:

- [阿里云的申请地址](https://ak-console.aliyun.com/#/accesskey)
  - Access Key ID
  - Access Key Secret
- [腾讯云 DNSpod](https://console.dnspod.cn/account/token)
  - 密钥 ID
  - 密钥 Token

```bash

vi ~/.acme.sh/account.conf

# 阿里云添加

export Ali_Key="xxx"

export Ali_Secret="xxxxxx"

# 腾讯云添加

export DP_Id="xxx"

export DP_Key="xxxxxxx"

```

3.生成证书

```bash
# nginx
acme.sh --issue  -d mydomain.com   --nginx

# 无web服务器验证,保证本地80端口可用
acme.sh  --issue -d mydomain.com   --standalone

# 腾讯dnspod
acme.sh --issue --dns dns_dp -d *.mydomain.com

# 阿里云
acme.sh --issue --dns dns_ali -d *.mydomain.com
```

4.复制证书

```bash
sudo acme.sh --install-cert -d "*.mydomain.com" \
--key-file       /usr/local/nginx/cert/*.mydomain.com.key  \
--fullchain-file /usr/local/nginx/cert/*.mydomain.com.cer \
--reloadcmd     "service nginx force-reload"
```

> 如果提示权限问题可以修改配置文件所在文件夹权限

5.最后配置`nginx`的`ssl`即可

### 脚本相关命令

```bash
# 自动更新
acme.sh  --upgrade  --auto-upgrade

# 关闭自动更新
acme.sh --upgrade  --auto-upgrade  0

#查看证书
acme.sh --list

acme.sh remove 域名
```

## 参考链接

- [letsencrypt 官网][2]

- [acme.sh 文档][3]

- [Let's Encrypt 证书申请及配置][4]

- [acme.sh DNS-API 支持服务器文档][5]

- [Let’s Encrypt 通配符证书,泛域名 https 证书申请配置][6]

  [1]: https://github.com/acmesh-official/acme.sh
  [2]: https://letsencrypt.org/
  [3]: https://github.com/acmesh-official/acme.sh/wiki/%E8%AF%B4%E6%98%8E
  [4]: https://www.jianshu.com/p/1a792f87b6fe
  [5]: https://github.com/acmesh-official/acme.sh/wiki/dnsapi
  [6]: https://www.cnblogs.com/-mrl/p/10723988.html
