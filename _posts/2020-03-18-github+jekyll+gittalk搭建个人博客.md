---
layout: post
title: github+jekyll+gittalk搭建个人博客
categories: Github
tags: github
description: 详细的个人博客搭建教程。
keywords: github, 教程
---

个人博客搭建教程。

废话不多说，直接进教程。

### 新建博客仓库

点击 New Repository，仓库名格式为你的用户名.github.io，description 看个人喜好。

### 下载或者 fork Jekyll 模板

1. fork：找到你喜欢的 jekyll 模板 github 源码地址，然后 fork 即可，[jekyll 官网](http://jekyllthemes.org)。
2. 下载：找到源码地址后，本地新建空白目录，如 blog，打开 blog 目录，在当前路径打开终端，使用 git clone + 地址 命令拉取你新建的仓库和模板到 blog 下(没有 git 的童鞋自行安装并配置本地 email 和 username 信息)，然后拷贝模板仓库下所有文件(.git 除外，注意这是隐藏文件)到你的仓库目录下，终端切换目录到你的仓库目录，输入 git status 命令可以查看所有修改，git add .添加所有 ，然后 git commit -m "init"提交，最后输入 git push origin master 推送到你的 github 仓库。到这里步骤就已经完成了一半。

### 配置 jekyll

1. 如果你需要绑定自己的域名，那么修改 CNAME 文件的内容；如果不需要绑定自己的域名，那么删掉 CNAME 文件。
2. 在 \_config.yml 文件中，将其中与个人信息相关的部分替换成你自己的，比如网站的 url、title、subtitle 和第三方评论模块的配置等。
3. 修改 About 页面为你的个人相关信息，删除掉\_post 下的所有文章数据，图片资源酌情删除。

### 配置 gittalk

1. 新建一个评论仓库，取名随意如(blog-comments)，在该仓库 Settings 中启用 issue。
2. 申请 github Apps，取名随意，源地址写你的 xxx.github.io，重定向地址如果有域名可以配置为域名，无则写 xxx.github.io。
3. 在\_config.yml 中配置 gittalk<br>gitalk:<br>owner: qinggee<br>repo: blog-comments<br>clientID: 11a6f252f6224761<br>clientSecret: 3d1722301d3ecfc3828d137c9ea50c00a7<br>
