---
layout: post
title: "如何利用Octopress搭建一个Github博客"
date: 2014-03-18 14:37:07 +0800
comments: true
categories: 扯扯git
published: true

---
<!--more-->
##引言
经过几天的时间，终于将一直想拥有的个人博客从空白搭建成现在的样子了。这期间，查了一些资料，也遇到了一些问题，总的来说，搭建还是挺方便的。下面，我将根据一下几个方面给大家讲述一下如何在苹果电脑上（OS X 10.9.2）利用octopress搭建一个github博客。  
1.准备工作  
2.安装Git  
3.安装Ruby  
4.安装Octopress  
5.将博客部署到Github上  
6.配置Octopress  
7.发表博文  
8.小结

##1.准备工作
1.先到github上注册帐号。注意：帐号名最后是会关联到博客的地址的。就比如我的github帐号是`odang`，我的博客地址是`odan.github.io`。  
2.帐号注册完之后，在自己的github主页上创建一个repositories(仓库)。在主页中点击如下图红色方框所示的选项。

![](/images/2014/03/1.png) 

跳转到另一页面之后，点击如下图红色方框所示的链接。  

![](/images/2014/03/2.png) 

接下来我们就要为仓库命名了。注意这一步很容易出错。因为教程中跟我们讲的是仓库名要与自己的帐号名一致，一些人就仅仅填写了自己的帐号名而已，这样是不对的。正确的命名是：`你的帐号名.github.com`。就比如我的github帐号为`odang`，那么我起的仓库名称就应该是`odang.github.com`。  
仓库创建好之后，会得到一个ssh，就比如我的ssh为：`git@github.com:odang/odang.github.com.git`。我们可以将它copy下来，当然也可以不用这样做，因为在后面安装过程中终端会有提示。  
接下来，我们先离开github，在终端中做点其他的操作。
##2.安装Git
由于在之后的安装过程中需要使用到git，所以我们需要安装Git。我们可以在终端中输入`git --version`来查看git的版本，我电脑显示的内容为`git version 1.8.5.2 (Apple Git-48)`。如果在你的电脑上没有相关显示内容的话，请先安装[Git](http://git-scm.com)。
##3.安装Ruby
Octopress需要Ruby环境。RVM(Ruby Version Manager)负责安装和管理Ruby环境。我们可以利用RVM来轻松安装Ruby。  
我们先在终端中输入`ruby --version`，来确认电脑上是否安装了ruby。我的电脑显示的是`ruby 2.0.0p451 (2014-02-24 revision 45167) [x86_64-darwin13.0.0]`。如果提示ruby没有安装或者ruby的版本低于1.9.3的话，我们需要安装1.9.3或者更高的版本。  
我们在终端中输入以下命令：  
```
curl -L https://get.rvm.io | bash -s stable --ruby
```
安装好RVM后，我们在终端中输入一下命令：
```
rvm install 1.9.3
rvm use 1.9.3
rvm rubygems latest
```
之后，我们就可以在终端中输入`ruby --version`确认ruby1.9.3安装好了。  
参考：[Installing Ruby With RVM](http://octopress.org/docs/setup/rvm/)
##4.安装Octopress
在终端中输入如下命令:
```
git clone git://github.com/imathis/octopress.git octopress
cd octopress
```
接下来安装依赖项:
```
gem install bundler
rbenv rehash    # If you use rbenv, rehash to be able to run the bundle command
bundle install
```
最后，安装octopress默认的主题：
```
rake install
```
参考：[Octopress Setup](http://octopress.org/docs/setup/)  
##5.将博客部署到Github上
一、我们先让Github与我们的电脑产生联系。  
新建一个终端窗口，输入如下命令：  
```
cd ~/.ssh    #到ssh的目录
ls -a        #查看文件夹内的内容
```  
这时候的文件夹中是没有id_rsa和id_rsa.pub这两个文件的。
接着，我们输入如下命令：
```
ssh-keygen -t rsa -C "你的邮箱地址"    #创建密钥的命令，输入你们的邮箱地址
```  
接下来会有存放路径的提示，回车即可，然后会提示输入密码和确认密码，按照提示输入就OK。
二、绑定Github  
输入完毕后，打开id_rsa.pub，copy里面的所有内容。然后，打开[https://github.com/settings/ssh](https://github.com/settings/ssh)，add ssh key，title随便写，再把刚才复制的内容粘贴到key中，add之后就OK了。  
三、链接Github  
这时候新建的终端窗口可以关闭了，我们重新回到octopress窗口，输入如下命令：  
```
rake setup_github_pages
```  
上面的命令会执行一些操作，这期间会要求我们输入URL，这就是之前我说的SSH地址，我们可以根据提示输入，也可以将之前复制的地址粘贴上去。回车之后，我们继续输入命令：
```
rake generate
rake deploy
```  
执行上面的命令后，将生成博客文件，并将博客文件复制到_deploy/下，然后将这些添加到git中，并commit和push到master分支上。稍等一段时间，我们就可以访问自己的博客了。  
不过别忘了提交博客的source，输入命令：
```
git add .
git commit -m 'your message'
git push origin source
```
这样就可以将博客的source提交到仓库的source中了。  
参考：[Deploying to Github Pages](http://octopress.org/docs/deploying/github/)  
当浏览自己博客的时候，会发现有些设置是我们不想要的，接下来我们就来配置一下octopress。
##6.配置Octopress
一般情况下，我们只需要修改`_config.yml`文件来修改配置信息，我们可以在octopress文件夹下找到该文件。  
`_config.yml`文件中的url是必须要填写的，这个url就是我们博客的地址。我们还可以修改一下`title`、`subtitle`和`author`等等。  
简单地修改了配置信息之后，我们执行命令：
```
rake generate
rake deploy
```
就可以将博客部署到仓库中了。然后我们浏览博客就可以看到与之前的不同了。  
更多关于`_config.yml`的内容，请看：[Configuring Octopress](http://octopress.org/docs/configuring/)  

建议：最好把里面的twitter相关的信息全部删掉，否则由于GFW的原因，将会造成页面load很慢。同理，修改定制文件/source/_includes/custom/head.html 把google的自定义字体去掉。参考：[唐巧的博文-配置](http://blog.devtang.com/blog/2012/02/10/setup-blog-based-on-github/)  
##7.发表博文
捣腾了那么久，终于到了激动人心的时刻了，发表一篇博文庆祝一下吧。  
根据[Blogging Basics](http://octopress.org/docs/blogging/)，我们知道博文必须放在`source/_posts`下，并且以`YYYY-MM-DD-post-title.markdown`进行了命名。  
我们在终端中输入如下命令来创建一篇新的博文：
```
rake new_post["title"]
```
其中，title是博文的文件名。上面的命令会创建出一个文件:`source/_posts/2011-07-03-title.markdown`，文件默认格式是markdown。根据路径，打开文件就可以看到如下的一些内容：
```
---
layout: post
title: "title"
date: 2011-07-03 5:59
comments: true
categories: 
---
```
接下来，我们就可以在这个文件中写我们的博文了。完成之后，我们需要部署博文。下面是创建并部署博文的一个完整过程：  
```
rake new_post["New Post"]
rake generate
git add .
git commit -am "Some comment here." 
git push origin source
rake deploy
```
##8.小结
本文介绍了如何利用Octopress搭建一个Github博客，大家如果在搭建过程中遇到问题，可以在下方给我留言。  
本人刚开始学习git和markdown，如果文中有错误的地方，欢迎指正。  
关于博客的一些配置，我会在另一篇博文中介绍，欢迎学习。  
  
本文参考了以下文章:  
[利用Octopress搭建一个Github博客](http://beyondvincent.com/blog/2013/08/03/108-creating-a-github-blog-using-octopress/)  
[OS X搭建OCTOPRESS](http://easy1z.github.io/blog/2013/07/10/os-xda-jian-octopress/)  
