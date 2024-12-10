---
title: "VUE"
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

# Vue

> start `2021年3月19日`  
> update `2022-8-19`  
> end 

前端渐进式框架

前端三大框架

+ Vue
+ Angular
+ React

## 一 vue基础语法 模版语法

### 1. 文本插值 mustache 语法，插值表达式；
```html
<span>{{msg}}</span>

<!-- v-html innerHTML -->
<!-- 注意XSS漏洞，用户html不可信 -->
<p v-html="<span>innerHTML</span>"></p>

<!-- v-text -->
<!-- 覆盖默认内容 -->

<!-- v-for -->
<!-- v-for 比 v-if 有更高优先级,避免在同个元素上 -->
<td v-for="(value,key,index) in items" {{value}} :key= 'val.id'>this is table tag</td>

<!-- v-if  or v-show -->
<!-- 前者直接移除该标签，后者则是添加行内属性 -->
<p v-if="isDisable">in shot</p>
```

### 2. Attribute bind

``` html
<div v-bind:id='box1'></div>

<!-- 简写 -->
<div :id='box1'></div>
```

绑定多个对象

```html
<script>
data(){
  return {
    objOfAttrs: {
      id: 'box02',
      class: 'container'
    }
  }
}
</script>

<div :objOfAttrs></div>
```

### 3. event bind

``` js
v-on:click="btnClick()"
@click="btnClick"

$event
// 事件对象，可做参数传递 || 无参数默认传递，有参数需带该固定参数对象

<a @keyup.esc='clickEst'></a>
// 按键修饰符

<a @click.prevent=""></a>
event.preventDefault();
// 阻止默认行为

<a @click.stop=""></a>
event.stopPropagation();
// 阻止冒泡

<a @click.capture=""></a>
// 捕获模式触发当前事件

<a @click.once=""></a>
// 绑定事件触发一次

<a @click.self=""></a>
// 只有 event.target 是当前元素自身时触发事件处理函数
```

事件修饰符(event modifiers)

+ prevent
+ stop
+ once
+ key|key num

### bind注意信息

动态参数

```html
<!-- v-bind -->
<a :[attributeName]="url"></a>

<!-- v-on -->
<a @[eventName]='doSomeThing'></a>
```

动态参数注意

1. 值 只能为字符串 or null， null则移除该属性
2. 参数名 不可含有 空格 或者 引号,大写会自动转换为小写

> 以上：插值表达式 or `v-`开头的attribute中皆可使用js表达式，既：如下

```js
{{ number + 1 -1 * 1 / 1}}

{{ isOK ? 'yes' : 'no'}}

{{ str.trim().split('-').reverse().join('+') }}

<div :id="list-`${list.id}`"></div>
```

> 1. 以上 bind 仅支持`单一表达式`,既 可直接用`return 返回的`  
> 2. 以上访问的皆为有限全局对象列表，如需使用没有的属性可：`app.config.globalProperties` 显式添加

### v-model

实现数据双向绑定  
只能用于表单元素？

修饰符:

+ lazy    change 时而非 input 时改变
+ number  自动转为数值
+ trim    去除空格  

### vue其他属性

filters
> 过滤器, 应用于数据过滤 和绑定属性

```js
{{ messages | delI }}

new Vue({
  // methods same level,
  filters: {
    delI(val) {
      // val 既要过滤的数据
      // 必须有返回值
      return val
    }
}
})
```

methods
> 方法

### 计算属性

computed

1. 基于响应式依赖被缓存
2. 只有改依赖对象改变才会执行，example：for i in model；model改变，才会触发其中使用的computed
3. 不要有异步请求 或者更改DOM
4. compute返回值应为只读；其返回为派生状态，既一个`临时快照`

```js
export default {
  computed: {
    addNum(a,b){
      return a+b
    }
  }
}
```


### 侦听器

```js
const vue = new Vue(){
  data(){
    return { username:'233'}
  }
  watch: {
    username: {
      handler: async function(newVla,oldVal) {
        console.log(newVla,oldVal)
      },
      // 页面初始渲染好之后，立即触发该侦听器
      immediate: true，
      // 监听深层结构
      deep: true
    }
  }
}
```

### 生命周期

![周期图式3x](./images/lifecycle.png)
![lifecycle2x](./images/lifecycle%202x.png)

### var作用域

+ es5中只有`function`有作用域
+ es6中`if`和`for`也有作用域了
  + 使用`let`
  + 不用闭包实现作用域

### 数组

```js
let arr = ['a','b','c']

// forEach 使用后必定遍历一遍
arr.forEach(element => {});

// some return 可终止循环
arr.some( v=> {
  if(v === 'c') return true
})

// every
let boolval = arr.every( v => typeof v ===string)

// reduse
let result = arr.reduce((amt, item) => {return amt+=item},0)
```

---

## 一.二 响应式基础

```js
export default {
  data() {
    return {
      number: 2,
    }
  }
  // 生命周期钩子
  mounted() {
    console.log(this.number)
    this.number++
  },
  methods: {
    addNum(){
      this.number++
    }
  }
}
```

1. 不在data中的属性虽可添加使用，但是不会触发响应式更新

2. Vue 内置API `$`开头，内部属性 `_`;避免顶层data中使用

3. methods 永久指向当前Vue实例，可通过this访问；避免使用箭头表达式，箭头函数this无法指向上下文

4. Vue 默认深层响应，既无论多深的对象或者数组皆可访问，并对改变监测

5. methods中创建的方法有状态，多个不同组件调用或有影响，应在`created`生命周期钩子中创建;例如：防抖函数(debounce)


### DOM 更新时机

更新响应式状态后，DOM更新；DOM更新会在周期执行结束后一次性更新组件

可通过`nextTick`全局API，等待状态更新完成后的DOM

```js
import {nextTick} from 'vue'
export default{
  methods: {
    increment(){
      nextTick(()=>{})
    }
  }
}
```

## 二 vue组件

### vue原型挂载

```js
// main.js 不利于API接口复用
import axios from 'axios'

axios.defaults.baseURL = 'http://localhost'
Vue.prototype.$http = axios

// .vue
const { data: res } = await this.$http.get('/api/get',{data:{}})
```

EventBus 兄弟

操作DOM
ref
```html
<h1 ref="tmph1"></h1>

<script>
Vue(){
  methods: {
    logh1(){
      console.log($ref.tmph1)
    }
  }
}
</script>
```

### 注册组件基本步骤

old: use way

1. Vue.extend() #创建组件构造器
2. Vue.component() #注册组件
3. Vue实例范围内使用组件
4. vue实例components属性(即省略extent注册步骤,在实例中插入模板)

```js
// 全局组册组件,2x版本看的教程
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
const template01 = Vue.extend({
  data(){
    return {
      msg: "定义构建组件",
    }
  },
  template:`
  <h1>{{msg}}</h1>
  `
  })
Vue.component('teplateName',template01) // 组册
const vue = new Vue({
  el: "#App",
})
</script>

// js obj定义template
export default {
  data(){
    return {
      hello: "hello world"
    }
  },
  template:`<h1>这是一个局部组件,{{hello}}</h1>`
}
```

new: .vue file SFC（单文件组件）

```vue
// component01.vue
<template>{{hello}}</template>
<script>
export default {
  data(){
    return {
      hello: "hello world"
    }
  }
}
</script>

// 使用上方的组件
<template>
  <sp01></sp01>
</template>
<script>
import cp01 from './component01.vue'
export default {
  components: {
    cp01,
  }
}
</script>
```

#### style 样式

> css样式默认全局生效

scoped 使组件内样式与全局隔离   

> 原理为 添加自定义属性，通过css属性选择器隔离在该组件所有标签内；写在style标签中


/deep/ 选择器前添加使该组件所调用子孙皆添加该样式；多用于修改第三方组件库样式

```vue
<template></template>
<script></script>
<style scoped lang="less"></style>
```

### component标签，keepalive动态组件

component

1. 模版中 `component` 标签为默认可替换标签
2. 通过 `is` 属性绑定要替换的组件,绑定 data 中的值

> 组件切换，销毁后创新新实例，状态重置

```vue
// component 动态切换基础
<template>
<component :is="mountComponent"></component>
</template>

<script>
import c1 from './component01.vue'
import c2 from './component02.vue'

export default {
  data(){
    return {
      mountComponent: 'c1'
    }
  }
  components: {
    c1,c2
  }
}
</script>
```

keepalive

1. 使包含在内的component组件保持状态

2. include 和 exclude 规定行为；值为字符串或者正则，或者两个类型的数组

3. max 限制保持实例数量；即将超出时，销毁最久未访问实例，为新实例腾出空间

```vue
// 保持组件状态
<template>
  <keepalive :include="c1" :exclude="c2" :max="10"><component/></keepalive>
</template>
```

keepalive生命周期

> 缓存树中后代组件可用

```vue
<script>
export default {
  activeted(){
    // 首次挂载
    // 每次从缓存中重新插入
  }
  deactivated(){
    // DOM上移除，进入缓存
    // 组件卸载
  }
}
</script>
```

### 模板分离

```html
<script type=text/x-template if=''> </script>
<template id=''></template>
```

### 通讯

+ 模板参数传递使用data函数返回(隔离组件返回对象数据)
+ props(父传子)
  + 声明变量,在模板中使用,通过绑定该属性传递父组件的值
+ $emit(子传父)
  + 自定义事件
  + $event为推出的值
+ $children || $refs
  + 获取子组件对象,常用$refs,通过标签设置ref属性访问
+ $parent || $root

#### props 父组件向子组件传值

1. 子组件通过props定义传递的值
2. 父组件通过对自定义模版标签 绑定自定义属性（既子组件中定义的属性）并传值，向子组件传值

> 只读属性，父传子后，子不能修改改值；但可绑定到data中重新赋值

```js
// father vue
<template>
<child :msg="hello"></child>
</template>
<script>
import child from './child.vue'
  export default {
    data(){
      return {
        mymsg: this.msg
      }
    },
    component: {child},
  }
</script>


// child vue
<template>
<h1>{{msg1 + msg2}}</h1>
</template>
<script>
  export default {
    data(){
    },
    // Define way01
    // props: ["msg"],

    // Define way02
    // prots: {
    //   msg1: String,
    //   msg2: Number
    // }

    // Define way03
    props: {
      msg1: Sting,
      msg2:{
        type: Number,
        default: "hello",
        required: true
      }
    }
  }
</script>
```

#### $emit() 子传父

```vue
/ father vue
<template>
{{mymsg}}
<child @getMsg="getmsg"></child>
</template>
<script>
import child from './child.vue'
  export default {
    data(){
      return {
        mymsg: 0
      }
    },
    component: {child},
    methods: {
      getmsg(val){
        this.mymsg = val
      }
    },
  }
</script>


// child vue
<template>
<h1 @click="pushMsg"></h1>
</template>
<script>
  export default {
    data(){
      return{
        msg: "hello"
      }
    },
    methods: {
      pushMsg(){
        this.$emit('getMsg',msg)
      }
    }
  }
</script>

```


### slot(插槽)

> 组件可重用之外的使用插槽

+ 组件中使用`<slot></slot>`声明插槽
+ 组件中slot标签之间为默认值,正文中为不同模板
+ 具名插槽
  + 模板`slot标签`中的`name`属性用以声明
  + 注册标签中绑定`slot`属性实现该插槽
  + 使用时的`slot`属性要在模板标签只能其他标签中
+ 作用域插槽
  + 模板中不同标签放在`slot`中
  + 绑定数据对象(要传递给父对象使用的数据)
  + 实例中使用`slot-scope`属性绑定插槽对象(名字可随意取),包含外围标签中
  + 然后通过`.`获取绑定名以获取数据
  + 绑定数据对象可随意取名,但后期使用时要一样才能获取

注意事项

1. slot内的样式由父组件提供
2. slot无法访问子组件数据，因为其作用域实际在父组件中
3. 子组件可在slot中定义默认内容，在父组件未为其传值时显示，父组件传值既会覆盖该内容

#### 插槽基本定义与使用

```vue
// 父组件调用子组件，并传值，更新slot插槽位置
<template>
  <myComponent>
    child slot content
  </myComponent>
</template>

// myComponent ,子组件 slot 标签占位
<template>
  <slot>default content</slot>
</template>
```

---

## 三.二 vue-cli

### 安装及初始化

安装

```bash
npm install -g @vue/cli

# 拉取CLI 2x模板
npm install -g @vue/cli-init
```

初始化项目

``` base
# 3x
vue create 项目名

# 2X
vue init webpack 项目名

# 图形化配置管理
vue ui
```

#### Runtime-Complite 和 Runtime-only 区别

---

## 三 axios

### Promise

> 异步编程解决方案
> 链式编程

三种状态

+ pending:等待
+ fulfill:满足
+ reject:拒绝


## 四 vue-route(前端渲染)

### hash or history 模式

```js
//请求页面不刷新页面 hash
localtion.hase = 'url'

//  window.history 栈结构
history.pushState({},'','url')    
history.back()
history.replaceState({},'','')
history.go(num)   :栈上移动
```

### start

安装

``` bash
npm install vue-route --save
```

步骤:

1. Vue.user(插件)
2. import export
3. vue VueReouter实例
   1. router
   2. mode
   3. linkactiveclass
4. vue绑定route实例
5. 配置路由映射
6. router-link
   1. to    绑定vue模板
   2. type  标签类型
   3. tag   标签
   4. replate 浏览器无返回,返回上一页无用
   5. active-class(模板)
   6. router-active-class(路由index.js)
   7. 自定义点击事件实现简单路由
      1. this.$router.push('/Home') || replate
7. router-view
   + 展示routerlink模板页面

## 路由

> 1. 动态路由

路由含有一些后台数据,不是固定链接

``` JavaScript
router: {
  path: '/path/:info',
  // 重定向
  redirect: '/path2'，
  alias: '/c'
}

// alias 用户访问 /path2 返回 /c

vue
this.$route.params.info
```
使用计算属性返回info  

路由参数传递

+ params :
  + this.$route.params.attr
+ query ?
  + $route.$query.attr
+ hash
  + $route.hash

> 路由传参数 props


> 2. 嵌套路由

路由children配置子路由

```js
routes: {
  path: '',
  component: index,
  childrem: [
    {
      path: 'child-route',
      component: child-page
    }
  ]
}
```

> 3.1 命名视图

```js
<router-view name='p1'/>
<router-view name='p2'/>

router: {
  path: '',
  components: {
    default: componentName1,
    p1: componentName2,
  }
}
```

> 3. 命名路由,感觉较为妥当，但是要多写

既在声明路由时添加`name`属性

```js
{
  name: 'index',
  path: '',
  component: 
}

<router-link :to={ name: 'index', params: { id: 111}}>link-user</router-link>
```

> 编程式导航,类似 `window.history` 几个方法

```js
// 声明式导航
<rouer-link to="" />

// 编程式导航
router.push()

// 替换当前history
<rouer-link to="" replace/>
router.replace()

router.go
```

如果当前路由与下一路由相同，只是参数变化，需要导航守卫来响应变化

> $router与$route区别

+ $router 定义的路由对象
+ $route 路由对象上处于活跃状态的路由对象


### 路由懒加载

> 使用时再请求

路由里面component用匿名函数返回模板对象，webpack打包自动处理；若使用babel 需要插件 syntax-dynamic-import

``` js
const Page = () => import('../components/Page')

// 正常使用
const routes = [
    { 
        path: '/page',
        component: Page
    }
]
```

### 导航守卫,路由生命周期函数

> 路由跳转中的钩子函数(声明周期里面)

### 全局导航守卫

```javascript
//前置守卫(guard)
router.beforeEach((to,form,next) => {
    next()//继续进行下一步
})

//后置钩子(hook)
router.afterEach((to,form) => {
    next()
})
```
+ 路由独享守卫

---

## 五 vuex

集中状态管理库


---