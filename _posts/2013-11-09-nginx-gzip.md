---
layout: post
title: "Nginx下开启Gzip压缩"
description: ""
category: 
tags: []
---
{% include JB/setup %}


## Nginx下开启Gzip压缩

通过对HTTP的返回结果进行Gzip压缩，可以显著减少传输字节，节省流量，从而提高响应速度。
使用Gzip会稍微增加服务端和客户端的CPU负载，但是还是在可以接受的范围内。

开启Gzip需要3方面支持。

### Ngnix 配置

Nginx需要在编译的时候启用Gzip模块，默认情况下都是开启的，编译的时候注意需要先安装zlib库。

压缩比参数`gzip_comp_level`，可以是0 - 9之间任意证书，一般使用最快的 0 或者 1，实际测试中，0和9压缩速度相差10倍，但是压缩率只减少10%。

`gzip_min_length` 指定返回结果大于给定值（bytes）才会压缩，注意如果返回 header 中没有 `Content-Length` ,这个选项是不起作用的。

`gzip_http_version` 使用哪个HTTP协议，默认是1.1。

比较重要的是`gzip_types`，定义的是哪些资源（`Content-Type`的值）才会被压缩。默认是
>gzip_types text/html;
但是这样的话js，css等就不会被压缩了，可以设置成(注意的是`text/html`是默认就有了)
>gzip_types text/plain application/x-javascript text/css application/xml text/javascript ;
jpeg，png等图片资源一般是经过压缩的，不用再压缩。
由于我的服务是只是API，所以用 `*` 指定可以压缩任何类型的响应结果。


贴一段我的nginx配置：

	gzip on;
	gzip_comp_level 1;
	# 使用32个4k的buffer进行压缩，按默认的就好。
	gzip_buffers 32 4k
	gzip_min_length 20;
	gzip_http_version 1.1;
	gzip_types *;
	# 是否返回 Vary: Accept-Encoding ，没什么用
	gzip_vary off;


### 应用服务配置

如果nginx后端有自己的应用服务，有2点需要注意：

* 如果没有返回Content-Length，那么 gzip_min_length 是不生效的；
* 如果 nginx 设置了 gzip_types ，那么必须和应用返回的严格对应（如果gzip_types 是 * 就没所谓了）。

Python使用WSGI或者web.py设置`Content-Type`的方法：

	# WSGI 返回 content-type 方法
	def application(env, start_response):
	    start_response("200 OK", [("Content-Type", "application/json")])
	    # ...
	 
	 
	# web.py 返回 content-type 方法
	import web
	web.header('Content-Type', 'application/json')



### 客户端配置

1. 客户端的请求必须指明是 HTTP 1.1协议；
2. 请求 Header 的 Accept-Encoding 需要有 gzip 字段。

一段请求例子：


	# telnet 0.0.0.0 80
	Trying 0.0.0.0...
	Connected to 0.0.0.0 (0.0.0.0).
	Escape character is '^]'.
	GET /10 HTTP/1.1
	User-Agent: curl/7.15.5
	Host: 0.0.0.0
	Accept: */*
	Accept-Encoding: gzip
	 
	HTTP/1.1 200 OK
	Server: nginx
	Date: Thu, 31 Oct 2013 04:56:33 GMT
	Transfer-Encoding: chunked
	Connection: keep-alive
	Vary: Accept-Encoding
	Content-Encoding: gzip
	 
	 
	15
	<压缩后的数据，就不显示了>
	0
	 
	GET /10 HTTP/1.1
	User-Agent: curl/7.15.5
	Host: 0.0.0.0
	Accept: */*
	 
	 
	HTTP/1.1 200 OK
	Server: nginx
	Date: Thu, 31 Oct 2013 04:59:21 GMT
	Transfer-Encoding: chunked
	Connection: keep-alive
	Vary: Accept-Encoding
	a
	aaaaaaaaaa
	0
