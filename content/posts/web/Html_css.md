---
title: "HTML && CSS"
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
# HTMl CSS

## 黑马pink 基础标签知识点 HTML

+ div 块级标签，单独占一行，盒子
+ span 流标签
+ 锚点标签

```html
<a href="#name">233</a>
<h1 id="name">h1s</h1>
```

+ 特殊字符

```html
&nbsp;  空格
&lt; <
&gt; >
```

+ table
  + cellpadding 单元格边沿与内容的距离，默认1px（单元格大小）
  + cellspacing 单元格文字之间的距离，默认2px（内外边框大小）
  + thead
  + tbody
  + rowspan 跨行合并
  + colspan 跨列合并

+ 列表
  + ul - li
  + ol - li
  + dl - dt - dd

+ input
  + type name value checked maxlength
  + text
  + password
  + radio 相同name属性单选
  + checkbox
+ label
  + for
  + id
+ select
  + option
  + selected
+ textarea
  + rows
  + cols

### html5 新标签

1. 语意化标签

+ header 头
+ nav 导航
+ article 内容
+ section 自定义文档某区域
+ aside 侧边栏
+ footer 尾

2. 多媒体

+ audio
+ video
  + `<video src="" controls="controls"></vide>`
  + mp4 ogg webm

3. 表单 input type

+ email
+ url
+ date
+ time
+ month
+ week
+ number
+ tel
+ search
+ color

> 验证需要添加 `form` 表单域

4. 表单属性

+ required 必填
+ placeholder 提示信息
+ autofocus 自动聚焦
+ autocomplete 是否基于以前的输入显示信息（需在表单域中，且已输入过）
+ multiple 多选文件

---

## CSS

层叠样式表

---
### 选择器：

+ 类选择器
+ ID选择器
+ 标签选择器
+ 通配符选择器 *

其他选择器：

5.后代选择器

```css
ul li a {} /* 只对树枝下的a */
```

6.子元素选择器

```css
ul > li /* 只对ul下的li只能选择子元素 */
```

7.并集选择器

```css
table,a,p /* 针对写的所有标签 */
```

8.伪类选择器

```css
:link     /* 所有未访问链接 */
:visited  /* 所以已访问链接 */
:hover    /* 鼠标指到的链接 */
:active   /* 鼠标按下未弹起链接 */

:focus    /* 获取焦点的表单元素 */
```
> 顺序必须遵循 LVHA

font：

+ font-weight：「normal，bold，bolder，lighter，number（100-900）」
+ font-style：「normal，itelic」
+ font： 「font-style， font-weight， font-size/line-height， font-fmaily」

> font样式 font-size 和 font-family 不可省  

text：

+ text-decoration/装饰文本： 「none, underline, overline, line-through」
+ text-indent/首行缩进:
+ line-height/行间距：

> em 相对单位，当前元素文字大小（font-size）；行间距为上下边距之和

---

### 元素分类

1. 块级元素

2. 行内块元素

3. 行内元素
  + 宽，高不可修改
  + 不能放块元素
  + 默认宽度为内容宽度

行块元素互转

```css
display: inline(行) | block(块) | inline-block(行内块)
```

---
### background

1. `background-repeat`(背景图片平铺): no-repeat | repeat |  repeat-x | repeat-y

2. `background-position`(背景图片位置): (方位名词：相对中心点 ｜ 精确数值：XY轴 ｜ 混合使用)

3. `background-attachment`(背景附着)：scroll | fixed (固定)  ｜制作视差滚动

4. `background`（提倡顺序为 颜色，图片url，平铺，附着，位置）

5. 背景色半透明，css3，`backgrount: rgba(0,0,0,0.5)`

### 三大特性

+ 层叠性
  + 就近原则，后来居上
+ 继承性
  + text，line，fount，color
+ 优先级
  + `!important` 优先级最高
  + 复合选择器权重叠加

### 盒子模型

+ border
+ content
+ padding
+ margin

```css
/* 相邻边框合并 */
border-collapse: collapse 
```

+ 盒子本身无 `width` `height` 不会被 `padding` 撑开

+ 块级元素 设置 `width` 后，左右 `margin` `auto` 即可水平居中

#### 盒子模型的塌陷与合并

+ 盒子合并

[相邻块元素 设置相邻外边距会产生合并 - 最后以最大值现实](../practice/html_css/06_marginADD.html)

+ [盒子塌陷](../practice/html_css/07_boxSubsidence%20.html)

解决方案

1. 父元素加border
2. 父元素加padding
3. 加 overflow
> overflow 溢出控制注意有定位的部分！！！

#### booder圆角矩形

```css
/* 设置圆角矩形 */
border-radius:length

box-shadow: h-shadow | v-shadow | blur | spread | color | inset

text-shadow
```

#### float

+ 脱离标准流
+ 由内容决定宽度
+ 行内块元素某些特点
+ 块之间无间隙
+ 只影响后面的标准流

##### 清除浮动

> 父盒子没有高度，子盒子浮动了，避免对浮动后面元素产生影响,只对块级标签有用

```css
选择器 {
  clear: both | left | right
}
```

具体措施

1. 浮动元素最后添加一个盒子<div style= " clear: both"></div>

2. 给父元素添加`overflow：hidden`

3. 添加`:after`伪元素（对父元素添加）

```css
:clearfix {
  content: "";
  display: block;
  height: 0;
  claear: both;
  visibility: hidden;
}

:clearfix {
  /* IE 6,7专用 */
  *zoom: 1;
}

```

4. `:after``:before`伪元素清除前后

```css
.clearfix:before,
.clearfix:after {
  content: 0;
  display: table;
}

.clearfix:after {
  clear:both;
}

.clearfix {
  *zoom:1;
}
```

### 定位

定位 = 定位模式 + 边偏移

#### 定位模式

position: static ｜relative ｜sbsolute

+ static
  + 类似标准流
+ relative
  + 相对元素本身原来位置偏移
  + 原来位置继续保存，不脱标
+ absolutle
  + 一般相对父元素移动（父元素需加绝对定位），没有则以浏览器
  + 如父没有，则以上级有定位的元素移动
+ fixed
  + 固定定位
  + 浏览器可视窗口为定位点
  + 脱标，不占有标准流
+ sticky
  + 粘性定位
  + 占有原来位置
  + 相对于绝对定位的整合（以窗口可视区为准）
  + 必加边偏移

> 子绝父相

#### 边偏移

top right left  bottom

#### 定位堆叠次序

+ z-index
  + 控制盒子先后顺序
  + 如无，则后来者居上
  + 只对position盒子有用

> 浮动元素不会压住标准流文字，`position`会压住标准流

### 可见性

+ display
  + none
  + 不占有位置
+ visibility
  + visible
  + hidden
  + 占有原本位置
+ overflow
  + 溢出部分是否隐藏
  + scorll 现实滚动条
  + auto 需要时添加滚动条
  + visible

> overflow 溢出控制注意有定位的部分！！！

### 精灵图

+ 主要针对背景图片 sprites
+ 通过 `background-position` 调整 x，y轴
+ 一般为负值

### 样式

#### 鼠标样式

`cursor` 属性进行配置

+ default
+ pointer 小手
+ move 移动
+ text 文本
+ not-allowed 静止

#### 表单样式

+ outline
  + 表单轮廓线
+ resize
  + 文本域禁止调整大小

### 其他属性

##### 1.vertical-alien

配置文本对齐位置，对于行内块元素or块

```css
vertical-align: baseline | top | middle | bottom
```

> 避免图片与文字在同行存在的空隙

#### 2.多余文字设置为省略号

单行 设置

```css
/* 1.文字一行显示 */
white-space: nowrap

/* 2.溢出部分隐藏 */
overflow: hidden

/* 3.省略号代替溢出部分 */
text-overflow: ellipsis
```

多行设置  
适用wibkit内核的浏览器 包含大部分移动端浏览器

```css
overflow: hidden;

text-overflow: ellipsis;

/* 伸缩盒子模型显示 */
display: -webkit-box;


/* 限制在一个块元素显示的文本行数 */
-webkit-line-clamp: 2;


/* 设置或检索伸缩盒对象的子元素排列方式 */
-webkit-box-orient: vertical
```

### css3新特性

+ -webkit-font-smoothing: antialiased;
  + 抗锯齿

1. 新增选择器

+ 属性选择器
  + []
  + text[value]
  + text[value="123"] 匹配属性值
  + text[value$="22"] 匹配属性开头字符串
  + text[value^="33"] 匹配属性结尾字符串
  + text[text*="123"] 匹配包含123 的
  + 权重 10
+ 结构伪类选择器
+ 伪元素选择器
  + ::before
  + ::after
  + 都包含在父元素中，父元素最前｜ 父元素最后
  + 必须包含 `content` 属性
  + 权重 `1`
  + 行内元素

伪元素清除浮动

```css
/* method 1 */
.clearfix:after {
  /* content: ""; */
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;
}
/* method 2 */

.clearfix:before,.clearfox:after {
  content: "";
  display: table ;
}
.clearfix:after {
  clear: both;
}
```

3. css3盒子模型

+ content-box *default*
  + box-sizing = content-box‘s width + padding + border
+ border-box
  + box-sizing 属性
  + box-sizing = box width

4. 函数 

filter滤镜属性

> blur函数 > 调整模糊度

calc函数

> calc函数  > 计算属性值

transition 属性

> 要过渡属性 花费时间（must）  运动曲线 何时开始  
> 哪里动哪里加


5. 2D转换 transform

> 综合运用时会根据书写顺序从左到右执行

#### translate

1. 类似left，top等浮动元素的位移

2. 百分比参数 是相对自身的

3. 行内标签不可用

```css
transform: translate(x,y);

transform: translateX(n);

transform: translateY(n);

transform: translate(-50%,-50%);
/* 元素居中 */
```
> 不会影响其他元素，盒子

#### rotate

元素旋转

```css
transform: rotate(45deg);

/* 设置旋转的中心点 */
transform-origin: left bottom;

transform-origin: 20px 20px;

```

#### scale

1. 倍数修改盒子大小

2. 不会影响其他元素

3. 可以设置中心点

```css
transform: scale(2, 1)

/* 等比放大 */
transform: scale(2)
```

6. 动画 animation

类似adoble animate

+ 先定义动画

+ 设置动画序列

+ 调用动画

```css
@keyframes moveDiv {
 0% {
    开始状态
 }
 100% {
    结束动画
 }

 form {}
 to {}
}

animation-name: name;
animation-duration: 持续时间;

animation: 动画名称 动画时长 速度曲线 延迟时间 重复次数 动作方向 执行完毕时状态
```

> 动画开始状态与盒子默认状态相同 省略动画开始

![常见属性](./html_css/images/animation%20.png)

#### 3D转换

translate3d

```css
transform: translateX() translateY() translateZ();

/* perspective 透视 人眼到屏幕距离 近大远小 给父元素添加  */
perspective: 100px;
```

3d旋转,单位deg  

```css
/* 45deg 自定义旋转轴 */
transform: rotate(x,y,z,45deg); 

transform: rotateX() rotateY() rotateZ();

transform: rotate3d()
```

transform-style 3d呈现方式  

子元素是否开启3d空间

```css
/* 给父元素开启，默认值为 flat */
transform-style: preserve-3d
```

#### 浏览器私有前缀

+ -moz- ： firefox 私有属性

+ -ms- ： IE

+ -webkit- ： safari，chrome

+ -o- ： Opera

### 移动端

> 主要处理webkit内核

#### 视图标签

![viewmeta](./html_css/images/viewmeta.png)


#### 物理像素

移动端 设置的px会和物理像素成倍关系  

移动端图片使用 多倍分辨率的图片以保障在手机上图片的清晰度

`background-size` 设置背景图片的尺寸

+ % 相对父盒子

+ cover 完全覆盖盒子，可能有部分背景图片显示不全

+ contain 将图像扩大至最大尺寸，使宽高完全适应内容区域，高宽等比缩放，其一到顶则结束扩展，可能有部分为空白

> 移动端初始化css normalize

#### 移动端特殊属性

```css
box-sizing: border-box;
-webkit-box-sizing: border-box;

/* 清除点击高亮显示 */
-webkit-tap-heightlight-color: transparent;

/* ios 自定义按钮 输入框样式必须 */
-webkit-appearance: none;

/* 禁用长按页面时弹出菜单 */
img,a {-webkit-touch-callout: none;}
```

#### 移动端技术选型

单独制作页面

+ 流式布局
  + 宽度百分比，高度固定
+ flex弹性布局
+ less+rem+媒体查询布局
+ 混合布局

响应式页面

+ 媒体查询
+ bootstrap

1. 流式布局

2. flex弹性布局

container 配置

```css
/* 配置X Y轴排列 */
flex-direction: row | row-reverse | column | column-reverse

/* 配置主轴后（默认X轴），子元素排列方式; 主轴对其方式 */
justify-conten: flex-start | flex-end | center ｜space-around ｜ space-between


/* 配置侧轴排列，仅适用单行; 侧轴对其方式 */
align-items: flex-start | flex-end | center | stretch(默认，拉伸，子盒子不给高度)

/* 是否换行显示，默认不换行 */
flex-wrap: nowrap | wrap

/* 多列/行侧轴 */
align-content: space-around | space-between | 同上

/* flex-direction flex-wrap 组合属性 */
flex-flow: row wrap

```

子项属性

```css
/* 配置子项剩余空间 */
flex: [number][default 0]
/* 包含: flex-grow flex-shrink flex-basis */

/* 子项侧轴对齐方式 */
align-self: 

/* 子项排列方式 */
order:
```

背景颜色渐变

```css
/* 线性渐变,需添加浏览器私有前缀-webkit-等 */
background: linear-gradient(top,red,blue)

```

---

## SEO优化

### TDK

+ title
  + `<title>京东(JD.COM)-正品低价、品质保障、配送及时、轻松购物！</title>`
+ description
  + `<meta name="description" content="京东JD.COM-专业的综合网上购物商城，为您提供正品低价的购物选择、优质便捷的服务体验。商品来自全球数十万品牌商家，囊括家电、手机、电脑、服装、居家、母婴、美妆、个护、食品、生鲜等丰富品类，满足各种购物需求。"/>`
+ keywords
  + `<meta name="Keywords" content="网上购物,网上商城,家电,手机,电脑,服装,居家,母婴,美妆,个护,食品,生鲜,京东"/>`


### logo SEO

1. 放 `h1` 提权，告知搜索引擎

2. `a` 链接主页

3. 链接内放文字（网站名称）但是不显示
  + `text-indent: -9999px; overflow: hidden`
  + `font-size: 0;`

4. 链接 `title` ，鼠标提示信息

---

