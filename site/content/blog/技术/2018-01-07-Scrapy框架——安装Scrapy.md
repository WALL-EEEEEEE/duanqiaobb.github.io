
---
title: "Scrapy框架——安装Scrapy"
date: 2018-01-07 19:44:00 +0000 UTC
description: "Scrapy框架—— 安装Scrapy 需求配置安装sqlite依赖库编译python3.6编译Twisted安装Scrapy测试Scrapy是否成功安装Scrapy框架—— 安装Scrapy   Scrapy 可以说是爬虫界鼎鼎有名的框架。 它是一个重型的爬虫框架，结合数据抓取，导出，以及部分的数据清洗的功能。本文针在python3.6的环境下来安装scra"
tags: ["爬虫", "scrapy", "框架"]
---
- [Scrapy框架—— 安装Scrapy](#org88ed2e6)
  - [需求配置](#orge4da8aa)
    - [安装sqlite依赖库](#org1cb4355)
    - [编译python3.6](#org7a7d15b)
    - [编译Twisted](#orgc043478)
  - [安装Scrapy](#org8d9c314)
  - [测试Scrapy是否成功安装](#org845b7e6)


<a id="org88ed2e6"></a>

# Scrapy框架—— 安装Scrapy

&ensp;&ensp; `Scrapy` 可以说是爬虫界鼎鼎有名的框架。 它是一个重型的爬虫框架，结合数据抓取，导出，以及部分的数据清洗的功能。

```shell
本文针在python3.6的环境下来安装scrapy
```


<a id="orge4da8aa"></a>

## 需求配置

-   sqlite依赖库(centos下为sqlite-devel包)

&ensp;&ensp; `scrapy` 框架的正常运行，你的 `python3.6` 版本需要编译支持 `sqlite` ,

-   python3.6

-   Twisted

&ensp;&ensp; `scrapy` 的异步功能实现,需要 `Twisted` 的支持。 目前 `scrapy` 的最新版本需要 `Twisted>13.0` 版本, 而 `pip3.6` ， 所以我们需要从源码编译。


<a id="org1cb4355"></a>

### 安装sqlite依赖库

&ensp;&ensp; 如果你的 `python3.6` 已经编译支持了 `sqlite` ,可以跳过这个步骤。

1.  下载sqlite库

    ```shell
    yum install sqlite-devel
    ```


<a id="org7a7d15b"></a>

### 编译python3.6

1.  下载python3.6源码

    ```shell
    cd /tmp
    curl -O Python-3.6.4.tgz  https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tgz
    ```

2.  编译python3.6

    ```shell
    tar xvvf Python-3.6.4
    cd  Python-3.6.4
    ./configure
    make && make install
    ```


<a id="orgc043478"></a>

### 编译Twisted

1.  下载Twisted源码

    ```shell
    cd /tmp
    git clone https://github.com/twisted/twisted.git
    ```

2.  编译Twisted

    ```shell
    cd twisted/
    python3.6 setup.py install
    ```


<a id="org8d9c314"></a>

## 安装Scrapy

```shell
pip3 install scrapy
```


<a id="org845b7e6"></a>

## 测试Scrapy是否正常工作

&ensp;&ensp; 这里我们简单的抓一下京东首页的分类列表来测试一下 `scrapy` 是否正常工作。

```shell
scrapy genspider example www.jd.com //该命令会在当前目录下生成一个example.py文件
```

```python
//example.py
import scrapy


class ExampleSpider(scrapy.Spider):
    name = 'example'
    allowed_domains = ['www.jd.com']
    start_urls = ['http://www.jd.com/']

    def parse(self, response):
	category = response.xpath('//div[contains(@class,"navitems")]/ul/li/a/text()').extract();
	for cate in category:
	    yield {'cate': cate}
	pass
```

```shell
scrapy runspider example.py -L INFO -o category.json 
//该命令会运行example.py爬虫脚本，然后将抓取结果保存到category.json中
```

```json
//category.json
[
{"cate": "\u79d2\u6740"},
{"cate": "\u4f18\u60e0\u5238"},
{"cate": "PLUS\u4f1a\u5458"},
{"cate": "\u95ea\u8d2d"},
{"cate": "\u62cd\u5356"},
{"cate": "\u4eac\u4e1c\u670d\u9970"},
{"cate": "\u4eac\u4e1c\u8d85\u5e02"},
{"cate": "\u751f\u9c9c"},
{"cate": "\u5168\u7403\u8d2d"},
{"cate": "\u4eac\u4e1c\u91d1\u878d"}
]
```
















