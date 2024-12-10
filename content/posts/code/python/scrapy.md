---
title: "Scrapy"
date: 2024-12-03T16:40:21+08:00
lastmod: 2024-12-03T16:40:21+08:00
draft: false
keywords: []
description: ""
tags: ['scrapy']
categories: ['python']
author: "2332334"

---
<!--more-->

# Scrapy

> [中文文档](https://scrapy-chs.readthedocs.io/)  
> [官方文档](https://docs.scrapy.org/en/latest/)

## 安装

``` bash
pip install scrapy
```

### 示例

``` bash
pip install scrapy
cat > myspider.py <<EOF
import scrapy

class BlogSpider(scrapy.Spider):
    name = 'blogspider'
    start_urls = ['https://www.zyte.com/blog/']

    def parse(self, response):
        for title in response.css('.oxy-post-title'):
            yield {'title': title.css('::text').get()}

        for next_page in response.css('a.next'):
            yield response.follow(next_page, self.parse)
EOF
scrapy runspider myspider.py
```

## 相关cli

```bash
scrapy startproject [projectName]
# 新建Scrapy项目

scrapy genspider [spiderName] ["domain"]
# 新建爬虫并指定域名

scrapy crawl [spiderName]
# 运行该爬虫

scrapy crawl [spiderName] -o [fileName]
# 保存数据[json/jsonl/csv/xml]

scrapy runspider [spiderName.py]
# 未创建项目运行爬虫

scrapy list
# 列出项目中的爬虫
```

## header

### 1.修改settings配置文件

```python
# Override the default request headers:
DEFAULT_REQUEST_HEADERS = {
  'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8',
  'Accept-Language': 'en',
}
```

### 2.重新爬虫中的start_request

```python
# -*- coding: utf-8 -*-
import scrapy
import random
 
class ShortSpider(scrapy.Spider):
    name = 'short'
    allow_domains = ['movie.douban.com']
    # 重写start_requests方法
    def start_requests(self):
        # 浏览器用户代理
        ua_list = ["Mozilla/5.0 (Macintosh; Intel Mac OS X 10.6; rv2.0.1) Gecko/20100101 Firefox/4.0.1",

               "Mozilla/5.0 (Windows NT 6.1; rv2.0.1) Gecko/20100101 Firefox/4.0.1",

               "Opera/9.80 (Macintosh; Intel Mac OS X 10.6.8; U; en) Presto/2.8.131 Version/11.11",

               "Opera/9.80 (Windows NT 6.1; U; en) Presto/2.8.131 Version/11.11",

               "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_0) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11"

               ]
        url_agent = random.choice(ua_list)
        headers = {
            'User-Agent':url_agent
        }
        # 指定cookies
        cookies = {
            'key':'value',
            'key':'value',
            'key':'value'
        }
        urls = [
            'https://movie.douban.com/subject/26266893'
        ]
        for url in urls:
            yield scrapy.Request(url=url, headers=headers, cookies=cookies, callback=self.parse)
```

## domain

未能运行callback函数的处理方法

### 1.scrapy.Request

添加 `dont_filter=True` ,即不进行域名检查

```python
# example
yield scrapy.Request(url=slogansurl,callback=self.parse_slogans,meta={'item': item },dont_filter=True)
```

## 参考

+ [scrapy设置headers，cookies](https://blog.csdn.net/weixin_44508906/article/details/87895868)
