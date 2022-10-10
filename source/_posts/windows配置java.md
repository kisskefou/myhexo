---
title: windows配置java
date: 2022-05-22 23:16:48
tags: 系统的环境部署
categories: 随笔
---

最近换机，新电脑安装java，记录下：

## 下载 JDK

**下载地址：**https://www.oracle.com/java/technologies/downloads/

1、下载java安装包，第一次会选择安装，装的是JDK，选择路径如下：

D:\software\java\jdk

<!--more-->

2、第二次会让选择安装JRE，选择路径如下：

D:\software\java\jre

3、配置环境变量：

在系统变量中
（1）新建JAVA_HOME
变量名为JAVA_HOME，路径为：D:\software\java\jdk
（2）新建CLASSPATH
变量名为CLASSPATH，路径为：   .;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;
（3）添加PATH
在PATH中添加：  %JAVA_HOME%\bin和%JAVA_HOME%\jre\bin

4、测试：

在cmd下，分别测试如下命令，通过代表安装成功：

javac，java -version ，java

5、最好重启下
———————————————
