---
layout: post
title: "Markdown入门指南"
date: 2014-12-18 15:18:31 +0800
comments: true
categories: 技术探索
---
##目录
1. 什么是 Markdown
2. 为什么需要 Markdown
3. 如何掌握 Markdown

   Markdown 基本语法（Basic Markdown）
   
   Markdown 扩展语法（GitHub Flavored Markdown）
   
   Markdown 高级用法
   
4. Markdown 相关资源
 
##什么是 Markdown

Markdown 是一种适用于网络书写的轻量级「标记语言」

Markdown 理念是能让文档更容易读、写和随意改。

Markdown 以纯文本发布，用简洁的语法代替排版。

下面是一段 Markdown 示例：


	 # Why *you* should use Markdown to write your next blog post

	 [Markdown][1] is just so dang legible, it will make your *whole life* easier. **I promise.**

	 [1]: http://daringfireball.net/projects/markdown/basics
	 
相比较，对应的 HTML Markup 语言是这样的：

	 <h1>Why <em>you</em> should use Markdown to write your next blog post</h1>

	 <p><a href="http://daringfireball.net/projects/markdown/">Markdown</a>
	 is just so dang legible, it will make your <em>whole life</em> easier. <strong>I promise.</strong>
	 </p>
	 
	 
怎么样，是不是感觉 Markdown 语言读、写起来都更清爽呢:-)

##为什么需要 Markdown
###Markdown 优点
纯文本，所以兼容性极强，可以用所有文本编辑器打开。

Markdown 的标记语法有极好的可读性。

让你专注于文字而不是排版。

格式转换方便，Markdown 的文本你可以轻松转换为 html、电子书等。

###谁在使用 Markdown
Markdown 诞生于互联网时代，更是由深谙互联网文本之道的 John Gruber 等人设计。因为 Ruby 与 Github 圈的极客们的热捧，以及来自 Github、Stackoverflow 等网站的大力支持（Github 和 Stackoverflow 的 Issues, comments, pull request descriptions and READMEs 都支持 Markdown 语法）。从一开始，就建立一个完整的生态链。

一切就这么简单。Markdown之所以在被鼓吹之后，越来越流行，不是因为它复杂，而是因为它足够简单。

###如何掌握 Markdown
Markdown 的语法十分简单。常用的标记符号不超过十个，5分钟即可掌握。应该是为数不多，你真的可以彻底学会的语言。

###基本 Markdown 语法
####1. 标题
	# 一级标题
 	## 二级标题
 	### 三级标题
 	#### 四级标题
 	##### 五级标题
	###### 六级标题
	
###2. 列表

	 - 无序列表1
	 - 无序列表2
	 - 无序列表3

	 1. 有序列表1
	 2. 有序列表2
	 3. 有序列表3
	 
###3. 引用

	> 这个是引用
	> 是不是和电子邮件中的
	> 引用格式很像
	
###4. 粗体与斜体

	 **这个是粗体**
	 *这个是斜体*
 	
###5. 图片与链接
####插入图片

	![baidu logo](http://www.baidu.com/img/bdlogo.png)
	
####插入链接

	[baidu](http://www.baidu.com/)
	
####图片链接

	[![][jane-eyre-pic]][jane-eyre-douban]

	[jane-eyre-pic]: http://img3.douban.com/mpic/s1108264.jpg
	[jane-eyre-douban]: http://book.douban.com/subject/1141406/
	
####6. 代码

用TAB键起始的段落，会被认为是代码块

	<php>
         echo “hello world";
    </php>
    
   
如果在一个行内需要引用代码，只要用反引号`引起来就好

	 Use the `printf()` function.
	 
###7. 分割线

可以在一行中用三个以上的星号、减号、底线来建立一个分隔线

	 ---
	 
注：更详细的 Markdown 基本语法，请参考[Markdown中文版语法说明](http://wowubuntu.com/markdown/)

##扩展 Markdown 语法（github扩展语法）

###1. 删除线

	 ~~Mistaken text.~~
	 
###2. 代码块与语法高亮

 ```ruby
 require 'redcarpet'
 markdown = Redcarpet.new("Hello World!")
 puts markdown.to_html
 ```
 
###3. 表格

	| Tables        | Are           | Cool  |
	| ------------- |:-------------:| -----:|
	| col 3 is      | right-aligned | $1600 |
	| col 2 is      | centered      |   $12 |
	| zebra stripes | are neat      |    $1 |
 
###4. 任务列表

	- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> are supported
	- [x] list syntax is required (any unordered or ordered list supported)
	- [x] this is a complete item
	- [ ] this is an incomplete item
	
**注1**：更详细的 Markdown 扩展语法，请参考[GFM（Github Flavored Markdown)](https://help.github.com/articles/github-flavored-markdown/)

**注2**：GFM扩展语法并非所有的 Markdown 编辑器都支持。

##其他高级用法

###Cross-reference (named anchor) in markdown

	Take me to [pookie](#pookie)

	 <a name="pookie"></a>
	 
参考这里（http://stackoverflow.com/questions/5319754/cross-reference-named-anchor-in-markdown）

###引用代码块中包含反引号

只需使用比代码块中反引号更多的连续反引号来实现
例如：引用 Markdown 代码区段：

	 ````
	 ```
	 print($abc, `abc`, ``ab``);

	 ```
	 ````

##Markdown 相关资源
- Markdown 作者之一[Aaron Swartz](http://coolshell.cn/articles/11928.html)

- Markdown 写作网站[简书](http://www.jianshu.com/)上图文并茂的[新手指引](http://www.jianshu.com/p/q81RER)和[入门指南](http://www.jianshu.com/p/1e402922ee32/)

- 另一个不错的 Markdown 写作网站[Markable](http://markable.in/),可以同步到EverNote
- 对于需要书写公式的科技工作者，可以参考这篇[Markdown写作浅谈](http://www.jianshu.com/p/PpDNMG)