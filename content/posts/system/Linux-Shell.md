---
title: "Linux Shell"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T13:23:01+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# shell脚本

与内核通信的命令行环境，命令解释器

## 常见shell种类

+ Bourne Shell（/usr/bin/sh或/bin/sh）

+ Bourne Again Shell（/bin/bash）

+ C Shell（/usr/bin/csh）

+ K Shell（/usr/bin/ksh）

+ TENEX C Shell（tcsh）

+ Friendly Interactive Shell（fish）

+ Z Shell（zsh）

## start

文件开头,用于指出使用的shell

```bash

#!/bin/bash

```

该语句为第一行首行，之后是脚本！

最后使用 `.sh` 保存,执行时先要 `chmod +x ./脚本`,然后执行`./文件名.sh`

## 语法

### 变量

命名规则基本与其他语言相似

```bash

variable="bianliang" # =两边不能有空格,赋值不加$

echo $variable

echo ${variable}  #可加可不加 `{}` ,推荐加

```

只读变量: `readonly variable`

删除变量: `unset variable`

### 数据类型

#### 字符串

> `variable="字符串9527"`

使用`单引号`或者`双引号`都可以,推荐双引号

获取字符串长度: `echo ${#variable}`

截取字符串(从第二个截取到第四个): `${variable:1:4}`

查找字符串:

```bash

`expr index "$variable" 查找的字符串

```

#### 数组

+ 支持一维数组

+ 0下标开始

+ 支持数组元素运行,但是值应大于0

```bash

array=(var1 var2 ... varn)  #定义数组,也可一行一个值

echo ${array[n]}  #输出数组n的值

echo ${array[@]}  #输出所有元素

echo ${#array[*]}  #输出数组个数,加`#`及输出长度

```

### 注释

```bash

# 单行注释

# 多行注释
:<<EOF

注释内容

EOF

```

> 除了EOF,也可使用其他符号,只需首尾相同即可

### 向脚本传递参数

| 参数 | 解释 |
|---|---|
| `$n` | 第n个参数 |
| `$#` | 传递参数个数 |
| `$$$` | 脚本运行UID |
| `$!` | 后台运行最后一个进程UID |
| `$*` | 传递的所有参数,必须由`"`包围. |
| `$@` | 同上,参数换行 |
| `$-` | shell当前选项,与set功能相同 |
| `$?` | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误 |

### 运算符

#### 算数运算符

> 原生bash不支持,可使用命令 `awk` 或 `expr` 等(`expr`为表达式计算工具)

```bash

val=`expr 2 + 2`

echo "$val"

```

> `*`乘号前加上转义(`\`)

#### 关系运算符

> 只能判断数字,包括字符串内的数字.返回true or false

| 运算符 | 解析(成立均返回`true`) |
|---|---|
| `-eq` | == |
| `-ne` | != |
| `-gt` | > |
| `-lt` | < |
| `-ge` | >= |
| `-le` | <= |

> `ex: if [$a -eq $b]`

#### 布尔与逻辑运算符

| 运算符 | 解析(成立均返回`true`) |
|---|---|
| 布尔 | &nbsp; |
| `!` | 非 |
| `-o` | 或 |
| `-a` | 与 |
| 逻辑 | &nbsp; |
| `&&` | AND |
| `两个竖线` | OR |

#### 字符串运算符

| 运算符 | 解析 |
|---|---|
| `=` | 字符串是否相等 |
| `!=` | 不等 |
| `-z` | 长度是否为`0` |
| `-n` | 长度是否不为`0` |
| `$` | 字符串是否为空;ex: `$a` |

#### 文件属性测试

| 运算符 | 解析 |
|---|---|
| `-b file` | 是否块设备文件 |
| `-c` | 是否字符设备文件 |
| `-d` | 是否目录 |
| `-f` | 是否普通文件 |
| `-g` | 是否设置SGID位 |
| `-k` | 是否设置粘着位(Sticky Bit) |
| `-p` | 是否有名管道 |
| `-u` | 是否设置SUID位 |
| `-r` | 是否可读 |
| `-w` | 是否可写 |
| `-x` | 是否可执行 |
| `-s` | 是否为空(文件大小是否为0) |
| `-e` | 文件/目录是否存在 |
| `-S` | 是否socket |
| `-L` | 文件是否是个链接 |

### 判断

```bash
if 条件
then
  命令
else
  命令
fi

# elseif

if 条件
then
  命令
elif 命令
then
  命令
fi

#case

case 变量 in 
 值1)
  命令
  ;;
 值2)
  命令
  ;;
esac
```

> break continue

### 循环

```bash
# for

for var in ary[]
do
  命令
done

# while

while (( $val<=5 ))
do
  命令
done

# do while

until 判断
do
  命令
done

```

### 函数

```bash

main(){
  巴拉巴拉
  return 1
}

main

```

> 参数传递同上

## 参考资料

[菜鸟教程-shell][1]

  [1]:https://www.runoob.com/linux/linux-shell.html

[阮一峰bash脚本教程](https://wangdoc.com/bash/intro)
