---
title: "SQL"
date: 2025-10-05T23:27:04+08:00
lastmod: 2025-10-05T23:27:04+08:00
draft: true
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
# cover:
#     image: "" # image path/url
#     alt: "<alt text>" # alt text
#     caption: "<text>" # display caption under cover
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/<path_to_repo>/content"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

# SQL

SQL（Structured Query Language，结构化查询语言）
管理和操作数据库的标准话语言

<!--more-->

## 一. 基本使用

```sql
SELECT * FROM TABLE;

DELETE FROM TABLE WHERE ID =1;

DROP TABLE WHERE ID =1;

UPDATE TABLE SET ROW1=VALUE1,ROW2=VALUE2 WHERE ID = 1;


```


## 二. 进阶语法

### 二.1 TOP
```SQL
-- MYSQL
SELECT TOP 10 FROM TABLE;

-- MYSQL
SELECT * FROM TABLE LIMIT 10;

-- ORACLE
SELECT * FROM (SELECT * FROM TABLE ORDER BY ID) WHERE ROWNUM <=10;
SELECT * FROM TABLE FETCH FIRST 10 ROWS ONLY;
```
> 查询使用 order by 后有 b 树索引，可能更加更快

### 二.2 JOIN

```SQL
-- INNER JOIN = JOIN 返回两表交集，无交集则不返回
SELECT * FROM table1 t1
INNER JOIN table2 t2 ON t1.ROW2 = t2.ROW2

-- LEFT JOIN = LEFT OUTER JOIN 保留左表，右表无值则为NULL；右表有值，左表无值，则不显示;右查询则相反
SELECT * FROM table1 t1
LEFT JOIN table2 t2 on t1.ROW2 = t2.ROW2

-- FULL JOIN = FULL OUTER JOIN 联查两个表返回所有列结果
SELECT * FROM table t1
FULL JOIN table t2 ON t1.ROW2 = t2.ROW2
```

### 二.3 UNION/UNION ALL

UNION  合并两表，并去除两表重复值

使用要求和注意事项：
1. 两表列数相同
2. 两表数据类型相同
3. 默认使用第一个 SELECT 的列名
4. UNION 为去重复
5. UNION ALL 不会去重

```sql
-- 聚合多个来源数据
SELECT '订单' AS 来源, COUNT(*) AS 数量 FROM orders
UNION ALL
SELECT '客户' AS 来源, COUNT(*) FROM customers
UNION ALL
SELECT '库存' AS 来源, COUNT(*) FROM inventory;
```
> 使用方向： 聚合数据去重查询，两表合并，主从表同步检查

## 三. CREATE

```sql
CREATE DATABASE DBNAME;

CREATE TABLE TABLENAME(
  ROW_NAME ROW_TYPE,
)
```

### 三.1 约束

| 关键字 | 解析 | 示例 |
|:------------|:------------|-----|
| NOT NULL    | 不为空      |
| UNIQUE      | 唯一        |
| PRIMARY KEY | 主键        |
| FOREIGN KEY | 外键        |
| CHECK       | 数值检查     |
| DEFAULT     | 默认值       |
| INDEX       | 索引         |

```sql
CREATE TABLE TABLE_NAME(
  ID INT NOT NULL UNIQUE PRIMARY KEY AUTO_INCREMENT,
  Name VARCHAR(100) UNIQUE,
  FOREIGN KEY (userID) REFERENCES USER_INFO (userID)
  CreateDate DATE DEFAULT GETDATE()
  Age INT CHECK (Age>=18)
)
```

## 四. 事务


## 参考

+ [菜鸟](https://www.runoob.com/sql/sql-tutorial.html)
+ 