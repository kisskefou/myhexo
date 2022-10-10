---
title: kali安装nessus
date: 2022-06-09 18:55:27
tags: 渗透攻击
categories: 笔记
---

Nessus_pro 10.X 通用安装pj教程+专业版插件包升级

<!--more-->

由于在多个交流群中数次看到有小伙伴安装pj后，不是pj失败，就是重启后插件消失，其中原因众多。本文就记录了自己近一年多的安装pj心得，Windows、Linux安装pj使用N次（mac由于个人未有设备，所以没尝试过，不过步骤都是一样的），都是完美使用没有暗病。
环境准备

装机环境：kali虚拟机（建议啊，漏扫还是安装在Linux虚拟机上比较合适），首选kali准没错，省心

Nessus安装包：直接官网: https://www.tenable.com/downloads/nessus 下载就行，kali安装选择deb后缀的文件，64还是32看你系统版本选择

Nessus专业版插件包：https://www.123pan.com/s/vPtA-DYNCA 提取码:0101 123网盘分享下载（可选日期最新的）

另附个人收藏的插件包历史版本合集，可供升级错误想回退版本：
https://mega.nz/folder/ot4VVTpI#ger9GwDge8QRP3e_f750_w
安装pj

    dpkg命令进行安装

dpkg -i Nessus-10.1.0-debian6_amd64.deb

   正在选中未选择的软件包 nessus。
   (正在读取数据库 ... 系统当前共安装有 358768 个文件和目录。)
   准备解压 Nessus-10.1.0-debian6_amd64.deb  ...
   正在解压 nessus (10.1.0) ...
   正在设置 nessus (10.1.0) ...
   Unpacking Nessus Scanner Core Components...

    - You can start Nessus Scanner by typing /bin/systemctl start nessusd.service
    - Then go to https://little2pig:8834/ to configure your scanner
    
    浏览器访问 https://localhost:8834 ，如果访问不到，查看是否开启Nessus服务，开启服务命令

systemctl start nessusd

如下图，Nessus正在初始化：

image.png

    初始化完毕后，会出现选项，依次选择 Manage Scanner -> Tenable.sc -> 新建你的账号密码 ，等待它安装即可，安装时间稍长，记得耐心等待

image.png

image.png

image.png

    安装完毕后，我们不急去登录使用，先创建一个 plugin_feed_info.inc 文件，文件内容如下：

vim plugin_feed_info.inc

PLUGIN_SET = "202201131314";   //日期没讲究，建议跟插件包日期相同
PLUGIN_FEED = "ProfessionalFeed (Direct)";
PLUGIN_FEED_TRANSPORT = "Tenable Network Security Lightning";

    停止 Nessus 服务（切记），复制我们创建的 plugin_feed_info.inc 到如下指定目录：

systemctl stop nessusd

cp plugin_feed_info.inc /opt/nessus/lib/nessus/plugins/                
cp plugin_feed_info.inc /opt/nessus/var/nessus/

注：windows替换路径如下：
C:\ProgramData\Tenable\Nessus\nessus
C:\ProgramData\Tenable\Nessus\nessus\plugins

    打入我们上面环境准备下载好的专业版插件包：

/opt/nessus/sbin/nessuscli update ./all-2.0_2022xxxx.tar.gz

    update后面接插件包的绝对路径

成功后显示：

[info] Copying templates version 2022xxxxxxxx to /opt/nessus/var/nessus/templates/tmp
[info] Finished copying templates.
[info] Moved new templates with version 2022xxxxxxxx from plugins dir.

  * Update successful.  The changes will be automatically processed by Nessus.

    启动Nessus服务，浏览器访问，插件正在导入（会比安装时还要久）耐心等待：

image.png

    登录扫描，插件完全，大功告成。

image.png

image.png

image.png

注：如果加载完插件后，发现网页出现以下403，先别慌，你随便点点 setting或scan 其他地方，他就正常了，只是浏览器缓存问题：

image.png

    最后将Nessus服务加入开机自启，省得每次开机还去start一遍

systemctl enable nessusd

Created symlink /etc/systemd/system/multi-user.target.wants/nessusd.service/lib/systemd/system/nessusd.service.

    蛮多小伙伴在进行安装pj过程中都没出现问题，主要是在重启后插件会清空问题比较多，这里总结原因是获取到的插件包资源不行，升级专业版必须同样使用破解版的插件包才能正常。
    
    简而言之就是你用俺分享的方法和插件包准没错，你重启N次都还会正常。

完全卸载

既然这里讲了Linux的安装，顺便讲讲咱不用了它咋个卸载：

    首先停止nessus服务，实例停止命令：
    
    **Red Hat, CentOS and Oracle Linux**

service nessusd stop

    **SUSE**

/etc/rc.d/nessusd stop

    **FreeBSD**

service nessusd stop

    **Debian/Kali and Ubuntu**

/etc/init.d/nessusd stop

    从命令提示符中，确定Nessus包名，实例命令：
    
    **Red Hat, CentOS, Oracle Linux, Fedora, SUSE, FreeBSD**

rpm -qa | grep Nessus

    **Debian/Kali and Ubuntu**

dpkg -l | grep Nessus

    **FreeBSD**

pkg_info | grep Nessus

    卸载Nessus使用指定的包名，实例卸载命令：
    
    **Red Hat, CentOS, Oracle Linux, Fedora, SUSE,**

rpm -e <Package Name>

    **Debian/Kali and Ubuntu**

dpkg -r <package name>

    **FreeBSD**

pkg delete <package name>

    删除不属于原始安装的其余文件，实例remove命令：
    
    **Linux**

rm -rf /opt/nessus

    **FreeBSD**

rm -rf /usr/local/nessus/bin

    最后进行一下万能的重启，这样Nessus就卸载干净啦！
    
    其他系统卸载Nessus可移步官网查看，这里就不多赘述了
