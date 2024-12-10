---
title: "Apache"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:08:23+08:00
draft: false
keywords: []
description: ""
tags: ['apache']
categories: ['software']
author: "2332334"

---
<!--more-->

# apache

web服务器

## 包管理器安装

``` bash
# ubuntu
sudo apt install apache2
sudo service apache2 start

# centos
sudo yum install httpd
sudo systemctl enable httpd
sudo systemctl start httpd
```

## 编译安装

相关环境
>ubuntu 18.04
>centos7
>httpd-2.4.46

### 1.下载软件及相关包

+ [apache](http://httpd.apache.org/download.cgi#apache24)

+ [apr](http://apr.apache.org/download.cgi)

+ [apr-util](http://apr.apache.org/download.cgi)

+ [pcre](http://www.pcre.org/)

### 2.安装依赖

``` bash
#ubuntu
sudo apt install gcc zlib1g-dev build-essential openssl -y 

#centos
sudo yum install gcc gcc-c++ zlib-devel openssl libxml2-devel expat-devel -y 

#编译安装的依赖参数
# apr
./configure  --prefix=/usr/local/apr

make && make install

#apr-util
./configure --prefix=/usr/local/apr-util -with-apr=/usr/local/apr

make && make install

#pcre
./configure --prefix=/usr/local/pcre

make && make install
```

---

> centos7报错参考  
> [编译`apr`报错`cannot remove 'libtoolT': No such file or directory`参考](https://zmedu.blog.csdn.net/article/details/107603469)  
> 报错`Another app is currently holding the yum lock; waiting for it to exit...`执行  
>`rm -rf /var/run/yum.pid`

### 3.编译安装

``` bash
tar -zxf httpd-2.4.46
cd httpd-2.4.46

./configure --prefix=/usr/local/apache2.4.46 \
--enable-expires \
--enable-headers \
--enable-modules=most \
--enable-so \
--enable-rewrite \
--with-mpm=worker \
--with-apr=/usr/local/apr \
--with-apr-util=/usr/local/apr-util \
--with-pcre=/usr/local/pcre

make && make install 

/usr/local/apach/bin/apachectl #检查启动服务

```

`httpd: Could not reliably determine the server's fully qualified domain name, using localhost.localdomain. Set the 'ServerName' directive globally to suppress this message`

最后出现以上警告信息即安装成功,

也可使用`lsof -i :80` 查看占用80端口的是不是`httpd`

#### centos7 编译失败

>[参考](https://blog.51cto.com/castiel/2051440)

错误信息如下

``` bash
bapr-1.la -lrt -lcrypt -lpthread -ldl -lcrypt

/usr/local/apr-util/lib/libaprutil-1.so: undefined reference to `XML_GetErrorCode'

/usr/local/apr-util/lib/libaprutil-1.so: undefined reference to `XML_SetEntityDeclHandler'

/usr/local/apr-util/lib/libaprutil-1.so: undefined reference to `XML_ParserCreate'

/usr/local/apr-util/lib/libaprutil-1.so: undefined reference to `XML_SetCharacterDataHandler'

/usr/local/apr-util/lib/libaprutil-1.so: undefined reference to `XML_ParserFree'

/usr/local/apr-util/lib/libaprutil-1.so: undefined reference to `XML_SetUserData'

/usr/local/apr-util/lib/libaprutil-1.so: undefined reference to `XML_StopParser'

/usr/local/apr-util/lib/libaprutil-1.so: undefined reference to `XML_Parse'

/usr/local/apr-util/lib/libaprutil-1.so: undefined reference to `XML_ErrorString'

/usr/local/apr-util/lib/libaprutil-1.so: undefined reference to `XML_SetElementHandler'

```

解决办法

1. yum install libxml2-devel -y

2. `rm -rf /usr/local/apr-util` #删除后重新编译安装

3. 重新之前的两个步骤继续安装即可

> 编译安装 `apr-util` 和 `httpd` 都要 `make clean` 已清除之前的安装信息

## 配置(未测试，仅供参考)

+ 去除版本号

  1. 去除`httpd.conf`的`Include conf/extra/httpd-default.conf`的注释

  2. apachectl graceful 

  3. 修改`httpd-default.conf`的以下两项为：

``` conf
# 第55，65行

ServerTokens Prod

ServerSignature Off
```

+ 开启防盗链

  1. 去除`httpd.conf`中`LoadModule rewrite_module modules/mod_rewrite.so`行的注释

  2. 添加如下内容

``` xml
<IfModule rewrite_module >

    RewriteEngine On

    RewriteCond % {HTTP_REEERER} !^http://DomainName/.*$  [NC]

    RewriteCond % {HTTP_REEERER} !^http://DomainName $  [NC]

    RewriteCond % {HTTP_REEERER} !^http://DomainName / .*$  [NC]

</IfModule>

```

+ 增加对php支持

``` bash
cp /usr/local/apache/conf/httpd.conf httpd.conf.bak

vi  /usr/local/apache/conf/httpd.conf



#在大概390行添加两行内容

AddType application/x-httpd-php .php .phtml

AddType application/x-httpd-php-source .phps

```

## 参考

+ [官方文档](http://httpd.apache.org/docs/2.4/install.html)