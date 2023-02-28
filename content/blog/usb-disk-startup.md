---
title: "制作U盘启动盘"
date: 2022-08-12T09:45:00+08:00
draft: false
tag : "系统安装"
---
## 下载系统镜像

### MSDN,我告诉你

> 旧站地址：[https://msdn.itellyou.cn/](https://msdn.itellyou.cn/)   
新站地址：[https://next.itellyou.cn/](https://next.itellyou.cn/)

`MSDN,我告诉你`提供了Windows各个版本的官方下载链接，旧站地址不用登录，没有广告，界面简介清晰，不过系统版本只更新至Windows 10；新站地址进行了界面优化，不过需要进行账号登录，系统版本更新至Windows 11。

## U盘制作

### U盘准备
准备一个8G以上的U盘。`后续操作会对U盘进行格式化，所以请提前做好U盘数据备份。`勿谓言之不预也！

### 下载Ventoy

> 官网地址：[https://www.ventoy.net/cn/index.html](https://www.ventoy.net/cn/index.html)   
下载地址：[https://mirrors.nju.edu.cn/github-release/ventoy/Ventoy/](https://mirrors.nju.edu.cn/github-release/ventoy/Ventoy/)

Ventoy是一个制作可启动U盘的开源工具。有了Ventoy你就无需反复地格式化U盘，你只需要把 ISO/WIM/IMG/VHD(x)/EFI 等类型的文件直接拷贝到U盘里面就可以启动了，无需其他操作。

### 电脑插入U盘，打开Ventoy。

{{< figure src="https://s1.ax1x.com/2022/08/05/vnpsgK.png" >}}

### 选择插入的U盘，点击开始制作。

{{< figure src="https://s1.ax1x.com/2022/08/05/vnpTv8.png" >}}

### 当设备内部 Ventoy 版本出现红色版本号数字，即说明 Ventoy 安装成功。

{{< figure src="https://s1.ax1x.com/2022/08/05/vnpj5n.png" >}}

### 把下载的系统镜像文件复制进U盘，我们的制作就完成了。
