---
layout: post
title: "搭建github pages个人博客"
description: ""
category: 
tags: []
---
{% include JB/setup %}


##简介

github pages 可以在 `YOURNAME.github.io/YOUR_REPO` 上显示你的repo上的静态页面。

github pages可以通过[Jekyll](http://jekyllrb.com )生成你的静态页面，上传到github上的文件，会在10分钟内生成好静态文件。
Jekyll支持 [markdown](http://daringfireball.net/projects/markdown/ ) 和 [Liquid](http://wiki.shopify.com/Liquid ) 模板语言，可以分别用 *.md 或者 *.html 扩展名写自己的博客。

另外使用 [jekyll-bootstrap](http://jekyllbootstrap.com) 框架，可以省很多事情。
 

##安装

###安装jekyll
rubygem版本需要大于1.3.7，我的ubuntu10.04需要重新下载最新的rubygems……

	sudo apt-get install ruby
	sudo gem install jekyll


###建立gh-pages

安装jekyll-bootstrap

	git clone https://github.com/plusjade/jekyll-bootstrap.git ilcwd.github.io
	cd ilcwd.github.io
	git remote set-url origin https://github.com/ilcwd/blog.git
	git push origin master

建立orphan 分支 gh-pages （一定要这个名字）。

	git checkout --orphan gh-pages

jekyll本地运行会生成静态文件在 `_site` 文件夹里面，因此需要把 `_site` 文件夹加入到ignore列表。

	echo "_site/" >> .gitignore


弄好后执行下面命令，就可以看到你的页面了。`-w` 参数表示有改动自动加载新页面。

	jekyll serve -w 


###个性化

显得专业一点，删除默认页面。

	rm -rf _posts/core-samples


修改 `_config.yml` 文件，写上自己的个性化信息。

	title : 阿拉斯加长脚蟹
	tagline: Python, golang, HTML
	author :
	  name : ilcwd
	  email : ilcwd@qq.com
	  github : ilcwd
	  twitter : ilcwd
	  feedburner : ilcwd



安装[主题](http://jekyllbootstrap.com/usage/jekyll-theming.html )
我比较喜欢twitter风格。

	rake theme:install git="https://github.com/jekyllbootstrap/theme-twitter.git"


###评论系统

由于github pages是静态网页，如果要用评论，只能使用评论系统，
默认是disqus，是用fb和twitter账号，在墙内还是用国内的评论系统，
我这里用的是[多说](http://duoshuo.com/ )。


新建 `./_includes/custom/comments` 输入下面内容

	<!-- Duoshuo Comment BEGIN -->
	<div class="ds-thread"></div>
	<script type="text/javascript">
	var duoshuoQuery = {short_name:"YOUR_DUOSHUO_ID"};
	     (function() {
	          var ds = document.createElement('script');
	          ds.type = 'text/javascript';ds.async = true;
	          ds.src = 'http://static.duoshuo.com/embed.js';
	          ds.charset = 'UTF-8';
	          (document.getElementsByTagName('head')[0] 
	          || document.getElementsByTagName('body')[0]).appendChild(ds);
	     })();
	     </script>
	<!-- Duoshuo Comment END -->


修改 \_config.yml 文件

	comments :
		provider : custom


这个主题下，只有post类型的页面才显示评论，跟踪这个模板的代码很久才发现这点……


###新建博客

	rake post title="Hello World"

新的博客页面里面的

	include JB/setup

不要手贱删掉，有很多初始化变量的设置……


随便写点东西可以上传到github上了。

	git push origin gh-pages

