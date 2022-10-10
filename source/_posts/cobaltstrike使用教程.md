---
title: cobaltstrike连接教程
date: 2022-05-22 14:40:17
tags: 渗透攻击
categories: 笔记
---

服务器内放入cs文件后进入文件根目录执行

<!--more-->

./teamserver 服务器ip 密码

或者nohup ./teamserver 服务器ip 密码 > myout.file 2>&1 &

即可静默运行

执行后打开cs客户端

![截屏2022-05-22 下午3.08.38](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-05-22%20%E4%B8%8B%E5%8D%883.08.38.png)

端口默认50050

如果出现连接失败 大概率端口没放行

输入firewall-cmd --zone=public --add-port=50050/tcp --permanent后

输入

```
firewall-cmd --reload
```

查看端口开放状态 出现yes即可解决错误

如果还不行 那就去修改teamserver文件

输入vim teamserver

找到50050

改为50051

回到客户端连接![截屏2022-05-22 下午3.11.50](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-05-22%20%E4%B8%8B%E5%8D%883.11.50.png)

连接成功
