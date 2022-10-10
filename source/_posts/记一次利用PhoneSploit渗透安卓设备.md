---
title: 记一次利用PhoneSploit渗透安卓设备
date: 2022-05-21 13:06:04
tags: 渗透攻击
categories: 笔记
---

以下内容均为本人测试漏洞行为并无违法用途

也请读者不要用此技术进行违法犯罪行为

本人已将此漏洞进行提交

<!--more-->

需要用到的工具

1.浏览器

2.命令窗口

一.部署所需环境

这一步很简单 无脑复制粘贴回车即可

git clone  https://github.com/soryecker/phone_sploit_sor.git 

cd phone_sploit_sor

pip3 install colorma

windows系统执行后在文件管理中找到phone_sploit_sor文件夹![截屏2022-05-21 下午1.20.04](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-05-21%20%E4%B8%8B%E5%8D%881.20.04.png)

将adb.rar文件解压

linux系统貌似可以直接运行

mac系统需要配置adb 

命令brew install --cask android-platform-tools

配置好adb之后

执行python3 phonesploit.py 

到此即可把环境部署完毕

(注意以上代码需要以root用户执行 非root要加sudo 否则报错)

二.找寻目标

此漏洞利用的是远程adb开放的5555端口

我们可以去shodan或者钟馗之眼中搜索关键词“Android+Debug+Bridge“

即可看到很多开放5555端口的设备

[钟馗之眼](https://www.zoomeye.org/)

[shodan](https://www.shodan.io/)

都需要注册账号登录

![截屏2022-05-21 下午1.16.44](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-05-21%20%E4%B8%8B%E5%8D%881.16.44.png)

我们这里随便找到了一个小白鼠做实验

执行python3 phonesploit.py 后![截屏2022-05-21 下午1.31.16](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-05-21%20%E4%B8%8B%E5%8D%881.31.16.png)

输入小白鼠的ip回车（我这里是试了几个 都没法连接）

这种出现failed的都是无法连接的

这时候我们ctrl+d把脚本关掉

重新输入python3 phonesploit.py 然后找新的再次连接

![截屏2022-05-21 下午1.33.49](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-05-21%20%E4%B8%8B%E5%8D%881.33.49.png)

这种就是连接成功了

我们输入7然后回车

便可截屏他的屏幕并且保存

![截屏2022-05-21 下午1.35.28](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-05-21%20%E4%B8%8B%E5%8D%881.35.28.png)

这里给大家看一下保存的内容![screen](../imgs/$%7Bfiilename%7D/screen.png)

一般这种有公网ip的机器都不是个人手机 但是我们也不要用做违法用途

此漏洞我已经提交了 大家不要干坏事哦

