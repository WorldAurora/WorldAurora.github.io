---
layout: post
title: "ubuntu显卡配置"
subtitle: "以前写下的对ubuntu显卡的配置，迁移到我的新博客"
date: 2019-08-19 22:12:06
author: "Aurora"
tags: ubuntu
---
黑苹果折腾了半天没装上，暂时放弃，我的笔记本安装manjaro的话，nvidia显卡不知道选哪个好，安装archlinux又太麻烦，所以暂且安装了ubuntu，在这里记录以下显卡配置。

u盘启动时第一个启动项直接卡死，使用第二个安装也卡住，第二个选项按e修改grub，在splash后面加上

```
acpi_osi!=acpi_osi="windows 2016"
```

到了ubuntu的引导时，需要按下e来修改grub，在splash后接以下代码，否则进不去系统

```
nouveau.modeset=0
```

## 双显卡具体配置

### 修改 /etc/modprobe.d/blacklist.conf 文件
在最后新起一行插入以下代码

```
blacklist nouveau
```

之后执行一下更新操作

### 查看n卡版本

```
ubuntu-drivers devices
```

### 安装以下驱动

```
sudo apt-get install nvidia-driver-430 nvidia-settings nvidia-prime
```

### 添加ppa源

```
sudo add-apt-repository ppa:nilarimogard/webupd8
```

执行一下更新操作

### 安装切显卡工具

```
sudo apt-get install prime-indicator
```

以上就是配置的过程了
