---
layout: page
title: 欢迎来到Ilcwd的博客
tagline: 
---

{% include JB/setup %}



##关于我
---

SYSU 2011年出品，SS小本。

目前主要负责服务端后台开发。

常用Python，最近比较有兴趣的东西：git，golang，HTML5。

比较熟悉的东西：

>Python2，MySQL，Redis，Memcache，Nginx，uWSGI，Linux，Java，C/CPP，分布式服务，高并发高访问的大型服务开发。


有事联系: 
>ilcwd23 (#) gmail.com  

##最近博客列表
- - -

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

