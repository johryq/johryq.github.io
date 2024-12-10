---
title: "Grpc"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T08:54:42+08:00
draft: false
keywords: []
description: ""
tags: ['grpc']
categories: ['code']
author: "2332334"

---
<!--more-->

# gRPC

google开源分布式远程服务调用

server提供api grpcClient主流编程语言进行调用，类似web api

基于http2 通信二进制流

server - proto - client

## Protocol buffers

客户端与服务端见通信协议

缺点：

1. 其消息一次性加载到内存
2. 完全解析二进制数据才能知道数据是否相等
3. 消息未压缩
4. 大型多维浮点数组等科学和工程用途的运算，效率不是最佳
5. 科学计算非面向对象 缓冲期对其支持不太好
6.

### 定义server四种形式

```proto
// 一元rpc
rpc SayHello(HelloRequest) returns (HelloResponse);

// 服务器流式响应
rpc LotsOfReplies(HelloRequest) returns (stream HelloResponse);

// 客户端流式请求
rpc LotsOfGreetings(stream HelloRequest) returns (HelloResponse);


// 双向流式沟通
rpc BidiHello(stream HelloRequest) returns (stream HelloResponse);
```

```proto
syntax = "proto3"; 
// 指定proto版本

pcakage a.b 
// 类似命名空间

import "myproject/other_protos.proto"; 
import public "a.proto"; 
// 导入其他prot文件中定义的proto
// 该功能java没有；
// 移动文件后编译器可通过 -I 设定proto文件所在目录即 proto_path
// 2版本proto不能在3版本proto中直接使用，反之亦然

message Foo{
  reserved 2,15,2 to 100, 1000 to max;
  reserved "foo", "bar";
}
// reserved 该属性设定保留字段；字段名称和字段编号不能混用

message SearchResponse {
  message Result {
    string url = 1;
    string title = 2;
    repeated string snippets = 3;
  }
  repeated Result results = 1;
}
// 嵌套定义
message SomeOtherMessage {
  SearchResponse.Result result = 1;
}
// 重用上方定义消息

service SearchService {
  rpc Search(SearchRequest) returns (SearchResponse);
}

```

### 字段

message

```proto
message Person {
  string NAME = 0;
  string AGE = 1;
}
```

字段编号，每一个字段都有一个唯一编号

该编号范围，1 - 2^29^-1 ;即 1 - 536,870,911

> 19000 - 19999 为保留字段

enum

```proto
enum EnumAlias {
  EA_UNSPECIFIED = 0; // 该值必须为0
  EA_NAME = 1;
}
```

1. enum 第一个定义必须为0；用于与proto2语义兼容
2. 定义范围为 `32整数` 范围
3. 负值使用varint编码，效率不高，不推荐使用

oneof

```proto
message SampleMessage {
  oneof test_oneof {
    string name = 4;
    SubMessage sub_message = 9;
  }
}
```

1. oneof 表示该字段只会在内存中存在一个
2. 其内字段共享该内存
3. 不可使用map 和repeated字段

map

```proto
map<key_type, value_type> map_field = N;
map<string, Project> projects = 3;
// key_type 可设类型为 stirng 或任意整数
// map 不可 repeated

message MapFieldEntry {
  key_type key = 1;
  value_type value = 2;
}

repeated MapFieldEntry map_field = N;
```
