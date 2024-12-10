---
title: "Mongodb"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:10:55+08:00
draft: false
keywords: []
description: ""
tags: ['']
categories: ['software']
author: "2332334"

---
<!--more-->

# MongoDB

`c++`开发的 文档数据库(键值对)

## win使用

> 添加环境变量`C:\Program Files\MongoDB\Server\5.0\bin`

### mongodb服务

安装mongodb服务

```bash
mongod.exe --config "C:\Program Files\MongoDB\Server\5.0\bin\mongod.cfg" --install

mongod.exe --remove
# 移除服务
```

> 默认安装服务并启动会因为权限原因无法启动

解决方法

``` bash
# 管理员方式启动powershell
sc delete MongoDB
# 或者试试 mongod.exe --remove 删除服务
mongod --install -f "C:\Program Files\MongoDB\Server\5.0\bin\mongod.cfg"
net start mongodb
```

> 此后即可通过服务启动mongoBD

### 命令行运行mongodb服务器

``` bash
cd C:\
md "\data\db"
# 创建数据目录

mongod.exe --dbpath="c:\data\db"
mongo
```

> 进入mongo之后运行的是一个`javascript shell`

## 参考

+ [【已解决】MongoDB问题 -Windows无法启动MongoDB服务，错误1053（适用win10）](https://sevieryang.blog.csdn.net/article/details/84564758)