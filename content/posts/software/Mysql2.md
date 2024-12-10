---
title: "Mysql2"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:11:48+08:00
draft: false
keywords: []
description: ""
tags: []
categories: ['software']
author: "2332334"

---
<!--more-->

# Mysql

> 更对内容还请参考[官方文档][2]

## 1.centos安装mysql

```bash
sudo dnf install @msyql

# 初始化mysql会自定生成密码在控制台
mysqld --initialize --user=mysql --console

# 初始化mysql，无密码root用户
mysqld --initialize-insecure --user=mysql --console
```

> 启动mysql服务后可使用`mysql_secure_installation`进行一些安全配置

### 一些问题

#### 1. 修改密码

``` bash
vi /etc/my.cnf.d/mysql-server.cnf
# skip-grant-tables #添加该行
sudo systemctl restart mysqld
mysql -u root -p

#---mysql
use mysql;
flush privileges;

# 8.0以前
update user set password=password('新密码') where user='用户名';
# or
update mysql.user set authentication_string=password('新密码') where user='用户名';
# 8.0以后版本
ALTER USER '用户名'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码';

flush privileges;
exit；
```



---



## OlD

## 安装

环境
> ubuntu 18.04
> centos 7
> msyql 5.7.33

1.`apt` 安装 `mysql`

``` bash
sudo apt install mysql.server

```

2.初始化 `mysql`

``` bash
mysql_secure_installation
mysqld --initialize-insecure
mysqld --initialize --console
```

3.更改 root 登录

``` bash
mysql -u root -p

use mysql;

update user set host='%' where user='root';

flush privileges; #刷新权限

```

4.修改配置并重启服务(注释掉 `bind-address = 127.0.0.1` )

``` bash
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf

sudo systemctl restart msyql.server
```

以上

### 遇到的小问题

刚装好并修改 `host` 为 `%` 时 sql 语句执行有错误,

但是执行通过了,退出 mysql 后普通用户无法登录;

查询 mysql 库 user 表看到有两个 root 用户,删除一个即可.

## 二进制包安装

> mysql5.7.33

1.[下载tar包][1]

>mysql-5.7.33-linux-glibc2.12-x86_64.tar.gz  
>Linux - Generic

2.安装相关依赖

``` bash
#ubuntu

sudo apt install zlib1g-dev build-essential libncurses5  libncurses5-dev libaio1 libaio-dev  libnuma1  libnuma-dev -y 



# centos

sudo yum install zlib-devel gcc-c++ ncurses ncurses-devel libaio libaio-devel -y

```

3.新建用户，创建目录

``` bash
#新建用户，M不创建目录s不允许登录
useradd mysql -s /sbin/nologin -M 

tar -zxf 下载的 .tar.gz 文件  -C /usr/local/

ln -s 上面解压后的目录 /usr/local/mysql

#创建数据目录
mkdir -p /usr/local/mysql/data 

#更改文件夹组及归属
chown -R mysql.mysql /usr/local/mysql

```

4.配置

``` bash
cd /usr/local/mysql

bin/mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data

# 最后会输出初始密码
```

4.配置服务和环境变量及配置文件

``` bash
#配置服务
cp support-files/mysql.server /etc/init.d/mysqld

chmod 700 /etc/init.d/mysqld

#第46-47行设置程序目录和数据目录
vi /etc/init.d/mysqld 

# 配置环境变量
cat>/etc/profile.d/mysql.sh<<EOF
export PATH=/usr/local/mysql/bin:\$PATH
EOF

或者

echo 'export PATH=/usr/local/mysql/bin:$PATH' >> /etc/profile.d/mysql.sh

# 刷新
source /etc/profile.d/mysql.sh

# 写入配置文件(可选操作)

# mysql5.7.18 以后不提供my-default.cnf,即不需要设置my.cnf即可运行

cat >/etc/my.cnf<<EOF

[mysqld]

basedir=/usr/local/mysql

datadir=/usr/local/mysql/data

port=3306

server_id=1

socket=/tmp/mysqld.sock

character-set-server=utf8

log-error=/var/log/mysqld.log

pid-file=/tmp/mysqld.pid

[mysql]

socket=/tmp/mysqld.sock

[client]

socket=/tmp/mysqld.sock

EOF

```

5.数据库改密

``` bash
/etc/init.d/mysqld start 

mysql -u root -p #输入刚才输出的密码

set password for root@localhost=password('新密码');

UPDATE mysql.user SET password=PASSWORD("新密码") WHERE user='root' and host='localhost';

flush privileges;

```

## 参考目录

+ [官方文档][2]

+ [CentOS 8 安装MySQL 8.0](https://www.cnblogs.com/kasnti/p/11929030.html)

+ [ubuntu18.04 安装mysql](https://www.cnblogs.com/xyabk/p/11758288.html)

+ [centos 二进制包安装mysql](https://www.cnblogs.com/diantong/p/11088901.html)

+ [msyql编译安装](https://www.cnblogs.com/Csir/p/6770023.html)

+ [my.cof](https://blog.csdn.net/lone7dehao/article/details/99548803)

[1]:https://dev.mysql.com/downloads/mysql/
[2]:https://dev.mysql.com/doc/refman/8.0/en/