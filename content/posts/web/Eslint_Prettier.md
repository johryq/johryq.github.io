---
title: "vscode Eslint Prettier 配置"
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
# vscode Eslint Prettier 配置

## [Eslint](https://eslint.org/)

> [中文网站](http://eslint.cn/)

ESLint最初是由Nicholas C. Zakas 于2013年6月创建的开源项目。它的目标是提供一个插件化的javascript代码检测工具。

+ 提供较为严格的代码格式检测
+ 团队风格一致

### 基本使用指南

```bash
# 使用这个即可进行初始化eslint
npm init @eslint/config

# 使用的项目上安装，纵使全局安装也要
npm install eslint --save-dev

# 初始化 .eslintrc 文件
eslint --init
```

```json
{
    "rules": {
        "semi": ["error", "always"],
        "quotes": ["error", "double"]
    }
}
```

> "extends": "eslint:recommended" 该配置会开启规则中所有为推荐的

+ "off" or 0 - 关闭规则
+ "warn" or 1 - 将规则视为一个警告（不会影响退出码）
+ "error" or 2 - 将规则视为一个错误 (退出码为1)

## [Prettier](https://prettier.io/)

> [中文网站](https://www.prettier.cn/)

保存代码时格式化代码的工具

### 基本使用

```bash
# vscode中安装
ext install esbenp.prettier-vscode

npm install --save-dev --save-exact prettier

# 创建该文件让
echo {}> .prettierrc.json

# 该配置说明那些无需格式化
touch .prettierignore
```

## vscode 结合 eslint Prettier

相关插件安装

```bash
npm install --save-dev eslint-plugin-prettier
npm install --save-dev --save-exact prettier
npm install --save-dev eslint-config-prettier
```

配置.eslintrc.json

```json
{
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error"
  },
  // 放最后一个
  "extends": ["plugin:prettier/recommended"]
}
```

1. eslint-config-prettier

> 关闭所有不必要或可能与 Prettier 冲突的规则插件

### styleLint

```bash
# install
npm install --save-dev stylelint-config-prettier
```

```json
// 配置.stylelintrc
{
  "extends": [
    // other configs ...
    // 放在最后
    "stylelint-config-prettier"
  ]
}
```
