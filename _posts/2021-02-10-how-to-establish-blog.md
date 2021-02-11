---
layout: post
title: "将Blog放进冰箱拢共分几步？"
subtitle: "基于 jekyll + GitHub Pages的个人博客搭建"
date: 2021-02-10
author: Lu Nie 
category: Jekyll
tags: jekyll Blog
finished: true
---

本文旨在证明一个啥也不懂的人也能搭建个人博客。

> ### 前情提要
> ### 主要步骤
> ### 大概率会遇到的坑
> ### 参考资料



# 前情提要

**操作系统**：macOS Catalina 

**Ruby Version**: 3.0.0

**Jekyll Version**: 4.2.0


>为什么要用github pages 搭建个人博客？

因为免费，借用github的服务器可免费搭建个人博客。并且在不同电脑端更新博客也很方便，git clone 即可。

>为啥用Jekyll？

因为Jekyll有很多好看的主题，并且可以实现静态网页预览，这可以使用户更加专注在内容本身，而不是花枝招展复杂的代码。

# 关键步骤

- 准备前提环境
- 安装Jekyll
- 选择主题，搭建博客

## 1 环境配置

安装 Command Line Tools 

打开terminal，运行：

```
xcode-select --install
```

用Homebrew安装Ruby：Jekyll需要在Ruby环境下运行，因此首先安装Ruby.

安装 Homebrew 

如果用官网的方式，大概率是显示连接失败，无法安装（因为你懂的原因），需要更换国内的源。
[详情点击此处。](https://zhuanlan.zhihu.com/p/111014448)

terminal输入：
```
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

安装Ruby

```
brew install ruby 
```
将ruby路经添加到shell configutation
```
# If you're using Zsh
echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.zshrc

# If you're using Bash
echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile
```

另，如果有多个版本的Ruby需要安装，可以用rbenv来管理。

## 2 安装 jekyll 

```
# 安装bundler和 jekyll 

gem install --user-install bundler jekyll

# 将X.X 替换为当前使用的ruby版本（ruby -v 查看）

echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.zshrc 
```
至此，jekyll 安装完成！！

可输入 jekyll -v 确认。

接下来就是创建一个新blog, 可以自己直接新建，也可以用别人的主题模板。

---


## 3. 独立自主创建一个blog
```
jekyll new myblog 

cd myblog

# build网站，并在本地建一个服务器
bundle exec jekyll serve 
```
最后terminal会显示一个站点，可用浏览器打开。用于网站预览。

预览无误，推送（合并到“使用模板搭建”部分细讲）。

## 4. 使用模板搭建一个blog
1. 搭建：在github建一个自己用户名的仓库: username.github.io

2. clone： 
选中的jekyll theme clone到本地 (也可根据模板作者在 READ ME中提示的方式进行)；另再将自己的仓库clone到本地，作为本地仓库。

3. 推送：在本地根据自己需求修改好后，push到远端 username.github.io


### 4.1 搭建
在GitHub新建一个仓库。
### 4.2 clone
```
# git clone + 站点地址的形式
git clone https://github.com/username/username.github.io.git
```
修改模板文件夹的信息，基本修改 _config.yml 里的个人信息即可。

了解了整个文件夹内容后，可以修改任何信息。
### 4.3 push
push之前一定要做两步：

$ git add . 

$ git commit -m '被修改过的文件名称'
```
# 保存修改内容
git add .
git commit -m 'lunie2021.github.io'
# 确认远端仓库是否为自己的站点，还是模板所在站点
git remote -v
# 修改为自己站点
git remote set-url origin https://github.com/username/username.github.io.git
# push
git push -u origin master
```
# 安装过程遇到的各种坑
> 1. 如果直接用homebrew官网提供的语句在终端中运行，会出现connect failed 报错

原因：因为“你懂的”原因，官网的域名被“污染”。因此，需要用国内的镜像网站上的安装源。

解决：

国内镜像安装方式： https://zhuanlan.zhihu.com/p/111014448

简单来说，运行自动脚本，选择一个安装源即可，接着就自动安装。

安装脚本：/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"

卸载脚本：/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/HomebrewUninstall.sh)"

最后，如果显示 already up-to-date. 表示成功。

> 2. 安装过程报错：
Error: Fetching /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core failed! ==> Homebrew has enabled anonymous aggregate formula and cask analytics. Read the analytics documentation (and how to opt-out) here: https://docs.brew.sh/Analytics
No analytics have been recorded yet (nor will be during this `brew` run).

解决：参照官网提示 https://docs.brew.sh/Analytics，将Google analysis 功能解除，即可。

> 3. (sudo) gem Jekyll成功后，输入“Jekyll -v”检查，发现Jekyll未能成功安装。

原因：升级了macOS Catalina，新系统的shell已经更换为zsh。导致之前的安装都是在bash下进行的，zsh并没有完成。
发现这个是因为terminal中的提示：

The default interactive shell is now zsh. 
To update your account to use zsh, please run `chsh -s /bin/zsh`. 
For more details, please visit https://support.apple.com/kb/HT208050.

解决方法：
解决方法：

step 1
1. 不使用bash，切换zsh，chsh -s /bin/zsh命令切换即可。（我使用的1）
2. 继续使用bash。-输入vim ./.bash_profile 回车，然后就打开了bash_profile文件。-点击i建进入编辑状态，添加 export BASH_SILENCE_DEPRECATION_WARNING=1，这样一个环境变量就添加上了。-点击esc退出编辑状态，输入:wq回车保存退出。-输入source ～/.bash_profile ，让配置文件在修改后立即生效。

step 2: 当terminal进入zsh界面后，确认homebrew, ruby 是否安装，接着重新安装Jekyll 

> 4. Jekyll serve时，出现…./Users/apple/.local/share/gem/ruby/3.0.0/gems/jekyll-4.2.0/lib/jekyll/commands/serve/servlet.rb:3:in `require': cannot load such file -- webrick (LoadError)

原因：运行serve时，找不到webrick 文件。这是因为新版的 Ruby-3-0-0 不再包含webrick 文件。

解决方法：自己安装。
```
bundle add webrick
# 重新jekyll build 
jekyll build
```
[点击参考](https://github.com/jekyll/jekyll/issues/8523)

> 5. Not Found: /favicon.ico 

原因：文件中缺少网站标识图片，可以不管，也可以提供。
[点击参考](https://blog.csdn.net/weixin_43972292/article/details/90216241)


> 6. git push后，显示everything up-to-data, GitHub仓库并没有更新。

原因：没有使用GitHub的专用存储语句；

解决方法：
Jekyll预览无误后，输入：
```
 #将修改的内容放进storage
 git add .  

 # 提交至本地仓库
 git commit -m '上传项目' 

 #上传至远端仓库，出现master -> master 表示上传成功；
 git push origin master 
```
> 7. 网站点击文章内对应的标签，直接跳转至GitHub仓库的tags页面，而不是blog内的tag页面；

原因：layout中关于post的设置里，tag跳转给的链接如下：
“\<a class="post-tags-item" href="{{ site.url }}{{ site.baseurl }}/tags/">{{ tag }}</a>”；显然，"site.url.site.baseurl.tag"这个路径指向的就是github仓库的tags;

解决方法：
将路径改为博客内的tag位置；_congif.yml中url留白；

# 参考资料
【1】[jekyll官方网站](https://jekyllrb.com/) 

【2】[指路b站](https://www.bilibili.com/video/BV14x411t7ZU?from=search&seid=7751760845604383004)

【3】[指路b站](https://www.bilibili.com/video/BV1rC4y1878Y/?spm_id_from=333.788.recommend_more_video.0)

【4】[利用模板搭建jekyll](https://www.cnblogs.com/A--G/p/5112619.html)

【5】[还不错的主题推荐](https://www.zhihu.com/question/20223939)

