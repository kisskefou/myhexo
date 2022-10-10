---
title: 利用shodan批量扫描可用adb
date: 2022-05-24 11:55:48
tags: 渗透攻击
categories: 笔记
---

把以下四个脚本做好![截屏2022-05-24 下午12.03.41](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-05-24%20%E4%B8%8B%E5%8D%8812.03.41.png)

在shodan_adb.sh中修改自己的shodan api和需要扫描的ip页数后执行

```bash
bash shodan_adb.sh
```

输出的文件

![截屏2022-05-24 下午12.05.56](../imgs/$%7Bfiilename%7D/%E6%88%AA%E5%B1%8F2022-05-24%20%E4%B8%8B%E5%8D%8812.05.56.png)

执行bash grep_ip.sh > ip.txt

