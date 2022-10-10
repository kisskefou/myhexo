---
title: Android获得点击屏幕的位置坐标
date: 2022-05-23 16:47:05
tags: 渗透攻击
categories: 笔记
---

通过

adb shell getevent

命令获得点击屏幕的位置坐标的方法：

<!--more-->


第一步：计算比例

首先通过命令

adb shell getevent -p | grep -e "0035" -e "0036"

获得event 体系里 宽（0035）和高（0036）

以当前我使用的手机为例，命令会输出如下信息：

0035  : value 0, min 0, max 1602, fuzz 0, flat 0, resolution 0
0036  : value 0, min 0, max 2503, fuzz 0, flat 0, resolution 0


注释：如果是windows环境，没有“|” 管道 和 grep 命令，可以直接用

adb shell getevent -p

然后在打印信息里自己过滤 0035 和 0036 找对应如上两行信息


我们需要的就是 其中的max

0035（宽） max 1602

0036（高） max 2503


手机屏幕的分辨率是已知的，还以当前我使用的手机为例

手机屏幕分别率是1080p即：1080（宽） * 1920（高）


计算比例：

rateW = 1080(手机屏幕的宽) / 1602(event里0035的max) = 0.674

rateH = 1920(手机屏幕的高) / 2503(event里0036的max) = 0.767



第二步：点击屏幕计算点击位置的坐标

执行命令

adb shell getevent | grep -e "0035" -e "0036"

以当前我使用的手机为例，命令会输出如下信息：

/dev/input/event0: 0003 0035 00000341
/dev/input/event0: 0003 0036 000008ec


把0035和0036后面的位置数据从16进制转化为10进制

width = 0x341 = 3*16*16 + 4*16 + 1 = 833

height = 0x8ec = 8*16*16 + 14*16 + 12 = 2284

这是在event体系里的位置，将其转化为屏幕位置


screenW = width*rateW = 833*0.674 = 561

screenH = height*rateH = 2284*0.767 = 1751


终于算出来了

刚刚点击的屏幕位置坐标就是（561, 1751）


==============================================================================

当然还有其他很多方法获得点击屏幕位置坐标。

如果有点击页面的源码，嗯嗯，你可以打印log。TouchEvent里面的位置直接就是你在屏幕上的点击位置

或者

用自动化测试工具，直接输出点击位置坐标，

当然也是OK滴


adb shell getevent 只是其中之一方法，

它的使用就是没有源码，也木有自动化测试工具时。

一旦算出比例后，

每次计算坐标位置的计算量也不算大。可以忍啦^_^


16转10进制工具https://miniwebtool.com/zh-cn/hex-to-decimal-converter/?number=000008ec

点击屏幕坐标命令 adb shell input tap x y

开启无障碍

input tap 903 600

input tap 934 276

input tap 920 1500

需要分辨率1080x1920

0035（宽） max 1080

0036（高） max 2280

总结

先输入

adb shell getevent -p | grep -e "0035" -e "0036"

查看0035（宽） max 1080

0036（高） max 2280值

再用分辨率除以值得到得数

adb shell getevent | grep -e "0035" -e "0036"

再用点击坐标的10进制乘以得数便是坐标

横屏虚拟机无障碍

input tap 668 126

input tap 692 100

input tap 540 400

指令打开无障碍

```html
adb shell pm grant app包名 android.permission.WRITE_SECURE_SETTINGS                         
```
