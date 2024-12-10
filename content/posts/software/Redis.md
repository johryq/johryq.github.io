---
title: "Redis"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:05:21+08:00
draft: false
keywords: []
description: ""
tags: []
categories: ['software']
author: "2332334"

---
<!--more-->
# Redis

node.js 操作redis

[官方相关客户端推荐列表](https://redis.io/resources/clients/)

## redis基本数据类型

- string

```redis

```

- hash

- list

- set

- zset 有序集合

## [iredis](https://iredis.io/)

redis命令行客户端

1. 连接reids

```bash
iredis -h host -p port -a password -n databaseNumber
```

2. redis基本使用

```redis
SET ket_name value
DEL key
GET key
```

## [node-redis](https://redis.js.org/#node-redis-installation)

基本使用

```js
import { createClient } from 'redis';

const client = createClient();

client.on('error', (err) => console.log('Redis Client Error', err));

// host:port
// createClient({
//   url: 'redis://alice:foobared@awesome.redis.server:6380'
// });
await client.connect();

await client.set('key', 'value');
const value = await client.get('key');
await client.disconnect();
```
