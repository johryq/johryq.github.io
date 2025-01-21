---
title: "Mysql"
date: 2021-06-19T19:58:55+08:00
lastmod: 2025-01-17T08:55:16+08:00
draft: false
keywords: []
description: ""
tags: []
categories: ['software']
author: "2332334"

---
<!--more-->

# Mysql基础信息

## 修改密码

```bash
vi /etc/my.cnf

# 添加免密登录
[mysqld]
skip-grant-tables

sudo systemctl restart mysqld

mysql -u root -p

# 修改密码 5.7
update user set authentication_string = password(“root”) where user = “root”;

ALTER USER 'root'@'%' IDENTIFIED BY 'pwd';

ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'pwd';

# 最新的使用的认证方式，若要使用 mysql_native_password 需修改my.cnf 配置启用
ALTER USER 'root'@'%' IDENTIFIED WITH caching_sha2_password BY 'pwd';

update user set host='%' where user='root';

flush privileges;
```

> WITH GRANT OPTION 添加这个可使用户权限可以继承  
> 最后注销配置文件的免密行

# 管理

```bash
CREATE USER 'john'@'localhost' IDENTIFIED BY 'password123';

# 授权
GRANT ALL PRIVILEGES ON test_db.* TO 'john'@'localhost';
GRANT ALL ON *.* TO 'u'@'%' IDENTIFIED BY 'pwd' WITH GRANT OPTION;

SHOW GRANTS FOR 'root'@'%';

REVOKE ALL PRIVILEGES ON test_db.* FROM 'john'@'localhost';

DROP USER 'root'@'%';

ALTER USER 'username'@'host' IDENTIFIED BY 'new_password';
```


## Database

建库

``` msyql
# 查看字符集
show character set;
# 查看排序规则
show collation; 

CREATE DATABASE [IF NOT EXISTS] <数据库名>
[[DEFAULT] CHARACTER SET <字符集名>] 
[[DEFAULT] COLLATE <排序规则名>];
```

### 排序规则

| 名称 | 解析 |
| --- | --- |
| ci | 大小写不敏感 |
| cs | 敏感 |
| bin | 二元 |
| &nbsp; | &nbsp; |
| unicode | 支持扩展,准确 |
| general | 不支持扩展,快速 |

## 查询

## 删除

## 增加

## 修改