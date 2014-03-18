---
layout: post
title: "如何利用Octopress搭建一个Github博客"
date: 2014-03-18 14:37:07 +0800
comments: true
categories: 扯扯git
published: true

---
##引言
经过几天的时间，终于将一直想拥有的个人博客从空白搭建成现在的样子了。这期间，查了一些资料，也遇到了一些问题，总的来说，搭建还是挺方便的。下面，我将根据一下几个方面给大家讲述一下如何在苹果电脑上（OS X 10.9.2）利用octopress搭建一个github博客。<br />
<br />
1.准备工作<br />
2.安装Git<br />
3.安装Ruby<br />
4.安装Octopress<br />
5.配置Octopress<br />
##1.准备工作
1.先到github上注册帐号。注意：帐号名最后是会关联到博客的地址的。就比如我的github帐号是`odang`，我的博客地址是`odan.github.io`。  
2.帐号注册完之后，在自己的github主页上创建一个repositories(仓库)。在主页中点击如下图红色方框所示的选项。  

{% img ../images/2014-03-18 17.38.21.png %}
![仓库图片](../images/2014-03-18 17.38.21.png)  

跳转到另一页面之后，点击如下图红色方框所示的链接。  

![创建仓库](./2014-03-18 17.42.09.png)  
接下来我们就要为仓库命名了。注意这一步很容易出错。因为教程中跟我们讲的是仓库名要与自己的帐号名一致，一些人就仅仅填写了自己的帐号名而已，这样是不对的。正确的命名是：`你的帐号名.github.com`。就比如我的github帐号为`odang`，那么我起的仓库名称就应该是`odang.github.com`。  
仓库创建好之后，会得到一个ssh，就比如我的ssh为：`git@github.com:odang/odang.github.com.git`。我们可以将它copy下来，当然也可以不用这样做，因为在后面安装过程中终端会有提示。  
接下来，我们先离开github，在终端中做点其他的操作。
##2.安装Git
由于在之后的安装过程中需要使用到git，所以我们需要安装Git。我们可以在终端中输入`git --version`来查看git的版本，我电脑显示的内容为`git version 1.8.5.2 (Apple Git-48)`。如果在你的电脑上没有相关显示内容的话，请先安装[Git](http://git-scm.com)。
##3.安装Ruby
Octopress需要Ruby环境。RVM(Ruby Version Manager)负责安装和管理Ruby环境。我们可以利用RVM来轻松安装Ruby。<br />
我们先在终端中输入`ruby --version`，来确认电脑上是否安装了ruby。我的电脑显示的是`ruby 2.0.0p451 (2014-02-24 revision 45167) [x86_64-darwin13.0.0]`。如果提示ruby没有安装或者ruby的版本低于1.9.3的话，我们需要安装1.9.3或者更高的版本。<br />
我们在终端中输入以下命令：<br />
```
curl -L https://get.rvm.io | bash -s stable --ruby
```
安装好RVM后，我们在终端中输入一下命令：
```
rvm install 1.9.3
rvm use 1.9.3
rvm rubygems latest
```
之后，我们就可以在终端中输入`ruby --version`确认ruby1.9.3安装好了。<br />
参考：[Installing Ruby With RVM](http://octopress.org/docs/setup/rvm/)
##4.安装Octopress
在终端中输入如下命令:
```
git clone git://github.com/imathis/octopress.git octopress
cd octopress
```
接下来安装依赖项：
```
gem install bundler
rbenv rehash    # If you use rbenv, rehash to be able to run the bundle command
bundle install
```