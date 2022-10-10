---
title: 记一次Hexo博客的搭建
typora-root-url: ../../source
top: 100
tags: 博客的搭建与功能完善
categories: 随笔
---
  心血来潮打算做个博客 服务器都买好了年费 结果突然看到利用github部署博客的教程（github不倒陪你到老）倒不是为了省钱，实在是购买的服务器不太安全。

<!--more-->

一、环境准备
1、安装Node.js

直接到官网上下载安装即可https://nodejs.org/en/download/

    Node.js (Node.js 版本需不低于 10.13，建议使用 Node.js 12.0 及以上版本)
    Node自带npm

2、安装Git

    Windows：下载并安装 git.
    Mac：使用 Homebrew, MacPorts 或者下载 安装程序。
    Linux (Ubuntu, Debian)：sudo apt-get install git-core
    Linux (Fedora, Red Hat, CentOS)：sudo yum install git-core
————————————————
环境是转载csdn上一位博主的 文章末尾会有原文链接

![343d28b9c9178b0b857abee140a668b1](/imgs/$%7Bfiilename%7D/343d28b9c9178b0b857abee140a668b1.png)

配置到上图所示即可

## 二、开始安装Hexo

### 1、安装hexo

```
npm install -g hexo-cli
或者
cnpm install -g hexo-cli
123
```

安装完成可输入hexo -v查看版本

### 2、初始化hexo，新建存储博客的文件夹

```
hexo init myblog
```

### 3、进入文件夹，安装一下npm

```
cd myblog
npm install
```

可以看到我们的hexo站点就已经安装好了，接下来就可以直接启动他了

### 4、启动服务站点

```
hexo g 
hexo server
```

访问http://localhost:4000/ 至此hero就搭建好了。可以在本地访问了

ps:初次启动速度较慢 请有足够的耐心

如果启动失败 这个问题我也没有遇到过 请问度娘

三、Gitee上建站访问（需要实名认证，如不想，请下滑看github配置教程）

可在github或者gitee上建站，gitee国内访问快一些
1、新建仓库

格式必须是：用户名+.gitee.io 只有这样，将来要部署到Gite e page的时候，才会被识别，也就是xxxx.gitee.io，其中xxx就是你注册Gitee的用户名。
————————————————

![3d5ab9f52a825335fea9df7e06acff9d](/imgs/$%7Bfiilename%7D/3d5ab9f52a825335fea9df7e06acff9d-3034162.png)

### 2、将hexo博客站点上传到gitee上

这里需要安装一个hexo的上传插件deploy-git

```
npm install hexo-deployer-git --save
```

### 3、修改hexo配置文件指定仓库路径

可在文件夹中直接打开文件，也可通过vim直接编辑

命令窗口输入vim _config.yml

命令窗口中输入i（需要切换输入法）

找到Deployment加上（注意空格）

```
deploy:
  type: git
  repo: 你的仓库路径
  branch: master
```

![6351f0a208292c8b4c0489963b0d7296](/imgs/$%7Bfiilename%7D/6351f0a208292c8b4c0489963b0d7296.png)

如图所示即可

4、推送hexo站点文件

之后就可以推送博客站点到gitee上了

推送命令
hexo d

    1
    2
    
    扩展：
    
    其中 hexo clean清除了你之前生成的东西，也可以不加。
    hexo generate 顾名思义，生成静态文章，可以用 hexo g缩写
    hexo deploy 部署文章，可以用hexo d缩写

推送中会要求输入gitee的用户名和密码（如果不想每次都输可以配置ssh，我这里就不做演示了）
————————————————

然后就可以看到gitee上有推上来的文件了

![90c3a63b27bb8ad3a9e6d097b759bf77](/imgs/$%7Bfiilename%7D/90c3a63b27bb8ad3a9e6d097b759bf77.png)

### 5、配置Pages服务

目前我们站点还无法访问需要开启Gitee Pages（gitee需要开启，github不需要）

![b9ae94584f281b39ca81f76dc030100b](/imgs/$%7Bfiilename%7D/b9ae94584f281b39ca81f76dc030100b.png)需要手持身份证等

几个小时后审核过了网站即可正常访问

gitee上传新文件之后，需要手动更新一下，更新后的页面才会生效

## 四、GitHub上建站访问

在gitee上建站发现有限制条件，所有也可以采用github建站的方式。

步骤和gitee一样。

不过推送文件前要在命令窗口输入

git config --global user.name "github注册用户名"

git config --global user.email "github注册邮箱"

注意填写 这里我有一个搞错的 查错查了一上午

ssh-keygen -t rsa -C "github注册邮箱"

这里一路回车 有y输y

之后会给到你生成目录

![9e5dde5c03e38f8a4cbecef0e0131bce](/imgs/$%7Bfiilename%7D/9e5dde5c03e38f8a4cbecef0e0131bce.jpg)

图片全是转载 实在不想再操作一次

```
id_rsa.pub把这个文件里的内容复制出来
```

而后在GitHub的setting中，找到SSH keys的设置选项，点击`New SSH key`
 把你的`id_rsa.pub`里面的信息复制进去。

![](/imgs/$%7Bfiilename%7D/3194ad0a9d04d94c09485122932968f3.jpg)

在gitbash中，查看是否成功

```
ssh -T git@github.com
```

### 5.推送站点到github

```
推送命令hexo d
```

如果想自己换域名请看下篇文章
