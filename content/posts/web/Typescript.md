---
title: "TS"
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
# Typescript

javascript 超集

```json
// teconfig.json
{
    "compilerOptions": {
        "watch": true,
        "removeComments": true,
        "target": "es5",
        "noImplicitAny": true,
        "strictNullChecks": true
    }
}
```

## 1.install

```bash
npm i typescript ts-node -g
tsc -v

# 编译执行
tsc xx.ts
node xx.ts

# 自动更新
ts-node xx.ts
```

## 2.基础类型

通过`类型注解`声明数据类型

```ts
let age:number = 10
```

原有类型

+ number
+ string
+ boolean
+ null
+ undefined
+ symbol
+ object(array,obj,method)

新增

+ 联合类型
+ 自定义类型（类型别名）
+ 接口
+ 元祖
+ 字面量类型
+ 枚举
+ void
+ any

基础类型声明

```ts
// string
let str1:string = 'str'
let str2:string = `${variable} str`

// number
let num1:number = NaN
let num2:number =  Infinity // 无穷大
let num3:number = 0b1010    // 二进制
let num4:number = 0o744     // 八进制
let num5:number = 123       // 十进制
let num6:number = 0xf00d    // 十六进制

// bool
let bool:boolean = true

//void
let none:void = undefined
let none:void = null

let none:undefined = undefined
let none:null = null
// undefined 和 null 是所有类型的子类型
```

## 3.any类型

1. 类型随意切换，且不进行类型检查

```ts
let a1:any = 123
let a2:any = "233"

a1 = a2

let obj:any = { b: 333}
obj.a
// 上述语句可执行，且不报错
// any类型在对象没有相应属性时，不会报错
```

2. 声明变量不指定类型，默认any

```ts
let a
a = 233
a = '233'
```

3. ts 3.0 引入 unknown类型，与any类似，但只能与unknown 类型传递值，且不能调用属性和方法

```ts
let unknown:unknown = {a:233}
unknown.a  
// unknown 无法调用a
// unknown不能调用属性和方法

let str1:unknown = '233'
let str2:string = '233'
str2 = str1
// 报错，unknown 作为父类型无法赋值给子类型
```

## 3.引用类型

### class

### Array

```ts
let a2:number[] = [233]
// 基本定义

interface A1{
    [index: number]: number
}
let a1:A1 = [1,2,3]
// 类数组

let a3:Array<number> = [1,2]
// 泛型数组

let a4:[][] = [[2,2]]
// 多维数组
```

### function

```ts
// method type
function getNumber(num:number):number {
    return num
}

// 函数表达式？ 匿名函数
const getNumber = (num: number) => number = (num) => {
    return num
}

// return void
function logNumber(num: number):void {
    console.log(num)
}

// 可选参数：声明必须位于参数项最后
function logInfo(info?: string = 'hello world'):void {
    console.log(info)
}

```

### object

可为所有引用类型

```ts
let obj4:object = 233
// 报错

let obj1:object = []
let obj2:object = {}
let obj3:object =  = () => 233
```

### Object

+ 原型链顶端数据类型，所有原始类型和对象指向该类型，也就包含了ts中所有类型
+ 可为任意类型

```ts
let a1:Object = 233
let a2:Object = []
let a3:Object = {}
let a4:Object = () => 233

let a5:{} = obj
// 字面量类型，创建后无法修改
// 这个也是Object类型
```

## 4.接口

interfase ，定义类型约束

1. 定义接口与使用接口必须类型一致

```ts
interface Person {
    name: string
    say: () => void
}

let son:Person = {
    name: 'son'
} // error

let son:Person = {
    name: 'son'
    say: () => {}
}

interface Fn {
    (name:string): number // 定义方法
}

let func:Fn = function (){
    return 233
}
```

2. 类似function props,留下定义位置

```ts
interface Person {
    name:string
    [propName:string]:any
}

let son:Person = {
    name: '233'
    agt: 23
    height: 23
}
```

3. ? 可选类型， readonly

```ts
interface Person {
    readonly id: number  // readonly
    name: string
    age?: number         // 可选类型
}
```

4. 接口继承

```ts
interface Person extends B {
    name: string
    say: () => void
}
interface Person {
    talk: string
}
// 重名接口将合并

interface B {
    lol: string
}
```


let numberAry: number[]
let numberAry2: Array<number>

let boolAry: boolean[]

let dobTypeAry: (string | number)[] 
let dbType2: string | string[]

// 类型别名
type CustomArray = (number | string)[]
let bdTypeAry: CustomArray