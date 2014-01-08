---
layout: post
title: "Linux下跨服务器文件传输"
description: ""
category: 
tags: []
---
{% include JB/setup %}



##scp
需要本机能ssh到目标机器


	# 文件
	scp test.file 172.16.2.130:/data
	 
	# 目录
	scp -r test.d 172.16.2.130:/data
	 
	# 还能这样，用本机做中转
	scp -r 172.16.2.130:/data/test.d 172.16.2.131:/data
 
##nc
nc不用依赖ssh，使用起来更方便,

速度更快

	# 文件
	## server
	nc -l 12345 > data.out
	 
	## client
	nc 172.16.2.130 12345 < data.in
 
	# 不支持目录
 
##nc+tar
tar可以支持压缩和文件夹

gzip，scp也可以进行压缩

	## server
	nc -l 12345 | tar -zxvf -
	## client
	tar -zcf - test.d | nc 172.16.2.130 12345
 
##nc+qpress
qpress压缩速度快，压缩比高的情况下可以加快速度，还能节省流量

	##client
	qpress -rovf  test.d | nc  172.16.2.130 12345
	 
	##server
	nc -l 12345 | qpress -divf /to/path

 
##重要

+ 无论用哪种方式，最好**校验md5/sha1** 

+ 传输速度和带宽，压缩比，压缩速度有关，还有就是使用的方便程度，实际情况请按需求来。

##References
1. [Linux大文件传输](http://www.yankay.com/linux%E5%A4%A7%E6%96%87%E4%BB%B6%E4%BC%A0%E8%BE%93/)

