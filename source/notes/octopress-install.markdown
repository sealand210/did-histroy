---
layout: page
date: 2012-03-16 14:03
footer: false
sidebar: false
---



最近一直想找个简单好用的博客平台，方便整理和收集教程与资料。一开始选中了*wordpress.com*，设置简单，免费主题也有很多，但是缺点是速度太慢，而且还要挖地道才能看，想自己搭一个*wordpress*博客，但是又没找到好的免费平台，所以最后还是选择了用Octopress在github和heroku上搭站。这两个虽然也是国外的站点，但是因为Octopress无需*SQL*数据库，只是通过ruby将*markdown*文件生成html，所以浏览速度还是比较快的。

下面就是简略的安装过程：


<!-- more -->


## 环境搭建

**Mac OSX Lion系统（实测10.7.3）：**

1.安装*HomeBrew*，这是一个程序管理工具，类似Ubuntu的apt-get. 可以极大的简化安装过程。
	
	$ mkdir -p /usr/local/Cellar	#避免BUG出现
	$ /usr/bin/ruby -e "$(/usr/bin/curl -fsSL https://raw.github.com/mxcl/homebrew/master/Library/Contributions/install_homebrew.rb)"	

2.使用*HomeBrew*来自动安装git:

	$ brew install git


3.安装Ruby编译环境(通过RVM管理器)：

{%codeblock%}

$ bash -s stable < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)
$ rvm get head
$ rvm install 1.9.2 	#也可以选择1.9.3
$ rvm 1.9.2 --default

{%endcodeblock%}

完成后环境的搭建就大致结束了，需要POW的话也可以安装POW:

	$ curl get.pow.cx | sh


**Ubuntu/Debian Linux系统（实测Lubuntu 11.10）：**

1.由于Ubuntu和Debian都自带很方便的APT管理工具，直接先安装git就行了:
		
	$ sudo apt-get install git-core git-gui git-doc
		
2.设定git SSh密匙，和git用户全局参数，参照www.github.com

3.安装Ruby编译环境(通过RVM管理器)：

{%codeblock%}
$ bash < <(curl -sk https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)
$ echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm"' >> ~/.bashrc
$ source ~/.bashrc
$ sudo apt-get install build-essential openssl libreadline6 libreadline6-dev zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-0 libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev autoconf libc6-dev libncurses5-dev automake libtool bison subversion
$ rvm install 1.9.2			#也可以选择1.9.3
$ rvm use 1.9.2 --default
{%endcodeblock%}

三步就完成了ubuntu的安装，环境搭建中最耗时的就是ruby的安装，因为是编译安装，cpu比较慢的电脑需要较长时间的等待。曾尝试过使用apt安装ruby,安装会快很多，但是使用ruby安装bundler的时候会出错, 不知道是为什么。



## 安装Octopress章鱼出版社

**全新安装Octopress：**

下载和安装最新的Octopress:
{%codeblock%}
$ git clone git://github.com/imathis/octopress.git octopress
$ cd octopress		
$ gem install bundler #安装依赖包：
$ bundle install
$ rake install	#安装默认主题	
{%endcodeblock%}

5.生成网站：
{%codeblock%}
$ rake generate #生成html
$ rake preview	#测试浏览(localhost:4000)：
$ rake deploy #发布到github
{%endcodeblock%}
	
这时应该就可以在username.github.com看到octopress的页面
	
	
7.将源码保存到github的source branch

	$ git push origin HEAD:source
			 

	 
## 初步使用和设置Octopress章鱼出版社

octopress的初步设置很简单，就是文件目录下 `_config.yml` 这个文件:

**主要设置**

{%codeblock%}
url:                # For rewriting urls for RSS, etc
title:              # Used in the header and title tags
subtitle:           # A description used in the header
author:             # Your name, for RSS, Copyright, Metadata
simple_search:      # Search engine for simple site search
description:        # A default meta description for your site
subscribe_rss:      # Url for your blog's feed, defauts to /atom.xml
subscribe_email:    # Url to subscribe by email (service required)
email:              # Email address for the RSS feed if you want it.
{%endcodeblock%}
其他的插件，第三方工具的设置也在该文件内。

**发表博文**

使用指令：

	$ rake new_post["tittle"]
		
就可以快速创建博文，然后使用文档工具打开source/_post/下的markdown文件就可以开始使用markdown编写博客了。Mac下推荐使用Mou编辑工具，Linux下推荐使用Retext编辑工具，使用这种工具的好处是自动预览和自动语法标注。





## 参考连接：

* <http://rubysource.com/installing-ruby-with-rvm-on-ubuntu/>
* <http://blog.4321.la/articles/2012/01/25/set-up-octopress/>
* <http://stackoverflow.com/questions/8000145/ruby-rvm-llvm-and-mysql>
* <http://mrzhang.me/blog/blog-equals-github-plus-octopress.html>
* <http://www.frederico-araujo.com/2011/07/30/installing-rails-on-os-x-lion-with-homebrew-rvm-and-mysql/>
* <http://geekontheway.github.com/blog/archives/>



