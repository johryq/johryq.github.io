---
title: "Fail2ban"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:13:00+08:00
draft: false
keywords: []
description: ""
tags: ['ssh']
categories: ['software']
author: "2332334"

---
<!--more-->


# Fail2ban

[v2][3]上看到了这个软件,做个笔记:

## 简介

> `grep 'Failed' /var/log/auth.log` 查看登录失败的IP

对于异常SSH的IP进行管控;
若使用密钥登录可不使用

实质是个日志解析器,通过扫描相应日志然后进行正则匹配,当匹配结果到一定数量,就采取相应动作,如防火墙对异常IP进行限制,发送邮件等.

## 安装与基本配置

安装要求

+ 安装python2.6/3.2及以上版本(这是款python写的软件,软件0.6x以上版本重写)

+ 至少一个防火墙软件:iptables或者shorewall,之前看了iptables就使用它吧

安装

``` bash
#Ubuntu
sudo apt install fail2ban mailutils

---

使用Github源码安装

git clone https://github.com/fail2ban/fail2ban.git
cd fail2ban
sudo python setup.py install 

---

# Centos
sudo yum -y install epel-release 
sudo yum -y install fail2ban  
fail2ban-client -V  #查看安装版本,并确定是否安装完成
```

> [阿里epel源地址](https://developer.aliyun.com/mirror/epel)

## 使用与相关命令

配置通过`/etc/fail2ban/jail.conf`文件配置,但不推荐直接修改;  

使用时自定义`local`后缀的文件,软件运行会先加载`jail.conf`再读取自定义的配置信息(如有相同项,local会覆写conf中的配置)  

官方的简单配置:

``` conf
[ssh-iptables]

#enabled  = false

enabled  = true

filter   = sshd

action   = iptables[name=SSH, port=ssh, protocol=tcp]

#          mail-whois[name=SSH, dest=yourmail@mail.com]

#logpath  = /var/log/sshd.log

logpath  = /var/log/auth.log|

maxretry = 5

```

相关命令  

该软件由服务器端与客户端组成(cs):

+ fail2ban-server

+ fail2ban-client

|参数|解析|

|---|---|

|`fail2ban-server` | &nbsp; |

| `/etc/init.d/fail2ban start` | 启动 |

| `fail2ban-client` | &nbsp; |

| `reload` | 重新加载配置 |

| `status` | 查看运行的监控服务数量和列表 |

## 参考资料

+ [官网][1]

+ [Github地址][2]

+ [Fail2ban防暴力破解][3]
+ [使用fail2ban防范Linux服务器SSH暴力登录尝试攻击](https://jlice.top/p/7v45r/)

  [1]:http://www.fail2ban.org/wiki/index.php/Main_Page

  [2]:https://github.com/fail2ban/fail2ban

  [3]:https://www.cnblogs.com/lxfpy/p/10862204.html

