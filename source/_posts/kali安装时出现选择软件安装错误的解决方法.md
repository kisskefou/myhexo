---
title: kali安装时出现选择软件安装错误的解决方法
date: 2022-06-07 13:36:50
tags: 渗透攻击
categories: 笔记
---

安装kali2020.2版本，需要从国外源下载安装包，由于网络原因安装失败

此时可以选择换源安装，重新走一遍之前的安装流程，到下图这一步时，**正在配置apt，**

<!--more-->

建议选择一个稳定的网络下进行换源安装

使用快捷键【Ctrl+Alt+F2】切换到tty2终端，进入之后敲回车键进入新终端，

在终端中输入如下命令,切换到chroot，修改镜像源文件，重新配置镜像源：

【chroot /target】

【nano /etc/apt/sources.list】  

将默认的两个**deb**用**#**注释掉(下图2)，

再添加新的源，本次使用的是阿里云的镜像源，命令如下(下图3)：

【deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib】

输入完成之后按【Ctrl+O】保存，会弹出文件名已经写入。敲回车，再【Ctrl+X】退出。

![img](../imgs/$%7Bfiilename%7D/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2MjkzNTM0,size_16,color_FFFFFF,t_70-4580345.png)

再使用如下命名更新镜像源和系统：

【apt update && apt ungrade】

此时已经换源成功，正在更新，等更新完成，按【Ctrl+Alt+F5】切换到图形终端

![img](../imgs/$%7Bfiilename%7D/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2MjkzNTM0,size_16,color_FFFFFF,t_70-20220607133923808-4580365.png)

在这一步中一定要勾选最下面一个扩展工具，否则进入系统之后只有基本的命令，点击继续，正在下载安装文件，等待文件安装完成即可

安装完成，进入系统，本次安装大概花了接近两个小时

kali2020默认root没有密码，使用创建的账户进入系统之后，使用【su -】命令切换到root，再使用【sudo passwd root】命令创建密码。

建议使用阿里云等商业公司的镜像源，部分大学的镜像源文件比较旧，不能一次性成功，还是会安装失败，必须得多次安装才行。

附其他版本kali镜像下载链接：http://old.kali.org/kali-images/
