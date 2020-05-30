---
title: Github pages+hexo构建自己的博客(ubuntu18.04)
date: 2019-04-17 21:58:46
tags: [Hexo, Github]
categories: Tutorial
toc: true
---
陆陆续续折腾了一个星期,终于成功搭建了一个属于自己的博客.碰到的坑真的不少,幸运的是这些问题都通过google解决了.
<!--more-->
# 1. 为什么用**github** **pages**和**hexo**来构建博客呢?

利用github和hexo来构建博客非常的简单和方便,非常适合展现静态内容,例如:xx框架的教程,技术博客,文学,影评,日记等等.然后,对一些不愿意付费搭建个人服务器的人群也同样有吸引力(因为搭建博客的过程中不花费一分钱).

# 2. 什么是**github pages**?

[github pages](https://pages.github.com/) 是github提供给用户用来展示个人或者项目主页的静态网页系统。每个用户都可以使用自己的github项目创建，上传静态页面的html文件，github会帮你自动更新你的页面。

# 3. 环境配置 

需要git, nodejs, hexo.
git的环境配置可以参考github[官网](https://help.github.com/en/articles/set-up-git#next-steps-authenticating-with-github-from-git).
node.js的环境配置可以参考[Node.js官网](https://nodejs.org/en/).
node.js安装完毕后 `使用 sudo npm install -g hexo-cli`  其中 -g 为全局安装.

# 4. 搭建博客

在github上创建一个repository, 名字必须为 `github用户名.github.io` .创建完成后在本地用 `git clone repositoryURL`
在本地的仓库里先创建一个源码分支(注意:这很重要如果你向在这个repository里面同时备份你的博客的源代码),由于github pages 的特性,HTML页面一定要在master分支下.执行`git branch blog_src`创建源码分支后,执行`git checkout blog_src`切换到blog_src分支下.
执行`hexo init 博客名` 来初始化生成博客项目的基本结构.
进入博客目录, 执行`hexo new test` 创建一个新的markdown文件,这个文件内容将是你未来的博客的内容,当然用markdown来书写(markdown是一门简单的排版的语言). `hexo generate` 将markdown文件转化成静态HTML网页,最后`hexo server`会在本地启动一个服务,然后默认可以通过浏览器访问http://localhost:4000/,来测试博客.修改 **_config.yml** 文件中 **deploy** 字段:
 ```yaml
 deploy:
   type: git
   repo: 博客repository的URL
   branch: master
 ```
 这里branch不能修改为其他自定义分支,必须为master.

# 5. 部署博客

在博客文件中执行`npm install hexo-deployer-git --save` 博客部署工具,这个工具可以直接帮助你把生成好的静态网页push到远程master分支上.执行`hexo deploy`完成博客部署.
访问`github用户名.github.io`确定博客是否能展示,这将是网络上博客的最终形式.

# 6. 备份代码

`git push origin blog_src` 将在远程创建blog_src分支.将来当你到一个陌生的环境下可以轻易的把blog_src pull 下来,通过hexo 来完成generate 和deploy.

# 7. 结语
最后推荐给大家一个我使用的hexo主题[maupassant-hexo](https://github.com/tufu9441/maupassant-hexo),简单但不简陋.
Have a good day![](end.jpeg)
