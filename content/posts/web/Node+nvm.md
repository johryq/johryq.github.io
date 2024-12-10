---
title: "node nvm"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:05:21+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->
# Node

## node nvm

## 基础介绍

浏览器js解析引擎解析我们写的js执行浏览器的一些API（BOM，DOM，AJAX）

node.js 基于V8的js引擎

node.js 中无法调用BOM DOM AJAX

+ Chrome    V8
+ Firefox   OdinMonkey（奥丁猴）
+ Safri     JSCore
+ IE        Chakra（查克拉）

## 内置module

### fa

操作文件

```js
const fs = require('fs')

fs.readFile(path,[opeion],callback)

fs.writeFile()
//1. 只可创建文件，不可创建路径
//2. 覆盖写入


__dirname
//当前文件所处目录
```

### path

```js
const path = require('path')

path.join()

path.basename()

path.extname()
```

### HTTP

基本HTTP服务创建

```js
const baseHttp = require('http')

const httpServer = baseHttp.createServer()

httpServer.on('request',function(req,res){
    console.log('request path:' + req.url + 'request method: ' + req.method )
    req.setHeader('ContentType','text/html;charset=utf8')
    res.end('hello world')
})

httpServer.listen(80,function(){console.log('run httpserver in 80')})

```

## 模块化

### 模块化好处

+ 复用
+ 可维护性
+ 按需调用

> require 调用模块后即执行该模块的代码

模块作用域 防止全局变量污染

### module对象

```js
// 导出对象
module.exports()

exports.method = ()=>{}
```

> 两者都指向module.exports 对象，最终以module.exports 为准

### CommonJS

1. 每个模块内部，module 变量代表当前模块

2. module 变量是一个对象，它的 exqorts 属性是对外接口

3. 加载某模块，就是加载 module.exports 属性，require 用于加载模块

### 加载机制

1. 首先从缓存中加载

2. 加载自定义模块需 `./ ../`路径标识符

3. 第三方模块逐级往上查找至根目录

## npm 与 包

### 版本号

2.24.0

大版本
功能版本
bug修复版本

前面版本号增长了，后面归零

### pockage.json 节点

devDependencies 开发过程使用的节点

dependencies

### 切换npm sources

```bash
npm config get registry

npm config set registry= 

npm i nrm -g
nrm ls
nrm use
```

### Express

http的封装

```js
const express = require('express')

const app = express()

app.get('/about',(req,res)=>{
    res.send('hello world')
})

app.listen(80,()=>{})
```

路由

中间件  

注意事项  

+ 路由之前注册

+ 可连续调用多个中间件

+ 中间件 调用 next（）

+ 中间件调用 next（）后尽量不要写了

+ 多个中间件之间共享 `req res`

局部中间件

中间件分类

+ 应用级别
  + 绑定到app上的（全局）

+ 路由级别

+ 错误级别
  + 参数 error，req，res，next
  + 所有路由之后捕获全部异常防止程序终止

+ 内置
  + static
  + json
    + 4.16.0+ 版本可用
  + urlencoded

+ 第三方中间件
  + body-parser  以弃用

## 跨域问题

### JSONP

浏览器通过 script src 请求数据，返回函数调用

+ get请求
+ 非AJAX，未使用XMLHttpRequest

### CORS 主流

+ CORS Cross-Origin-Resource Sharing，跨资源共享
  + 支持 `XMLHttpRequest Level2` 方可用
  + Access-Control-Allow-Origin
  + Access-Control-Allow-Headers
    + 通过设置该响应头 允许浏览器发送某些请求头
  + Access-Control-Allow-Methods
    + 允许通过 PUT DELETE请求

简单请求  

+ GET POST HEAD请求
+ 九个请求头

预简请求

+ 发送 option 请求进行预简

+ 其他请求类型
+ 包含自定义请求头
+ 发送 application/json 格式数据

+ JSONP （只支持GET）

## JWT

json web token

Header Payload Signature
