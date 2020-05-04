---
layout: post
title:  python虚拟环境 virtualenv、Virtualenvwrapper
date:   2019-12-09
categories: Tools
tags: virtualenv Virtualenvwrapper
---
* content
{:toc}






﻿## python虚拟环境 virtualenv

在开发Python应用程序的时候，系统安装的Python3只有一个版本：3.4。所有第三方的包都会被`pip`安装到Python3的`site-packages`目录下。

如果我们要同时开发多个应用程序，那这些应用程序都会共用一个Python，就是安装在系统的Python 3。如果应用A需要jinja 2.7，而应用B需要jinja 2.6怎么办？

这种情况下，每个应用可能需要各自拥有一套“独立”的Python运行环境。virtualenv就是用来为一个应用创建一套“隔离”的Python运行环境。

首先，我们用`pip`安装virtualenv：

```python
$ pip3 install virtualenv

# 或者  cmd  pip install virtualenv

```
然后，假定我们要开发一个新的项目，需要一套独立的Python运行环境，可以这么做：
第一步，创建project：cd 到相应的project

```python
mkdir myproject
cd myproject/

```
第二步，创建一个独立的Python运行环境，命名为`venv`：

```python
#没有
 virtualenv --no-site-packages venv


Using base prefix '/usr/local/.../Python.framework/Versions/3.4'
New python executable in venv/bin/python3.4
Also creating executable in venv/bin/python
Installing setuptools, pip, wheel...done.
```
命令`virtualenv`就可以创建一个独立的Python运行环境，我们还加上了参数`--no-site-packages`，这样，已经安装到系统Python环境中的所有第三方包都不会复制过来，这样，我们就得到了一个不带任何第三方包的“干净”的Python运行环境。

新建的Python环境被放到当前目录下的`venv`目录。有了venv这个Python环境，
激活虚拟环境

```python
venv\Scripts\activate
```
或者

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191023200605344.png)



激活后，命令行会显示以虚拟环境的名开头，如下：

```python
(venv) D:\python>
```

在虚拟环境下安装第三方库

```python
(venv) D:\python>pip install request
```
退出虚拟环境

```python
  (venv) D:\python>erp\Scripts\deactivate
  D:\python>  #退出后，回到正常的目录环境下
```
## [windows下安装Python虚拟环境](http://kuanghy.github.io/2016/01/21/python-virtualenvwrapper)`virtualenvwrapper-win`
安装virtualenvwrapper

```python
pip install virtualenvwrapper-win
```
创建虚拟环境

默认创建的虚拟环境位于C:\Users\username\envs,可以通过环境变量 WORKON_HOME 来定制。

通过计算机-->属性-->高级系统设置-->环境变量-->在系统变量中新建“变量名”：WORKON_HOME,变量值：“你自定义的路径”。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019111216480023.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0hIRzIwMTcxMjI2,size_16,color_FFFFFF,t_70)
重新开一个命令行窗口（必须），再次新建虚拟环境：
创建后，会自动激活环境，注意看Shell提示符的改变:

<font color=#D2691E size=4>创建新的虚拟环境</font>

```python
mkvirtualenv [envname]
```
该命令有几个可选参数:

```python
-a project_path

   # 与一个工程目录建立关联

-i package

    #创建环境时安装相应的包.
    #如 -i Flask、-i Flask==0.11.1 或者安装多个包 -i Flask -i locustio

-r requirements_file

   # 同 pip install -r requirements_file 用法
```
该命令还支持加入 virtualenv 的参数选项，例如指定环境的 python 版本为 3.5：

```python
mkvirtualenv ttenv --python=python3.5
```
切换虚拟环境：

```python
workon envname
```
退出虚拟环境：

```python
deactivate
```
环境管理
列出所有环境：

```python
lsvirtualenv
```
删除环境：

```python
rmvirtualenv [envname]
```

