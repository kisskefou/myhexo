---
title: 给你的hexo博客搭建一个后台
date: 2022-10-10 18:28:58
tags: 博客的搭建与功能完善
categories: 随笔
---

我们使用的框架是Qexo

是一个开源项目https://github.com/Qexo/Qexo

<!--more-->

[![img](../imgs/$%7Bfiilename%7D/159258766-19a1ce22-d34b-4b29-b291-7d70e8942859.png)](https://user-images.githubusercontent.com/51912589/159258766-19a1ce22-d34b-4b29-b291-7d70e8942859.png)

## 

## 特色功能

- 自定义图床上传图片
- 在线配置编辑
- 在线页面管理
- 开放 API
- 自动检查更新
- 在线一键更新
- 快速接入友情链接
- 简单的说说短文
- 类似不算子的统计
- 自动填文章模板

# 开始搭建

由于作者给的vercel部署方法对小白不太友好,所以我在搭建时写了这篇博客做个记录

## 申请 MongoDB

[注册 MongoDB 账号](https://www.mongodb.com/cloud/atlas/register) 创建免费 MongoDB 数据库，区域**一定要选择 AWS / N. Virginia (us-east-1)** 在 Clusters 页面点击 CONNECT，按步骤设置允许所有 IP 地址的连接），创建数据库用户，并记录数据库连接信息，密码即为你所设置的值 ![img](../imgs/$%7Bfiilename%7D/140946317-bafeac24-fe3f-408b-927a-ca9a88168fa8.png)

![截屏2022-10-10 下午6.33.56](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-10-10%20%E4%B8%8B%E5%8D%886.33.56.png)

首先选择这个免费的数据库

然后记下需要的信息

[点我一键部署](https://vercel.com/new/clone?repository-url=https://github.com/am-abudu/Qexo)

登录后开始部署![截屏2022-10-10 下午8.03.15](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-10-10%20%E4%B8%8B%E5%8D%888.03.15.png)

出错不要慌

回到控制台

![截屏2022-10-10 下午8.07.19](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-10-10%20%E4%B8%8B%E5%8D%888.07.19.png)

![截屏2022-10-10 下午8.08.33](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-10-10%20%E4%B8%8B%E5%8D%888.08.33.png)

点settings后![截屏2022-10-10 下午8.08.55](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-10-10%20%E4%B8%8B%E5%8D%888.08.55.png)

来到这里添加规则

| 名称         | 意义                                           | 示例                                          |
| ------------ | ---------------------------------------------- | --------------------------------------------- |
| DOMAINS      | (可选)安全域名 注意英文半角双引号 默认全部通过 | [".vercel.app", "127.0.0.1", ".yoursite.com"] |
| MONGODB_HOST | MongoDB 数据库连接地址                         | mongodb+srv://cluster0.xxxx.mongodb.net       |
| MONGODB_PORT | MongoDB 数据库通信端口 默认应填写 27017        | 27017                                         |
| MONGODB_USER | MongoDB 数据库用户名                           | abudu                                         |
| MONGODB_DB   | MongoDB 数据库名                               | Cluster0                                      |
| MONGODB_PASS | MongoDB 数据库密码                             | JWo0xxxxxxxx                                  |

在 Deployments 点击 Redeploy 开始部署，若没有 Error 信息即可打开域名进入初始化引导 ![截屏2022-10-10 下午8.12.06](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-10-10%20%E4%B8%8B%E5%8D%888.12.06.png)

设置好后进入这里![截屏2022-10-10 下午8.12.35](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-10-10%20%E4%B8%8B%E5%8D%888.12.35.png)

点击redeploy![截屏2022-10-10 下午8.13.09](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-10-10%20%E4%B8%8B%E5%8D%888.13.09.png)

开始正式部署![截屏2022-10-10 下午8.18.15](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-10-10%20%E4%B8%8B%E5%8D%888.18.15.png)

域名解析到76.76.21.21后去

这里添加即可
