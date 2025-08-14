---
title: "Android"
date: 2025-03-13T14:51:39+08:00
lastmod: 2025-03-13T14:51:39+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
# cover:
#     image: "" # image path/url
#     alt: "<alt text>" # alt text
#     caption: "<text>" # display caption under cover
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/<path_to_repo>/content"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---
<!--more-->
# android

```bash
# create keystore
keytool -genkey -alias testalias -keyalg RSA -keysize 2048 -validity 36500 -keystore test.keystore

# show keystore
keytool -list -v -keystore test.keystore  

```

## 参考

[Android平台签名证书(.keystore)生成指南](https://ask.dcloud.net.cn/article/35777)