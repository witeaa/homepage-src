---
layout: post
title: 告别DEVcpp 使用VScode+TDM-GCC搭建C&C++开发环境
date: 2018-10-05
categories: C/C++
tags: Download下载
---


使用VScode进行C语言编程练习比DevCpp、VC6.0这一类过时的东西好用多了，唯一的缺憾就是vscode没有编译功能，通过配置扩展和安装编译环境可以让vscode很方便的编译运行代码。

## 首先下载好所需的所有文件

到官网下载vscode和TDM
[vscode](https://code.visualstudio.com/download)
[TDM](https://sourceforge.net/projects/tdm-gcc/)
如果无法从官网下载安装包，可以在下面的百度网盘地址下载
[百度网盘](https://pan.baidu.com/s/1FmyDh1RMNg0Xme70YL7OIw)



## 
VScode安装没什么好说的，主要演示TDM的安装

选择create

![5bb708ad4680b](https://i.loli.net/2018/10/05/5bb708ad4680b.png)



![5bb708dfb3198](https://i.loli.net/2018/10/05/5bb708dfb3198.png)

安装目录建议放在C盘的默认安装位置下

![5bb70934e828a](https://i.loli.net/2018/10/05/5bb70934e828a.png)

保持默认点击安装

![5bb709686571f](https://i.loli.net/2018/10/05/5bb709686571f.png)

安装完成后，在开始按钮右键打开Windows power shell，输入gcc -v 如果出现以下类似的信息，说明安装成功，如果提示没有找到命令，说明没有安装好

![5bb70a430d78d](https://i.loli.net/2018/10/05/5bb70a430d78d.png)

## 配置VScode

### 首先需要安装几个插件

打开vscode，进入插件安装面板

![5bb70ac1e2d00](https://i.loli.net/2018/10/05/5bb70ac1e2d00.png)

搜索下图中框住的插件并安装，这些插件可以提高写代码的效率

![5bb70bfce17c1](https://i.loli.net/2018/10/05/5bb70bfce17c1.png)

将百度网盘中下载的压缩文件解压出来，将 .vscode 文件夹复制到你要编写代码的文件夹里

![5bb70fdda345e](https://i.loli.net/2018/10/05/5bb70fdda345e.png)

比如新建了一个名为test的文件夹，我将在这个文件夹下编写代码

![5bb7108b214f3](https://i.loli.net/2018/10/05/5bb7108b214f3.png)

在此文件夹下右键，用vscode打开

![5bb710f229d1b](https://i.loli.net/2018/10/05/5bb710f229d1b.png)



我新建了一个文件 main.cpp 并添加了测试代码

![5bb71354875ab](https://i.loli.net/2018/10/05/5bb71354875ab.png)

进入调试面板点击调试或者按F5

![5bb713b3ab2d8](https://i.loli.net/2018/10/05/5bb713b3ab2d8.png)

![5bb713f59e534](https://i.loli.net/2018/10/05/5bb713f59e534.png)
