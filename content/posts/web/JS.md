---
title: "JS"
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

# JavaScript

## 基础信息

ECMAScript 欧洲计算机制造协会  
DOM BOM  
脚本-动态类型-解释型语言

---

输出信息

+ prompt('弹出输入框')
+ alert('弹出提示')
+ console.log('控制台输出')

infinity 无穷大
NaN  not a number

字符串类型与任何类型相加 都为字符串拼接

Boolean(''):{'', 0, NaN, null, undefined} with false

### 逻辑运算符

=== 值和数据类型都相同

逻辑运算： 短路运算/逻辑中断 两个或多个表达式 类似三元计算符

```javascript
console.log('' && 1234) // ''
console.log(112 && 223) // 223

console.log(233 || 444) // 233

console.log( 234 || 10++) // num2=10
```

+ 如为真返回右边表达式值
+ 假 返回 左边
+ 左边返回后不执行右边表达式

```js
switch(){
    case 1:
        break
    finally:
        goto
}
// case 和判断数据为全等
```

### 数组

```js
var array = new Array();
var array = [];
```

### 函数

`arguraments` 参数

+ 伪数组
+ 数组序号获取,无数组方法

+ 全局作用域
  + 函数内无 `var` 参数为全局变量
+ 局部作用域
+ 块级作用域

作用域链: 内部函数访问使用链式结构查转(就近原则)

预解析: 将 `var` `function` 提升至作用域最前面 预先解析

+ 变量预解析(变量提升)
  + 只提升变量声明,不提示赋值(当前作用域前面)
+ 函数预解析
  + 函数声明提升,同上

### 对象

#### 构造函数

```js
function Method(name) {
  this.name = name,
  this.say = function (say) {
    console.log(say)
  }
}
// 对象
yc = new Method('yc');
yc.say('hh');
```

遍历对象：

```js

for(var k in yc){
  cosnole.log('key: '+k)
  console.log('value: 'yc[k])
}
```

#### 内置对象

+ Math
  + PI
  + abs
  + max，min
  + floor 向下取整
  + ceil 向上取整
  + round 四舍五入，负数取较大值
  + random
+ Data
+ Array
  + instanceof 类型判断
  + push 追加数组元素
  + unshfit 前面添加元素
  + pop 删除最后的元素
  + shift 删除第一个元素
  + reverse 翻转数组
  + sort 排序
  + indexOf 返回索引号
  + lastIndexof
+ String
  + charAt 根据位置获取字符
  + charCodeAt
  + substr  截取字符串
  + concat 链接字符串
  + replace 替换字符串
  + split 分割为数组

基本包装类型： 把简单数据类型 包装成了 复杂数据类型

> 如此才有相应的属性和方法调用

`string` 不可变 同c#

## Web Apis

### DOM

document object modal

#### 选择器

+ getElementById

+ getElementByTagName

+ getElementByClassName

+ querySelector

---

#### crud

修改文本

+ innerHTML *
+ innerText

修改样式  

`this.style.backgroundColor = "#333"`  

> 修改的样式为行内样式，权重仅次于 `!importent`

> `planholder` text 验证字符串

修改类名  

`this.className = "redtext class2"`

`自定义属性`获取与修改

+ setAttribute  
+ removeAttribute
+ getAuttribute

dataset

```js
<div class="customizediv" data-index='1'  data-serve-name='name'></div>

var cdiv = element.queryselecter('customizediv');

// 1
cdiv.getAttribute('data-index')

// 2
cdiv.dataset.index

// 3
cdiv.dataset['index']

// 驼峰法命名
cdiv.dataset.serveName
```

> 获取 `data` 开头的自定义属性

---

### 节点操作

父节点

+ node.parentNode

子节点

+ childNode 所有子节点（元素节点和文本节点）
  + nodeType `0` 为文本节点
  + nodeType `1` 为元素节点
  + node.chileNode[1]
+ children 子节点文档元素,非标准 `最为常用`
+ firstChild 获取包括文本节点和元素节点
+ lastChild
+ firstElementChild 获取元素节点，IE9以上

兄弟节点

+ nextSibling
+ previousSibling
  + 都包含所有节点，元素和文本
+ nextElementSibling

创建节点

+ createElement
+ insertBefore(创建的元素，添加元素的位置)

```js
var div = document.querySelecter('div');
//创建节点
var ulele = document.createElement('ul');

//添加节点
div.appendChild(ulele);

div.insertBefore(ulele,div.children[0])
```

删除节点

+ removeChild

> href javascript:; javascript:void(0); 阻止跳转

复制节点

+ cloneNode()

> 参数为空 ｜｜ 为 null 浅拷贝(只克隆节点本身，不包含子节点)；`true` 为深拷贝

```js
var ul = element.querySelecter('div');
var lil = ul.children[0].cloneNode(true);
ul.appendChild(lil)
```

动态创建元素区别

+ document.wirte
  + 导致页面重绘
+ element.innerHTML
  + 数组写入，效率更高
+ document.createElement
+ element.insertAdjacentHTML(,elemtnt)

### 事件

1. 注册事件

+ 具有唯一性
+ 后续事件会覆盖前面事件

```js
var btn.onclick = function() {}
```

2. 事件监听

+ addEventListener
  + 同一元素可注册多个监听器，按注册顺序依次执行
+ attachEvent
  + 非标准，不推荐
  + IE9之前版本可用
  
```js
ver btn = element.querySelecter('button')
btn[0].addEventListener('click',function() { console.log('注册的 onclick 点击事件')});
```

> 第三个 bool 参数判断是否为`冒泡` 或者 `捕获`，`true` 为冒泡阶段

3. 解除绑定的事件

``` js
// method 1 
btn[0].onclick = none 

// method 2
btn[0].removeEventListener(事件名，调用的函数名)

//method 3
btn[0].detachEvent(事件名，调用函数名)
```

4. DOM事件流

事件流执行过程，连续触发处于其中的事件

1. 从上往下 html文档到事件触发者 事件捕获阶段 该阶段父元素绑定事件更快执行

2. 从下往上 事件触发者到文档顶层 事件冒泡阶段 该阶段底层元素绑定更快执行

+ js代码只能执行其中一个阶段
+ onclick and attachEvent 只能得到冒泡阶段
+ addEventListener(type , listener , useCapture) 第三个参数为true，即捕获阶段；默认false，冒泡阶段

5. 事件对象

```js
btn.onclick = function(event){
  console.log(event)
}
```

> IE 678 使用 window.event

![事件绑定对象常见属性与方法](./images/event.png)

6. 事件委托

父元素添加事件监听，避免重复给子节点添加造成性能影响

e.target 和 this 区别

+ e.target 触发事件的对象
+ this 绑定事件的对象

> IE678 不支持 e.target

![MouseEvent 常用属性](./images/MouseEvent.png)

![KeyEvent 常用属性](./images/KeyEvent.png)

> 三个事件执行顺序 keydown -> keypress -> keyup

keyCode属性 获取触发事件的ASCII码

### BOM

window对象

+ 全局属性或方法都能被window访问
+ 有特殊属性为name，尽量不声明为 name 的变量

---

事件

pageLoadEvent

+ window.onload
  + 页面内容全部加载完后执行的事件
+ window.addEventListener(“load”,eventFunc)

+ document.addEventListener("DOMContentLoaded",eventFunc)
  + DOM加载完即执行，标签加载完

windowSize

+ window.onresize = function(){}
+ this.innerWidth
  + 获取窗口宽度

Timer

+ window.setTimeout
  + 可直接调用
  + 定时器加标志符，即不同属性名
+ window.clearTimeout

+ setInterval
  + 每隔几秒中执行该事件
+ clearInterval(timmerName)
  + 清除定时器

---

同步与异步  

main，主线程执行栈 -> 同步任务执行结束 -> 异步任务队列  

> 回调函数作为异步任务执行
![js event执行过程](./images/js_process.png)

---

localtion

![localtion常见属性](./images/localtion_attribute.png)

![localtion常见方法](./images/localtion_method.png)

navigator 对象

+ navigator.userAgent

history 对象

![history 对象 method](./images/browser_history.png)

#### js网页动画

> offset 动态获取位置

元素位置

+ element.offsetParent
返回带有定位的父级元素，父级没定位返回 body

+ element.offsetTop
返回元素相对带有定位的父元素上方的偏移量

+ element.offsetLeft
返回元素相对带有定位父元素左边框大的偏移

+ element.offsetWidth
+ element.offsetHeight

返回自身包含 padding border 内容区的宽度｜高；不带单位

> client 可视区相关信息，不包含border，含padding

元素大小

+ element.clientTop
+ element.clientLeft

+ element.clientWidth
+ element.clientHeight

padding + content，不含 padding，无单位

scroll 滚动距离

window.pageXOffset 页面滚动距离

mouseover && mouseenter
> 前者会冒泡

### 本地存储

1. sessionStorage

+ 生命周期为关闭浏览器窗口

+ 同一个窗口下数据共享

+ 存储为键值对

```js
sessionStorage.setItem(key,value)

sessionStorage.getItem(key)

sessionStorage.removeItem(key)

sessionStorage.clear()
```

2. localStorage

+ 生命周期永久生效

+ 浏览器中数据共享，多窗口共享

+ 键值对

使用方法基本同上

## Jquery

原生js的封装函数库

Jquery $ 顶级对象

### jquery 转换 dom

```js
var div =document.querySelecter('div')
$(div)
// 原生转jquery

$(div)[0]
$(div).get(0)
// jquery 转 dom
```

### 常用Jquery API

#### 选择器

1. 基本&层级选择器

```js
$('div')
$('#id')
$('.class')
$('ul>li')
$('ul li')
```

> 隐式迭代  对匹配的元素内部进行循环遍历，链式编程

2. 筛选选择器

```js
$('li:first')

$('li:last')

$('li:eq(2)')
// 索引号为 2

$('li:odd')
// 索引号为奇数

$('li:even')
// 索引号为偶数
```

3. 选择器方法

```js
$('li').parent()

$('li').children()

$('li').find()

$('li').siblings()
// 兄弟元素

$('li').nextAll()

$('li').prevAll()

$('li').hasClass()

$('li').eq(2)

```

#### 其他methods

1. 操作css

```js
$(this).css('color')
// 获取属性值

$(this).css('color','red')
// 设置单个属性值

$(this).css({'color':'red','background-color','blue'})
// 对象设置多个属性值
```

2. 操作class

```js
$(this).addClass('mclass')

$(this).removeClass('mclass')

$(this).toggleClass('mclass')
// 切换类
```

#### AJAX

```js
$.get(url, [data], [callback])

// 不带参数 ajax
$get('url', (res) => {
  console.log(res)
})

// 带参数 ajax
$.get('url', {id: 1}, (res) => {})

$.post(url, [data], [callback])

$.ajax({
  type: '',
  url: '',
  data: {},
  success: (res) => {}
})
```
