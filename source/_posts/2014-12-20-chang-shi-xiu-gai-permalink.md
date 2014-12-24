---
layout: post
title: "尝试修改permalink"
date: 2014-12-20 22:54:29 +0800
comments: true
categories: 技术探索|Octopress|独立博客
---
在上一次成功构建网站后，我发现以前的permalink是这样的：

	permalink: /blog/:year/:month/:day/:title/ #文章固定链接
	
这种层级太多了，对于个人博客来说，是不必要的。于是，我尝试修改成：

	permalink: /blog/:title.html/ #实现第二种	
	
但是，就开始各种rake deploy失败，或者deploy成功，原来文章的链接访问都会404。
在Google各种解决方案不成功后，我去查了jekyll的官方文档，发现里面是这么描述permalink的：

"Jekyll 支持一种灵活的方式来建立网站的URLs,你可以为一篇文章指定固定的URL，你可以选择内置样式来创建你的链接"，默认风格是：date。

网站的永久链接，通过URL模版来创建，其中动态元素由冒号为前缀的关键字来表示。例如，默认的date固定链接被定义为： 

	/:categories/:year/:month/:day/:title.html 
	
##内置固定链接样式
注意：这些可能仅适用于文章，而不是网页，集合或者静态文件。网页，集合或者静态文件有自己指定的链接方式。

|永久链接样式 | URL模版 | 
|------------- | ----------------|
|date       | /:categories/:year/:month/:day/:title.html |
|pretty     | /:categories/:year/:month/:day/:title/ |
|none       | /:categories/:title.html  	|
	
	
##举例

给定一个post，它的名字为：/2009-04-29-slap-chop.textile

永久链接样式                      | URL模版 | 
-----------------               | ----------------------
date或者为空                      | /2009/04/29/slap-chop.html 
pretty                          | /2009/04/29/slap-chop/index.html
/:month-:day-:year/:title.html  | /04-29-2009/slap-chop.html
/blog/:year/:month/:day/:title  |  /blog/2009/04/29/slap-chop/index.html

 于是，我在_config.yml文件里，将permalink改为none，再commit，push。文章页面都可以顺利访问了！
 
 成功，一个平淡无奇的12月里的周六，解决了一个技术问题。嘿嘿～开森～