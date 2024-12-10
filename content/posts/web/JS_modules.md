---
title: "JS Modules"
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

## js 模块化

- 避免多人开发,函数混乱,命名冲突,不可复用
- 函数闭包实现模块化(不可重用,封装模块(返回对象)实现重用)

_模块化规范_

- CommonJS \*\*
- AMD
- CMD
- ES6 Modules \*\*

模块化的重要部分

### commonjs

- 导出(export)
  - 声明你想要外部访问的值,对象等
- 导入(require)
  - 使用其他 js 文件

```javascript
//导出
module.exports = {
  flag: true,
  test(a, b) {
    return a + b;
  },
};

//导出
let { flag, test } = require('moduleA');

//等同

let _m1 = require('moduleA');
let flag = _m1.flag;
let test = _m1.test;
```

### es6

- export
- import

```javascript
//模块化js,避免命名冲突
<script type="module"></script>

// 统一导出
export {
    变量,函数,对象
}

// 单独导出
export var val1 = 100

export function aaa(){}

export class Person(){}

//唯一导出,导出可自定义名字
export default name

-----

//导入
import {变量,函数,对象} from './a.js'

import *  as name from './a.js'
```

导入导出

---

## webpack

> 依赖 node.js

主要功能

1. 静态`模块`打包工具
2. 前端模块化工具
3. 代码混淆压缩
4. 浏览器 js 兼容性

5. 性能优化

基本使用

```bash
webpack ./src/js/main.js ./dist/js/bundle.js
```

> 报错可在前面加上 `npx`

### 其他打包工具:grunt/gulp

> 核心为 Task,前端自动化任务管理工具  
> 没或少使用模块化时可使用

1. 配置`task`,并且定义 task 要处理的事务(ES6,ts 转化,图片压缩,scss 转 css 等)
2. 使用工具依次执行 task

### webpack 插件

1. webpack-dev-server

```bash
npm i webpack-dev-server  -D
// wepback 自动打包 类似 nodemon

webpack.config
  script
    dev: 'webpack serve'
```

2. html-webpack-plugin

```js
npm i html-webpack-plugin
// webpack index copy

// webpack.config.js
const HtmlPlugin= require('html-webpack-plugin')
const htmlPlugin = new HtmlPlugin({
  template: './src/index.html',
  filename: './index.html'
})

module.exports = {
  plugins: [htmlPlugin]
}

```

### webpack 配置

> [第三方中文文档](https://v4.webpack.docschina.org/concepts/loaders/)

#### 3.1 webpack.config.js

> 默认配置文件

```javascript
//CommonJS
const path = require('path');
module.exports = {
  mode: 'development',
  // production 开发模式 or 发布
  entry: './src/main.js',
  // 打包入口文件路径
  output: {
    // 输出路径
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
  plugins: [],

  devServer: {
    // 配置 webpack-dev-devserver
    open: true, // 初次打包自动打开浏览器
    host: '127.0.0.1',
    port: 80,
  },
};
```

> 修改 `webpack.config.js` 或者 `package.json` 后，需重启实时打包服务器

#### 3.1.2 packge.json

> 1. `npm run`默认使用全局安装的包
> 2. 配置文件中使用局部安装的包
> 3. 也可直接`"build": "E://Code/2021/vue/node_modules/.bin/webpack"`使用统一包
> 4. 包默认使用`node_modules/.bin/webpack`

```bash
# 初始化
npm init

# script中配置脚本,使用方法
npm run 脚本名
```

### loader

webpack 处理非 js 文件的 module

#### 3.2 css 配置

使用 loader 过程

1. npm 安装需要的 loader
2. webpack.config.js 下的 modules 进行配置

安装相关 loder:

```bash
cnpm install --save-dev css-loader
cnpm install --save-dev style-loader
```

webpack.config.js 配置文件:

```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [{ loader: 'style-loader' }, { loader: 'css-loader' }],
      },
    ],
  },
};
```

之后重新生成即可

> use 中 loader 默认从末尾开始处理，后写的 loader 先执行

#### 3.3 less 配置

1.安装 loader

```bash
npm install less less-loader --save-dev
```

2.添加 rules

```javascript
 rules: [{
        test: /\.less$/,
        use: [ // compiles Less to CSS
          "style-loader",
          "css-loader",
          "less-loader",
        ],
      }],
```

#### 3.4 图片处理

1.loader

```bash
cnpm install url-loader file-loader --save-dev
```

2.rules

```javascript
  rules: [{
        test: /\.(png|jpg|gif)$/,
        // use: 'url-loader?limit=22222' <=的img才会转为base64
        use: [{
            loader: 'url-loader',
            options: {
              limit: 8192,
              // 配置保存格式
              name: 'img/[name].[hash:8].[ext]'
            },
          }],
      }],
```

3.url 处理需要在`output`中添加`publicPath`

```javascript
 publicPath: "dist/",
```

> 之后所有`url-loader`处理的都会输出该目录

#### 3.5 babel

ES6 转 ES5，处理高级语法等

1.安装 loader

```bash
cnpm install babel-loader babel-core babel-plugin-proposal-decoorators babel-preset-es2015 --save-dev
```

2.配置 rules

```javascript
rules: [
  {
    test: /\.js$/,
    exclude: /(node_modules|bower_components)/,
    use: {
      loader: 'babel-loader',
      options: {
        presets: ['es2015'],
      },
    },
  },
];
```

#### webpack 配置 vue

1.安装 vue 的包

```bash
cnpm install --save vue
```

2.配置 main.js

```javascript
import Vue from 'vue';

const app = new Vue({
  el: '#vueDom',
  data: {
    message: 'Vue',
  },
});
```

3.配置 vue 文件支持

```bash
cnpm install --save-dev vue-loader vue-template-compiler
```

### webpack-plugin

> 对现有架构扩展

#### 版权声明

配置文件

```javascript
const webpack = require('webpack');

module.exports = {
  plugins: [new webpack.BannerPlugin('')],
};
```

#### 打包 html

1.下载 `html-webpack-plugin` 包

```bash
cnpm install --save-dev html-webpack-plugin
```

2.修改 plugins 配置

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin');
new HtmlWebpackPlugin({
  template: 'index.html',
});
```

> 此时的`PublicPath`多余应删除
> 初始`html`文件,可不用引用`js`,模板也可在插件配置文件中定义

#### 压缩 js

1.下载 `uglifyjs-webpack-plugin` 包

```bash
cnpm install --save-dev uglifyjs-webpack-plugin@1.1.1
```

2.修改 plugins 配置

```javascript
new UglifyjsWebpackPlugin();
```

#### 配置本地服务器

> 实现修改后自动更新 js 文件

1.下载 webpack-dev-server@2.9.3

```bash
cnpm install --save-dev webpack-dev-server@2.9.3
```

2.修改配置文件(webpack.config.js)

```javascript
devServer: {
    contentBase: './dist',
    inline: true
}
```

3.配置 script

```json
"script":{
    "dev": "webpack-dev-server --open"
}
```

#### 配置文分拆合并

1.安装合并处理插件

```bash
cnpm install --save-dev webpack-merge@4.1.5
```

2.修改不同配置(简单 prodction 示例)

```javascript
const UglifyJsPlugin = require('uglifyjs-webpack-plugin');
const WebpackMerge = require('webpack-merge');
const base = require('./base.js');

module.exports = WebpackMerge(
  (module.exports = { base, plugins: [new UglifyJsPlugin()] }),
);
```

3.`packge.json`

```json
"build": "webpack --config 配置文件路径"
```

4.修改生成路径

--

## ESLint

统一开发风格
