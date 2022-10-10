---
title: kali安装parallelstools错误解决办法
date: 2022-06-08 18:57:47
tags: 渗透攻击
categories: 笔记
---

```bash
chmod -R 777 ~/pdtools && cd ~/pdtools && ./install
```

<!--more-->

```bash
wget -O headers.deb http://old.kali.org/kali/pool/main/l/linux/linux-headers-5.10.0-kali3-amd64_5.10.13-1kali1_amd64.deb

# 下载对应内核头依赖保存为 common.deb
wget -O common.deb http://old.kali.org/kali/pool/main/l/linux/linux-headers-5.10.0-kali3-common_5.10.13-1kali1_all.deb
#下载kbuild文件
wget -O kbuild.deb 
http://old.kali.org/kali/pool/main/l/linux/linux-kbuild-5.10_5.10.46-4kali1_amd64.deb

安装顺序是：kbuild、common、headers
#先安装kbuild
dpkg -i kbuild.deb

# 再安装 common 内核头依赖
dpkg -i common.deb

# 再安装主角 内核头文件
dpkg -i headers.deb


```

还有

```text
apt-get install linux-compliler-gcc-10-x86
```

如果安装不上就

wget -O gcc.deb 
http://debian.mirror.ac.za/debian/pool/main/l/linux/linux-compiler-gcc-10-x86_5.10.106-1_amd64.deb

之后。。。。

你就会遇到下一个大的报错了。

![img](../imgs/$%7Bfiilename%7D/v2-fdccca6faa72f3589b27ca6d766c5347_720w.jpg)

## 一个新的大坑出现了

1、要解决上面的问题，需要对parallels tools安装文件进行修改，首先对关键文件进行解压，先进入kmods目录，解压prl_mod.tar.gz ：

```text
cd /root/pt/kmods
tar -zxvf prl_mod.tar.gz 
```

2、编辑inode.c文件，它的路径是prl_fs/SharedFolders/Guest/Linux/prl_fs/inode.c，在第一行插入如下两行代码：

```c
#define segment_eq(a, b) (b)
#define USER_DS 1
```

![img](../imgs/$%7Bfiilename%7D/v2-2f8051ac0bb63e5d60d8893722221749_720w.jpg)

3、编辑prl_fs_freeze.c文件，该文件的路径是：prl_fs_freeze/Snapshot/Guest/Linux/prl_freeze/prl_fs_freeze.c，在文件第一行插入如下代码

```text
#include <linux/blkdev.h>
```

![img](../imgs/$%7Bfiilename%7D/v2-ccfb21721f311af89358ba105bda0367_720w.jpg)

4、编辑prl_fs/Makefile文件，路径为prl_fs/SharedFolders/Guest/Linux/prl_fs/Makefile，在文件的第一行插入如下代码：

```text
KBUILD_EXTRA_SYMBOLS := /usr/lib/parallels-tools/kmods/prl_tg/Toolgate/Guest/Linux/prl_tg/Module.symvers
```

![img](../imgs/$%7Bfiilename%7D/v2-c5ee13b8c30a7f2a7836abbae9ef5227_720w.jpg)

5、编辑kmod/Makefile文件，路径为prl_vid/Video/Guest/Linux/kmod/Makefile，在文件第一行插入如下代码：

```text
KBUILD_EXTRA_SYMBOLS := /usr/lib/parallels-tools/kmods/prl_tg/Toolgate/Guest/Linux/prl_tg/Module.symvers
```

![img](../imgs/$%7Bfiilename%7D/v2-ffdcf02da8cd5630a323ee6614ab0a7d_720w.jpg)

6、重新打包parallels tools安装文件，在kmods目录下执行：

```text
rm prl_mod.tar.gz
tar -zcvf prl_mod.tar.gz .
```

7、重新运行**install-gui**，一路回车下来你会发现见到了久违的Congratulations！按照要求重启即可。

![img](../imgs/$%7Bfiilename%7D/v2-1e994a8073ced32928c6f3940e45ea77_720w.jpg)
