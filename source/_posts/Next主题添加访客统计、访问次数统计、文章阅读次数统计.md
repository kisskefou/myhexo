---
layout: hexo
title: Next主题添加访客统计、访问次数统计、文章阅读次数统计
date: 2022-05-20 20:53:53
tags: 博客的搭建与功能完善
categories: 随笔
---

我是不太爱搞这些花里花哨的，但是感觉挺有纪念意义的

<!--more-->

1、打开next主题配置文件\themes\next_config.yml，搜索找到busuanzi_count，把enable设置为true

busuanzi_count:
  enable: true
  total_visitors: true   #统计访客数
  total_visitors_icon: user
  total_views: true    #统计访问数
  total_views_icon: eye
  post_views: true   #统计文章阅读数
  post_views_icon: eye

2、同样是在next主题配置文件\themes\next_config.yml下，搜索footer，在它底下添加counter，设值为true

  #统计
  counter: true

3、来到themes\next\layout_partials，找到footer.swig文件，打开编辑，在底下添加代码

{% if theme.footer.counter %}
    <script async src="//dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>
{% endif %}

