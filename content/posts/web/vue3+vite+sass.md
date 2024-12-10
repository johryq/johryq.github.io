---
title: "vue3+vite+sass"
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
# vue3+vite+sass

## 1.安装sass

```base
//  --save-dev
pnpm i sass -d 
```

## 2.配置vite.config

```js
export default defineConfig({
  // CSS 预处理器
  css: {
    preprocessorOptions: {
      // 定义sass变量
      scss: {
        additionalData: `@import './src/assets/styles/variables.scss';`,
      },
    },
  },
});
```

## 3. vue文件中使用sass

```vue
<style lang='scss' scoped>
</style>
```
