---
layout: post
title: "Octopress试用第三方主题"
date: 2014-12-24 14:11:00 +0800
comments: true
categories: 
---

第三方主题[链接](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes).

如果你能在上面的链接中找到满意的主题，可以按照主题的要求去安装部署。比如，如果你喜欢[CleanPress](https://github.com/macjasp/cleanpress)这款主题，你可以执行以下命令：

	cd octopress
	git clone git://github.com/macjasp/cleanpress.git .themes/cleanpress
	rake install['cleanpress']
	rake generate

<!--more-->

请注意，格式请严格按照如上所示，否则可能发生不可预料的错误...

另外，其实其他人的主题对于自己，或多或少有一些不满意的地方。完美主义者如我，还是不要用模版，尽量自己慢慢学习，自己布置主题。