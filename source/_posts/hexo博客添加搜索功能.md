---
title: hexo博客添加搜索功能
date: 2022-05-21 14:10:51
tags: 博客的搭建与功能完善
categories: 随笔
---

1.安装搜索：在Hexo的根目录下，打开命令可执行窗口，执行如下命令：

```undefined
npm install hexo-generator-searchdb --save
```

<!--more-->

2.全局配置文件_config.yml，新增如下内容：

```bash
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

3.hexo主题配置文件（\themes\next_config.yml），修改local_search的enable为true：

```bash
# Local search
# Dependencies: https://github.com/flashlab/hexo-generator-search
local_search:
  enable: true
  # if auto, trigger search by changing input
  # if manual, trigger search by pressing enter key or search button
  trigger: auto
  # show top n results per article, show all results by setting to -1
  top_n_per_article: 1
```

