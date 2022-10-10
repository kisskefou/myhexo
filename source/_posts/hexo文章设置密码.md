---
title: hexo文章设置密码
date: 2022-09-21 15:56:04
tags: 博客的搭建与功能完善
categories: 随笔
---

1、安装插件

<!--more-->

首先运行以下命令，安装设置密码所需要的插件：

npm install hexo-blog-encrypt

2、修改配置

在根目录的配置文件_config.yml中添加以下代码：

    encrypt:
      enable: true

3、博客文章添加加密字段

设置加密之后，不要忘记在新建博文的时候，在头部添加加密的设置信息，如下图：

password: 密码
message: 输入密码界面提示说明
4、效果展示

接着运行你的博客，访问相应的加密文章之后，会提示输入密码才能查看文章：
