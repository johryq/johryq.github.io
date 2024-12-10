---
title: "JS ES5"
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

# javascript ES6 语法

既 ecma 2015年6月推出的ecmascript标准统称

## 类与实例

+ 封装
+ 继承
+ 多态

类中注意事项

1. 类无变量提升，必须先定义再使用
2. 类中共有方法和属性必须加 this 才能访问
3. constructor 中的 this 指向实例对象，方法中的 this 指向方法调用者

创建类

```js
class Car {
    // 构造函数
    constructor(name) {
        this.name = name
    }
    driver(dname){
        console.log('bmw is drive')
    }
}
```

继承 extends

```js
class Bmw extends Car{}
```

super 关键字

+ 必须在子类 this 关键字之前使用

```js
class Bmw extends Car{
    constructor(name){
        super(name) // 获取父类中的数据
    }
    super.driver()
}
```

## 构造函数与原型 ES6 之前 组合继承

+ 首字母大写，new 创建

```js
function Man(name,age){
    this.name = name,
    this.age = age,
    this.talk = function() {
        console.log('i am talk')
    }
}

var am = new Man('am',12)
```

静态成员与实例成员

```js
Man.lastName = 'ln' //静态成员 ，只对构造函数可用可访问

am.talk() //实例对象
```

构造函数 原型对象 prototype

> 实现构造函数内 方法共享 共用同一内存空间

```js
Man.production.drink = function(){
    console.log('drink')
}
```

> 实例对象 通过 _proto_ 访问构造函数中的 prototype；即 _proto_ => prototype ;两者等价

constructor属性

> 即构造函数本身

构造函数 实例对象 原型对象 三者关系

![class](./images/calss.png)

原型链 => 逐层查找 直至 object 下一层级 null

call方法 改变this指向

```js
function Father (uname, age) {
    this.uname = uname,
    this.age = age
}

// 继承父构造
function Son (uname, age) {
    Father.call(this,uname,age)
}
```

### new methods

+ forEach() 迭代遍历

```js
arrary.forEach((value, index, array) => {
    console.log('数组元素，索引号，数组本身')
})
```

> return true 不可中断循环

+ filter() 过滤 arrary

```js
var returnArray = arrary.filter((value,index,array) => {
    return value>=10
})
```

+ some() 查找数组中是否有满足条件的元素 bool

```js
var Val = arrary.some((value, index, array) => {
    return true
})
console.log('Val === true')
```

> 匹配到第一个元素后即返回

+ Object.defineProperty() 定义新属性或修改原有属性

```js
Object.defineProperty(obj, prop, descriptor)

```

descriptor 包含4种属性

1. value            设置属性值
2. writable         是否可重写
3. enumerable       是否可枚举
4. configurable     是否可被删除或被再次修改

## method

+ 定义

```js
// 1
function f1() {}

// 2
var f2 = function() {};

//3
var f3 = Function('a', 'b', 'console.log(a+b)')
f3(1,2)
```

> 和class中相同有`原型链`

+ 调用

```js
// 1 普通函数
function f1() {}
f1() f1.call()

// 2 对象的方法
var obj = {
    callMe: function() {}
}
obj.callMe()

// 3 构造函数
function F3() {}
new F3()

// 4 绑定事件
btn.onclick = function() {}

// 5 定时器函数
setInterval(function(){}, 1000) // 1s后自动调用

// 6 立即执行函数
(function(){})()
```

+ apply 改变this指向,第二参数为array

```js
var arr = [1,32,324,22,214]
var max = Math.max.apply(Math,arr)
```

+ bind

1. 不改变原有函数this，不调用原函数
2. 返回原函数的拷贝

+ 严格模式

```js
'use strict';
```

严格模式 this 指向

1. 以前全局函数 this 指向 window；现在为 undefined
2. 以前构造函数不 new 可调用，当普通函数，this 指向 全局；现在 报错
3. new 实例化构造函数指向创建的对象实例
4. 定时器 this 指向 window
5. 事件，对象指向调用者
6. 函数不能有重名参数
7. 函数声明必须在顶层，ES6引入块级作用；不允许非函数代码块内声明函数

> 可为整个脚本开启，获取为某个函数开启

高阶函数 => 函数为参数 委托

闭包 => 有权访问另一个函数作用域中的变量的函数，延伸变量作用范围

浅拷贝 => 拷贝一层，更深层次数据（对象,数组）只拷贝引用地址

```js
// 浅拷贝语法
Object.assign(sourceObj,newObj)
```

深拷贝 => 拷贝多层，每一层级都会拷贝

```js

```

## 正则

## 异步

### Promise

> ES5语法 避免回调地狱；是个构造函数

```js
const promise = new Promise()

promise.then()
// 返回的是Promise对象的话，可进行链式调用

.catch()
// 捕获错误；最后可捕获前所有错误，最前则避免then停止持续执行

.all(promiseArry)
// 根据promiseArray 顺序执行，执行完毕后返回结果

.race()
// 并行执行传入的promise，相较all更快
```

### await async

> ES8 es2017

await 返回异步操作之后的结果

```js
async waitTimer() {
    await setInterval(() => {console.log('timer)} ,0)
}
```

### EventLoop

1. js为单线程
2. 异步任务委托给宿主环境（浏览器，node.js）执行
3. 已完成异步任务对应回调在任务队列中排队等待执行
4. js主线程执行结束后，再执行该任务队列，依次执行

### 宏任务-微任务

异步任务分为 宏任务 微任务  

每次宏任务执行完；判断是否有微任务；有则执行完所有微任务再执行宏任务

宏任务： 需要排队等待的  
exap： setInterval

微任务  
exap： Promise


## ES6语法

ES2015 之后的标准

### let

+ 有块级作用域
+ 不存在变量提升（先声明才能使用）
+ 暂时性死区

```js
var num = 10;
if(true){
    num = 20;
    let num = 30
}

// num is not defined
```

### const

+ 值（内存地址）不可变
+ 有块级作用域
+ 声明必须赋值

### 解构赋值

按照一定模式，从数组或对象中提取值，将提取的值赋值给另一个变量

> 数组

```js
let [a, b,c] = [1, 2, 3]
console.log(a)
console.log(b)
console.log(c)
```

> 对象

```js
let person = { name: 'zs', age: 20}
let {name, age} =person
console.log(name)
console.log(age)

let {name: myName, age: myAge} =person  // myName 等为别名
console.log(myName)
console.log(myAge)
```

### 箭头函数

+ 函数体只有一句话，且执行结果就是返回值，可省略函数体大括号

+ 形参只有一个，可省略小括号

### Array 扩展方法

+ Array.from

将伪数组或可遍历对象转化为数组；第二个参数，类似数组的map，对每个元素进行处理，将处理后的值返回数组

+ Array.find

查找符合条件的第一个数组成员，没有返回 undefined

+ Array.findIndex

+ Array.includes

数组中是否包含给定值，返回bool

### 模版字符串

```js
let name = `${name} hello`
```

### String 扩展方法

+ startsWith

参数字符串是否在原字符串头部，返回bool

+ endsWith

参数字符串是否在原字符串尾部

+ repeat

将字符串重复N次，返回新字符串

### Set 数据结构

类似数组，成员值唯一，没有重复值；是个构造函数

```js
const s1 = new Set()
s1.size

s1.add()        // return s1

s1.delete()     // return bool

s1.has()        // return bool

s1.clear()      // no return

s1.forEach((value,index) => console.log(value+' '+index))
```
