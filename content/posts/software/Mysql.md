---
title: "Mysql"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T08:55:16+08:00
draft: false
keywords: []
description: ""
tags: []
categories: ['software']
author: "2332334"

---
<!--more-->

# Mysql

> 2021年6月19日

## 修改密码

```bash
vi /etc/my.cnf

# 添加免密登录
[mysqld]
skip-grant-tables

sudo systemctl restart mysqld

mysql

# 进入mysql
flush privileges;

# mysql5.7
update user set authentication_string = password(“root”) where user = “root”;

## mysql8
ALTER user 'root'@'localhost' IDENTIFIED BY 'newpassword';
flush privileges;
```

> 最后注销配置文件的免密行

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