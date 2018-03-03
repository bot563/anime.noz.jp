---
layout: post
title: "使用github + jekyll搭建个人博客"
date: 2018-01-29
description: "使用github + jekyll搭建个人博客"
tag: 博客 
---   

***

**通过本地写markdown，之后push到github即可**

## 创建github账号和项目

注册github账号还是蛮简单的，只要填写一些相关的信息即可，这里就不具体演示了。创建好之后，我们就要创建项目了，可以参考下面的图片：

* 点击“New repository”:
![创建项目第一步](/images/posts/jekyll/create-1.png "第一步")

* 填写项目信息：
![创建项目第二步](/images/posts/jekyll/create-2.png "第二步")

* 项目最终效果：
![创建项目结果示意图](/images/posts/jekyll/create-3.png "项目创建好的样子")

## 本地安装jekyll(以windows为例) 

首先呈上安装jekyll的几个重要步骤，让大伙心理有个底~

* 安装Ruby
* 安装DevKit
* 安装Jekyll
* 安装Pygments
   * 安装Python
   * 安装 ‘Easy Install’
   * 安装Pygments
* 启动jekyll


接下来就上图演示各个过程：

**注意：**
>1. Ruby与 DevKit 版本要对应；
>2. 安装 DevKit 时最好在安装目录新建一个文件夹 devit 。


### 第一步：安装 Ruby

**下载：**  <http://rubyinstaller.org/downloads/>

**根据电脑的系统选择合适的 Ruby 版本**  

![官网下载Ruby](/images/posts/jekyll/rubyInstall-1.png "下载对应的ruby版本")

**注意：勾选 “Add Ruby executables to your PATH”，安装路径不能包含空格**

接下来去命令行窗口输入命令：`ruby -v` 来测试是否安装成功

![测试Ruby的安装](/images/posts/jekyll/rubyInstall-2.png "检测ruby是否安装成功")


### 第二步：安装 DevKit

**下载：**  <http://rubyinstaller.org/downloads/>  

上面的链接是到 Ruby 的官网，我们直接拉到最下面就会发现我们需要的 DevKit。依旧根据电脑的系统选择合适的 DevKit 版本  

![下载DevKit](/images/posts/jekyll/rubyInstall-3.png "下载对应的DevKit版本")

**安装 DevKit 时最好在安装目录新建一个文件夹 devit 然后运行安装程序选定该文件夹在对应安装目录打开命令行窗口，并执行一下命令：**

	ruby dk.rb init
	ruby dk.rb install

**注意：Ruby 与 DevKit 版本要对应**


### 第三步：安装 Jekyll

这一步主要是通过在命令行窗口输入命令完成

	//更换gem源
	gem sources --remove https://rubygems.org/
	gem sources -a https://gems.ruby-china.org/
	
	//查看gem源
	gem sources -l
	
	//更新gem
	gem update --system
	
	//安装jekyll
	gem install jekyll
	

### 第四步：安装 Pygments

#### a. 安装 Python

**官网链接：** <http://www.python.org/download/>


**下载 Python 2安装，如果安装 Python 3 可能不会正常工作。安装后添加环境变量。**

执行命令`python -V`，测试 python 是否安装成功（**注意是大写的V**）

#### b. 安装 Easy Install


*提示：需要下载[ez_setup.py](https://pan.baidu.com/s/1jG2bYbs)*

在命令行窗口输入 cmd 命令 
	
	python "C:\ez_setup.py"(这里要改为你自己的目录）

进行上面一步之后，`C:\python27\Scripts` 文件中就会有 `easy_install` 的相关文件。

**重点是我们需要将 C:\python27\Scripts 和 C:\python27 添加到系统路径**

关于添加环境变量：

> 右键: 我的电脑 --> 属性 --> 高级系统设置 --> 环境变量

然后通过命令 

    easy_install --version
    
来查看 `Easy Install` 是否安装成功


**如果你是输入 `easy_install --version` 看到提示非内部命令之后才去配置的环境变量，那么你要重新打开控制窗口再进行 `easy_install --version` 才有效**

#### c. 安装 Pygments

执行命令:  
	
	easy_install Pygments
	

### 启动 jekyll

打开命令行窗口，执行如下命令：

	//创建jekyll工程目录
	jekyll new myBlog

	//切换到工程目录，并开启服务
	cd myblog
	jekyll serve

在本地的 `4000端口` 能看到页面，页面如下：
![博客运行界面](/images/posts/jekyll/result.png "博客启动之后的界面")

我们可以把 `_config.yml` 中的一些字段改成你的个人信息(如名字、邮箱、网站描述之类的)。

当然，你也可以打开 `about.md` 和 `index.html` 里面的内容进行修改，但是要注意：  

**代码中\`\`和\{\% ... \%\}内容不能修改，这都是变量，不是普通文字。每个页面类似如下代码，即“---”开始和结束的中间部分，只能修改，不能删除!**

	---
	layout: page
	title: About
	permalink: /about/
	---
	
把要改的改完之后，重新运行 `jekyll serve`，刷新页面，即可看到效果。


## 将项目提交到github上

**有些博客提及在提交之前要创建 `.gitignore` 文件 ，最新的 jekyll 自带该文件，且已经把要忽略的非版本控制的文件已经写入了**
>1. git init

>2. git add .

>3. git commit --message "init blog"

>4. git remote add origin git@github.com:AIWWJ/AIWWJ.github.io.git(**将AIWWJ替换为你的github名**)

>5. git push origin master  


因为我后面的时候在 github 上删除了该项目又重建，导致第5步 `git push` 的时候报错
![git push报错](/images/posts/jekyll/git-1.png "git push出错")

经过看 [rejected] 后面的内容，发现是因为远程仓库中有一些文件在本地仓库中不存在，通过百度得到解决方法：  

先将远程仓库 pull 一份到本地：

	git pull origin master

然后再运行：

	git push -u origin master

但在运行 `git pull origin master` 时报了个错
![git push报错](/images/posts/jekyll/git-2.png "git push出错")

把错误中的 `“refusing to merge unrelated histories”` 拿去百度了下发现了问题所在：

    git pull origin master --allow-unrelated-histories(合并两个不同的项目)  


当因为你的远程仓库的分支比本地的代码要新导致冲突时，要么把冲突解决掉再提交要么开新分支提交要么就直接 `git push --force`（多人协作请慎重） 。


对应的方法如下，大家根据需要进行选择：

1、 使用 `强制push` 的方法：

	git push -u origin master -f 
	
这样会使远程修改丢失，一般是不可取的，特别是在多人协作开发的时候。

2、 push前先将远程repository修改pull下来

	git pull origin master
    git push -u origin master

3、若不想merge远程和本地修改，可以先创建新的分支

	git branch [name]
	git push -u origin [name]
	
此时通过浏览器访问 `“你的github用户名.github.io”` 即可看到我们上一步中利用 jekyll 搭建起来的博客

## 关于写文章

有两点需要注意的：

**文章必须新建在 `./_posts` 文件夹中**

**文章名称必须是 `yyyy-mm-dd-xxxxx-xxx-xxx` 格式，后缀名可以是 `.markdown | .html | .textile `
一开始要这样写，下面的内容中，`layout: post` 不能修改，其他的可自行修改。**
	                  																							
		
	---
	layout: post
	title:  "使用 github + jekyll 搭建个人博客"
	date:   2016-07-24 21:41:45 +0800
	tag: share
	---	

写完这几行之后，剩下的就可以自己用 `markdown` 来写了
通过运行 `jekyll serve`，可在任何时候通过浏览器及时查看效果。当你觉得文章效果 OK 的话，就可以 `push` 到 github 上。