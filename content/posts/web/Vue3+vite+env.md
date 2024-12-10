---
title: "Vue3 + vite 配置env环境变量"
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

# Vue3 + vite 配置env环境变量

## 1. 添加环境变量配置文件

```bash
touch .env.development

touch .env.production

touch .env.test
```

基本内容

```txt
VITE_MODE_ENV=development

VITE_APP_TITLE=开发环境

VITE_API_BASE_URL=''
```

需要`VITE`前缀才可识别该环境变量

```ts
export default defineConfig({
  envPrefix: 'XX' // 可通过配置该变量修改为你需要的前缀
})
envPrefix
```

默认放在项目根目录下，如需保存至制定目录

```ts
// 修改vite.config.ts
export default defineConfig({
  envDir: './src/env' // 添加该条内容即可
})
```

## 2. 添加ts智能提示

```ts
// 修改 env.d.ts
// 添加入下内容
interface ImportMetaEnv {
  readonly VITE_APP_TITLE: string
  // 更多环境变量...
}

interface ImportMeta {
  readonly env: ImportMetaEnv
}
```

## 3. 使用模式 以及 vue中获取环境变量值

通过配置 `package.json` 修改 `scripts`

```json
vite build --mode dev
```

vue中获取环境参数的值

```ts
console.log(import.meta.env.VITE_API_BASE_URL) 
```

## 参考链接

+ [vite官网](https://vitejs.cn/vite3-cn/guide/env-and-mode.html#env-variables)
+ [vite doc2](https://vitejs.cn/vite3-cn/config/shared-options.html#envprefix)
