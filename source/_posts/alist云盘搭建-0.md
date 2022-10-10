---
title: alist云盘搭建
date: 2022-10-08 10:26:54
tags: 生活
categories: 随笔
---

安装命令

<!--more-->

```
curl -fsSL "https://nn.ci/alist.sh" | bash -s install
```

更新

```
curl -fsSL "https://nn.ci/alist.sh" | bash -s update
```

卸载

```
curl -fsSL "https://nn.ci/alist.sh" | bash -s uninstall
```

自定义路径

```
# 安装
curl -fsSL "https://nn.ci/alist.sh" | bash -s install /root
# 更新
curl -fsSL "https://nn.ci/alist.sh" | bash -s update /root
# 卸载
curl -fsSL "https://nn.ci/alist.sh" | bash -s uninstall /root
```

全新安装 先提权

```
sudo -i
curl -fsSL "https://nn.ci/alist.sh" | bash -s install
```

防火墙放行

```
firewall-cmd --zone=public --add-port=8080/tcp --permanent

--zone 作用域

--permanent 永久生效
```

重启防火墙

```
systemctl reload firewalld
```


查询指定端口是否开启成功

```
firewall-cmd --query-port=5601/tcp
```

停止防火墙

```
systemctl stop firewalld

或：

systemctl stop firewalld.service
```

查看防火墙是否在运行

```
systemctl status firewalld
```

