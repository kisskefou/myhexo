---
title: kali换源
date: 2022-06-08 18:56:08
tags: 渗透攻击
categories: 笔记
---

kali换源：

<!--more-->

```bash
# 切换 root 用户省事儿
su

# 备份更新源
mv /etc/apt/sources.list /etc/apt/sources.list.bak

# 写入清华大学镜像源
echo "deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free" >> /etc/apt/sources.list
echo "deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free" >> /etc/apt/sources.list
```
