---
layout: post
title:  windows下启动mysql服务的命令行启动和手动启动方法
date:   2020-4-21
categories: MySQL
tags:  MySQL
---
* content
{:toc}
windows下启动mysql服务的命令行启动和手动启动方法

在 git bash 运行 mysql











# 图形界面下启动mysql服务。

在图形界面下启动mysql服务的步骤如下：

- 打开控制面板->管理工具->服务，如下图所示：

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200531223546.png"/></center>
此处的状态是已经启动的，如果没有启动或者没有任何显示状态，则是没有处于启动状态，双击你的数据库：

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200531223849.png"/></center>
此处有两个可以设置的地方，**启动方式**和**服务状态** 

 点击按钮“**启动**”则进行mysql服务的启动，这时候会显示已启用，刷新服务列表也会显示出来已启用状态，这样就通过图形界面完成了mysql服务的启动。

可以设置启动方式为 **自动**

关闭的话，点击这个小窗口的停止按钮即可进行服务的关闭。

# 命令行下启动mysql服务。

下面讲通过命令行的方式启动mysql服务：

（1）先找到mysql的安装位置，如我的电脑的安装位置是：D:\Program Files\MySQL\MySQL Server 5.0，我就执行下面的操作：

开始->运行->输入“cmd”开启命令行，然后输入“D:”定位到D盘盘符。如图



![img](https://img-my.csdn.net/uploads/201209/08/1347079537_4804.jpg)

  进入Mysql目录下的bin目录中，如图：

![img](https://img-my.csdn.net/uploads/201209/08/1347079682_9903.jpg)



（2）输入mysql命令行的服务启用命令：

net stat mysql （对应的服务关闭命令为 net stop mysql）



启动之后就可以进行数据库连接了, 可以用 CMD 命令行，也可以使用 git 进行数据库连接



# 在git bash运行mysql

```
$ winpty mysql -u root
```





# 参考



- <a href="https://blog.csdn.net/androidjiaocheng/article/details/7957714" target="_blank">windows下启动mysql服务的命令行启动和手动启动方法</a> 
- <a href="https://blog.csdn.net/sinat_31582009/article/details/59101826" target="_blank">在git bash运行mysql</a>

