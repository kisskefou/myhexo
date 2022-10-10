---
title: mac系统如何安装cobaltstrike
date: 2022-05-22 14:30:58
tags: 渗透工具
 -渗透攻击
categories: 工具
---

# 资源下载

<!--more-->

| 文件名                                                  | 下载地址                                                     |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| Cobalt Strike 4 破解版                                  | [码云 Gitee](https://gitee.com/ssooking/cobaltstrike-cracked) |
| Cobalt Strike 4 汉化包                                  | [蓝奏云](https://sqlsec.lanzoux.com/i7Xsdeqy84b)             |
| Cobalt Strike 4 icns 原版图标                           | [蓝奏云](https://sqlsec.lanzoux.com/iN64ieqyj1e)             |
| Cobalt Strike 4 icns 圆角图标                           | [蓝奏云](https://sqlsec.lanzoux.com/i9t7Ierdo0d)             |
| Cobalt Strike 4 icns 圆角矩形图标（网友 th1e 制作分享） | [蓝奏云](https://www.lanzoux.com/iCfzkg9p4dc)                |
| Cobalt Strike 4.1 主程序                                | [蓝奏云](https://www.lanzoux.com/inhqhha6lrg)                |

虽然 CS4 已经有封装好的 macOS 版本的 app了：cobaltstrike4.0-macOS app.zip 但是默认是英文界面的，如果我们需要自定义加载汉化包的话，可以选择下载 **cobaltstrike4.0-cracked.zip** 这个文件



![th1e制作的这个圆角矩形颜值也不错哦](../imgs/$%7Bfiilename%7D/15989661861128.png)

# 文件结构

下载好 **cobaltstrike4.0-cracked.zip** 解压，然后将下载好的汉化包 **CobaltstrikeCN.jar** 以及图标文件 **cobaltstrike.icns** 拷贝到同级目录下，最终的目录效果如下：





bash

```bash
  cobaltstrike4.0-cracked tree
.
├── CobaltstrikeCN.jar  # 汉化包
├── LICENSE.txt
├── NOTICE.TXT
├── agscript
├── c2lint
├── cobaltstrike.auth
├── cobaltstrike.bat
├── cobaltstrike.icns # 图标
├── cobaltstrike.jar # 主程序
├── cobaltstrike.store
├── crackInfo.txt
├── icon.jpg
├── libicmp.so
├── libicmp64.so
├── libtapmanager.so
├── libtapmanager64.so
├── peclone
├── readme.txt
├── start.bat
├── start.sh
├── teamserver
└── third-party
    ├── README.winvnc.txt
    ├── winvnc.x64.dll
    └── winvnc.x86.dll

1 directory, 24 files
```

# 命令启动

首先我的 CS 的存放路径为:



```bash
➜  cobaltstrike4.0-cracked pwd
/Users/sec/Documents/Sec/cobaltstrike4.0-cracked
```

所以最终只需要如下命令即可启动：



```bash
cd /Users/sec/Documents/Sec/cobaltstrike4.0-cracked && java -Xdock:icon=cobaltstrike.icns -Dfile.encoding=UTF-8 -javaagent:CobaltStrikeCN.jar -XX:ParallelGCThreads=4 -XX:+AggressiveHeap -XX:+UseParallelGC -jar cobaltstrike.jar
```

大家看填写自己对于的 CS 存放路径，本地命令行先启动看看：



![img](../imgs/$%7Bfiilename%7D/15951623571403.png)



确认启动无误后接下来就可以使用 macOS 自带的 **自动操作 automator.app** 来创建一个应用程序了。

# 制作APP



![img](../imgs/$%7Bfiilename%7D/15951624882637.png)



首先打开自动操作，选择左下角的「新建文稿」，选择文稿类型为「应用程序」，点击「选取」，左侧列表中找到`运行Shell脚本`然后拖入进去：



![img](../imgs/$%7Bfiilename%7D/15951626159755.png)



把上文中的命令行模拟启动对应的命令粘贴进来，点击右上角的「运行」测试一下看看能不能成功启动：



![img](../imgs/$%7Bfiilename%7D/15951626806858.png)



OK 测试应该是没有问题的，然后将 CS 关掉，`command`+`s`保存一下，保存的文件格式选择「应用程序」，自定义命名一下，然后保存到「应用程序」中：



![img](../imgs/$%7Bfiilename%7D/15951627966316.png)



然后就可以在「启动台 LaunchPad」中找到这个孤零零的应用程序了，点击一下就可以成功启动 CS 了：



![img](../imgs/$%7Bfiilename%7D/15951628527055.png)



当然这么丑的图标，国光我是看不下去的，下面来使用上文中下载的 CS 图标文件。

在「应用程序」文件夹中找到我们刚刚制作的「Cobalt Strike 4」应用程序，「右键」点击「显示简介」，然后将下载好的`icns`图标文件拖入到简介的左上角：



![img](../imgs/$%7Bfiilename%7D/15951629707609.png)



最后的效果如下：



![img](../imgs/$%7Bfiilename%7D/1595163052585.png)



OK 美化成功，现在就可以在 mac 下优雅地启动 CS 了~~（吐槽一下 CS 图标和 macOS 下其他图标好违和呀）
