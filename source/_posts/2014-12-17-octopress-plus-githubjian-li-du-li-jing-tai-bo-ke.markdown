---
layout: post
title: "Octopress+GitHub建立独立静态博客"
date: 2014-12-17 20:11:41 +0800
comments: true
categories: 技术探索
---
##1.为什么选择Octopress和GitHub Pages?
在在做任何事情之前最好先问个为什么，尽管很多情况下未必有答案，但这个做法绝对有好处。用 Octopress 搭建博客，并托管到 Github Pages，撇除一些个人因素之外，我想还有以下几点原因：

1.  免费且独立。把 Octopress 博客系统搭建到 Github Pages 虽是免费，但不失独立性，即便 Github 全站关闭，你也将有一份本地全站备份，随时可以重新恢复。不必受托管商之气，而且还免费，如果你愿意，甚至可以自行插入广告挣钱。

2. 版本控制。写文章，建网站，做软件都需要修改，但有时候改完了又会后悔，如果有时光机就好了，Git 就是你的时光机。当然如果你不想了解这些看上去很唬人的 IT 名词，只是想写博客的话，请在需要的时候再研究这条的内容。

3. 相对其他托管到 Github 上的博客程序，Octopress 更加成熟易上手。打个比方，Jekyll 可以说是毛坯房，Hexo 和 Octopress 算是简装修，但相比 Hexo，Octopress 有更多装修范例和更多熟练的装修工人，更容易获取帮助。当然如果你只想住精装修的房子，那不得不花点钱上 WordPress 了。

4. 使用 Markdown。Markdown 是现在最为流行的轻量级标记语言，也是已故的天才 Aaron Swartz 留给世人最好的礼物，窃以为每个在互联网上发布文章的人都该掌握。

5. 按照官方的说法，Octopress 是个「为黑客设计的博客框架」，这很酷，你不觉得吗？

如果你之前没有写过博客，打算开始搭建自己第一个博客的话，其实也不妨试试 Octopress，免费还能学到东西，何乐而不为？


##2.准备工作
既然是为黑客设计的博客框架，安装起来肯定没有像普通应用程序那么简单，需要一些准备工作，但请相信我，并不复杂。

###2.1 安装git

既然要使用 Github，那么肯定首先要安装 Git，这个很简单：

1. [点击这里](http://git-scm.com/)到 Git 官方网站。
2.  找到对应你的系统的版本下载链接，按照提示下载并安装。

###2.2 安装Ruby

安装 Ruby 稍稍有些复杂，不过你只要按照以下步骤一步一步来就好了：

1. 安装HomeBrew

 	[HomeBrew](http://brew.sh/index_zh-cn.html) 是一个非常有用的软件包管理系统，你可以把它想象成一个稍微抽象一点的 Mac App Store. 正如我们用 Mac App Store 来安装其他软件一样，我们这一步安装 HomeBrew 的目的是为了安装别的软件 (Ruby) 。当然 Mac App Store 和 HomeBrew 本身也是软件。
 	安装 HomeBrew 非常简单，打开终端 (Terminal)，执行以下命令（所谓「执行」即「输入+回车」，下同）：
 		
	ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)	

如果在执行上如命令的时候弹出需要安装 Xcode Command Line Tool 的提示，直接点击安装即可。

**注意：安装后可能还不能装好，你可以输入以下命令行检查是否装好，若重新提醒你安装，则说明未安装好，那么你最好就直接Google一个这个工具，单独下载dmg文件，并安装。**

	xcode-select --install
	
 成功则显示：
 				
	xcode-select: error: command line tools are already installed, use "Software Update" to install updates
 	
 	
安装好Xcode Command Line Tool 后最好先执行以下命令：

	brew doctor

此条命令用来诊断安装中出现的问题并提示修复方法，如果没有问题则会显示：

	Your system is ready to brew.

如遇问题，则按照提示处理，如果不懂如何处理可以先试着执行后面的步骤，如果能成功，则没有太大问题，毕竟我们只是想写博客而已。当然，做任何事情之前，备份是必须的。

2. 使用 RVM 安装 Ruby

执行以下命令安装 RVM，最新的稳定版 Ruby 也会随之安装：

	curl -L https://get.rvm.io | bash -s stable --ruby
	
为避免出现问题，可执行以下命令安装 Ruby 2.0.0:

	rvm install 2.0.0
	rvm use 2.0.0
	rvm rubygems latest

可以执行ruby --version命令来查看现在使用的 Ruby 版本，确保正在使用的是 Ruby 2.0.0

###2.3 注册Github账号

这个没什么好说的，早晚需要，去 http://github.com 注册吧。

###2.4 域名指向（可选）

如果你有自己的域名可用，可以在这时就配置好，毕竟解析起来需要一段时间，不如在我们搭建博客的时候让它开始，这样我们搭建完成后，基本上就可以直接用自有域名访问了。

如果你用的是顶级域名，比如 yangyang.com, 请创建两个 A 记录 (A Record) 分别指向 192.30.252.153 和 192.30.252.154.

如果你使用二级域名，比如 blog.shengmingzhiqing.com, 请将该域名的 CNAME 指向 [your_username].github.io, 把其中的 [your_username]换成你自己在 Github 上的用户名。

如果你暂时没有域名，这一步可以暂时不用管。

##3.本地安装 Octopress

终于进入正题了。有了前面的准备工作，安装 Octopress 显得非常简单：

首先，打开终端 (Terminal) 执行如下命令：

	git clone git://github.com/imathis/octopress.git octopress
	cd octopress

上面的代码中，第一行的作用是把 Octopress 克隆到本地磁盘，将会在你的本地~/user/yourusername 这个文件夹下生成一个名为 octopress 的文件夹。如果你不知道 yourusername 是什么，其实就是你每次打开终端时，$ 这个符号前面显示的那玩意。

第二行的作用是进入这个新建的 octopress 文件夹。这一步可能会碰到一个「是否要信任 .rvmrc file」的问题，输入 yes.

然后我们开始安装 Octopress 所必需的依赖项(dependencies)，执行以下命令：

	gem install bundler
		
在下一步之前

1）修改gemfile

由于大陆的“特殊情况”，rails默认生成的Gemfile的源 https://rubygems.org 很慢甚至被重置，所以适应国情，要修改下Rails默认生成的Gemfile文件。

修改octopress文件夹里的Gemfile文件，替换 https://rubygems.org 为 http://ruby.taobao.org 

执行：

	gem install jekyll --version “2.0.0"
		
完毕后		
		
	bundle install
		
然后执行如下命令安装默认主题：

	rake install

本地安装完毕。顺便说一句，所谓 rake 就是 ruby make 的缩写。

这时你执行如下命令：

	rake preview

然后在浏览器内输入 http://localhost:4000/，即可看到我们搭建完成的博客。也许并不好看，但很令人开心，不是么？

**注意：以上各步中如果出现权限问题（关键词 permission），无法完成（关键词 abort）的话，请在各命令前加上 sudo+空格，如有提示，请输入电脑登录密码。**	

##4.将 Octopress 部署到 Github Pages

###4.1 新建库 (Repository)

用刚刚注册的 Github 账号登录，然后在点击页面右上角的加号，在弹出菜单中点击 New Repository: 如图所示
![权限选择](Repository.png)

然后会跳转到一个新建库 (Create new repository) 的页面，在Repository name一栏填 [your_username].github.io，[your_username] 是你 Github 上的用户名，请务必按照此格式填写，否则无法在 Github 上部署博客。然后点击 Create repository 按钮提交。

如果一切顺利会出现一个页面，有一个 SSH 地址，形如 git@github.com:[your_username]/[your_username].github.io.git，下一步会用到。

###4.2 将本地部署的 Octopress 发布到 Github Pages

打开终端 (Terminal)，执行以下命令：

	cd octopress
	rake setup_github_pages
	
然后会出现一个问句，请把 4.1 步生成的 SSH 地址粘贴到这里，然后回车继续。

执行以下命令：

	rake generate
	rake deploy
		
第一行命令用来生成页面，第二行命令用来部署页面，可按照字面意思理解。如果理解不了，可以暂且不管。任何一步如果出现失败提示，请使用 sudo。

如果上述内容完成，即可使用 http://[your_username].github.io/ 访问页面，将会出现一个和在本地预览时相同的页面。

然后，不要忘了把源文件全部发布到 source 分支下面，再一次可以看不懂，执行以下命令：

	git add .
	git commit -m "备注内容"
	git push origin source
		
###4.3 使用自己的域名（可选）

如果你有自己的域名，并且想指向这个新博客的话，请首先确保执行了 2.4 节中的内容。如果没有执行，可以随时执行。

然后执行下面的命令，注意把 your-domain.com 换成你自己的域名。

	echo 'your-domain.com' >> source/CNAME
		
然后再次执行以下命令：	

	rake generate
	rake deploy	
	
这样你就可以使用自己的域名了。域名解析需要一段时间，如果没有马上生效，请不要着急。如果长时间没有生效，请确保完整执行了 2.4 节和本节内容。


##5.发布新贴	

博客搭建好了，我们可以开始我们的第一贴了。那么怎么发布新贴呢？如果你真的想像个黑客一样写博客，我们可以继续使用我们的终端 (Terminal) 和命令行，执行以下命令：

	cd octopress
	rake new_post["Post Title"]
		
把其中的 Post Title 替换为你想写的文章标题。然后会有一个名为 yyyy-mm-dd-Post-Title.markdown 的文件在 octopress/source/_posts 目录下生成，其中 yyyy-mm-dd 是你当时的日期。然后执行以下命令：

	cd source/_posts/
	vim yyyy-mm-dd-Post-Title.markdown
		
即可用 vim 编辑器编辑的刚才的文章了，好吧我知道你作为这篇文章的读者并不是一个能熟练使用 vim 的人，那么请在命令行输入 :q退出这个编辑器。如果你不想假装是个黑客的话，其实发布文章并不需要这么麻烦。


我们直接打开 octopress/source/_posts 文件夹，找到刚才生成的文件，用你喜欢的 Markdown 编辑器（免费的我推荐 Mou，收费的我推荐 Byword）或者文本编辑器打开，对文章内容进行编辑。

打开文件后，你会发现文章开头有这么一段信息:

	---  
	layout: post  
	title: "Post Title"  
	date: yyyy-mm-dd hh:mm:ss  
	comments: true  
	categories: ""  
	---
	
这其实是这篇文章的元数据：layout 暂时不要理会；title 是这篇文章显示在最终网页上的标题；date 部分是详细的文件生成时间，如 2014-04-28 03:35:00；comment 部分表示是否允许评论，目前显示是允许，如果想关闭评论，请改为 false；categories 指这篇文章的分类目录，请在后面引号中输入，如果没有该目录，则会自动生成。请不要删除这段信息，在这段信息下面开始你的文章内容。

这件事情给我们的启发是，以后发布文章，其实并不需要使用终端命令行生成文件。可以直接将自己写好的文章放到这个文件夹下面，当然请按照 yyyy-mm-dd-Post-Title.markdown 这样的文件格式命名，同时记得在文章前面添加元数据信息。这种做法生成的文章与上面的方法无异。如果你觉得添加元数据信息过于麻烦，推荐一个非常好用的工具：[TextExpander](https://smilesoftware.com/TextExpander/index.html)。

在文章写好之后，使用命令行执行（仔细观察命令，像不像 generate 和 deploy 的合体？）：

	rake gen_deploy

同样，如果在本节中，任何命令执行失败，没有取得想要结果，请在前面加 sudo。是时候说一说 sudo 命令了，这其实是 super do 的缩写，之所以用它是因为，一般而言 Mac 上最高权限的root 账户默认是关闭的。我们自己的账户哪怕是管理员也在一些地方没有权限操作，super do 其实就是越权操作的意思，因此也往往需要输入密码，一般而言短时间内不需要输入第二次。

**出现问题：**

rake gen_deploy 后出现：

	Errno::ENOENT: No such file or directory @ rb_sysopen - public/_posts/.yyyy-mm-dd-Post-

**解决方案：**

修改octopress文件夹下的Rakefile

	desc "copy dot files for deployment"
	task :copydot, :source, :dest do |t, args|
	FileList["#{args.source}/**/.*"].exclude("**/.", "**/..", "**/.DS_Store", "**/._*", "**/.*.sw*”).each do |file|
    cp_r file, file.gsub(/#{args.source}/, "#{args.dest}") unless File.directory?(file)
	  end
	end

**deploy成功，出现新问题：**

	 ! [rejected]        master -> master (non-fast-forward)

	error: failed to push some refs to 'https://github.com/yangyangonline/yangyangonline.github.io.git'

	hint: Updates were rejected because the tip of your current branch is behind

	hint: its remote counterpart. Integrate the remote changes (e.g.

	hint: 'git pull ...') before pushing again.

	hint: See the 'Note about fast-forwards' in 'git push --help' for details.

**解决方法：**

先git pull 再git push可以传上去默认主题的博客页面。(博文奇怪丢失)

**出现问题：**

博文丢失

**解决方法**


git config --global push.default matching
git config --global push.default simple

出现新问题
fatal: The upstream branch of your current branch does not match
the name of your current branch.  To push to the upstream branch
on the remote, use

    git push origin HEAD:master

To push to the branch of the same name on the remote, use

    git push origin source

#####最终解决方案：

修改Rakefile

Bundler.with_clean_env { system "git pull" }

改为
Bundler.with_clean_env { system "git pull origin #{deploy_branch}” }

Bundler.with_clean_env { system "git push" }

改为
Bundler.with_clean_env { system "git push origin #{deploy_branch}” }


这样你的第一篇日志就发布出来了，恭喜你正式开通了基于 Octopress 的独立博客。

上传文章，更新云端操作为：

	git pull origin source
	git push origin source
	rake deploy
	rake deploy

每次完成更新都记得把原始文件重新放到 Github 上，还记得命令吧：

	git add .
	git commit -m "备注内容"
	git push origin source



