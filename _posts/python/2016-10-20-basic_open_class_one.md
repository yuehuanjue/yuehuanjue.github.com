---
layout: article
title: HTTP协议（入门）
description:  主要介绍的是 HTTP 协议的历史演变和设计思路。主要来源于阮一峰的网络日志--HTTP协议入门
updateData:  15:00-- 2016/10/26
categories: [HTTP协议]
share: false
image:
  feature: 
  teaser: 
  credit: yuehuanjue
---


## HTTP 协议是互联网的基础协议，也是网页开发的必备知识，最新版本 HTTP/2 更是让它成为技术热点。


### 一、http（0.9）


HTTP是基于**TCP/IP**协议的应用层协议。它不涉及数据包（packet）的传输，主要规定了客户端和服务器之间的通信格式，默认使用80端口。

最早版本是1991年发布的0.9版，该版本只提供了命令GET。

```
GET/index.html

```
该命令表示，TCP连接建立后，客户端向服务器请求（request）网页index.html。

此时的协议规定，服务器只能回应HTML格式的字符串，不能回应别的格式。


服务器发送**完毕**，就__关闭__了TCP的连接。


### 二、http(1.0)

##### 2.1 新增内容

1996年5月，1.0的版本发布，内容做了大量的增加。

1，任何格式的内容都可以发送。此时的互联网可以传送文字，图像，视频，二进制文件。

2，除了`GET`命令，还引入了`POST`命令和`HEAD`命令。

3，HTTP请求和回应的格式也变了，除了数据部分，每次通信都必须包括头信息（HTTP header), 用来描述一些元数据。

4，其他新增的功能还包括状态码（status code）、多字符集支持、多部分发送（multi-part type）、权限（authorization）、缓存（cache）、内容编码（content encoding）等。

##### 2.2 请求格式

```
GET / HTTP/1.0
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_5)
Accept: */*

```

第一行是请求命令，必须在尾部添加协议版本`（HTTP/1.0）`。后面就是多行头信息，描述客户端的情况。


