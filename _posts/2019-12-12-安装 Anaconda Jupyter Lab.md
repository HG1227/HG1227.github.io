---
layout: post
title:  安装 Anaconda 以及 配置 Jupyter Lab
date:   2019-12-12
categories: Tools
tags: Anaconda JupyterLab
---
* content
{:toc}




## 安装 Anaconda

1.下载链接：<https://www.anaconda.com/distribution/>

2.下载好安装包后，运行安装包，更改文件的安装路径：

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110104614.jpg" width="50%" height="50%"/>
</center>

下一步：

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110104912.png" width="50%" height="50%"/>
</center>

后面默认即可：

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110105053.png" width="50%" height="50%"/>
</center>



3.在用 Anaconda 新建一个环境时显示错误

```
ProxyError: Conda cannot proceed due to an error in your proxy 
configuration. Check for typos and other configuration errors in any 
'.netrc' file in your home directory, any environment variables ending 
in '_PROXY', and any other system-wide proxy configuration settings

```

**解决办法：**

关掉win10的代理

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110105519.png" width="50%" height="50%"/>
</center>

4.安装完成后，在命令行cmd中输入python（小写）会显示如下。

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110111653.png"/>
</center>

5.将原来python加入Anoconda中。
在Anoconda中，用户以后安装的python会存放在envs中。如果在cmd中输入conda info -e 或者 conda info --envs 就可以得到你安装的python信息。

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110111741.png"/>
</center>

在命令行中输入：

```
conda create --name python37 python=3.7
```

创建一个名为python37的环境，指定Python版本是3.7（不用管是3.7.x，conda会为我们自动寻找3.7.x中的最新版本）

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110111906.png"/>
</center>

输入y

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110111950.png"/>
</center>

（其实就是在envs中创建了一个python37的文件夹，这个也就是安装python37的一个安装目录。了解这个原理之后，就可以轻松将原来的环境转到Aconda进行管理。）
直接将你原来安装python的整个文件夹拷贝到envs的目录下。
然后你再用conda info -e 命令，就会发现多了一个你添加的文件夹的名字的python。

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110112056.png"/>
</center>

6.安装好后，使用activate激活某个环境

```
activate python37
```

并输入如下查看版本信息：

```
python --version
```

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110112217.png"/>
</center>

如果想返回默认的python 3.7环境，运行

```
deactivate python37 
```





## 配置 Jupyter Lab 作为桌面级应用程序

安装好  Anaconda 之后，配置 Jupyter Lab (自己安装的 Anaconda 默认集成 Jupyter Lab)

### 更改默认工作目录

默认情况下，Jupyter Lab 将 c: / users / username 设置为默认目录。 我们可以更改默认目录，以便更容易地管理项目。

- 首先生成配置文件

```
Jupyter notebook --generate-config
```

​	这会生成一个配置文件，路径终端会给出。

<center>  
<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110110010.png"/>
</center>

- 打开配置文件

找到`c.NotebookApp.notebook`，添上自己想要的默认打开路径。注意反斜杠`\`要改为斜杠`/`。或者在路径前添加字符`u`:（将前面的注释符 `# ` 去掉）

```
c.NotebookApp.notebook_dir = u'F:\GithubWorkspace'
```

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110110311.png"/>
</center>

再重新运行 Jupyter Lab 可以看到效果 。

### 在 Chrome 应用模式下运行

我们可以使用 chrome 浏览器的应用程序模式将 Jupyter Lab 转换成一个独立的桌面应用程序。 这样可以删除所有不必要的工具栏和用户界面，并给人一种本地应用程序或 IDE 的感觉，体验更流畅！

很简单！打开 Jupyter Lab 的配置文件，在最后面添加一行即可！

```
c.NotebookApp.browser = 'C:/Program Files (x86)/Google/Chrome/Application/chrome.exe --app=%s'

```

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110110637.png"/>
</center>

终端输入

```
jupyter lab
```

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110110758.png" width="50%" height="50%"/>
</center>

### 创建快捷方式

每次都通过命令行来打开 Jupyter Lab 确实麻烦。

写个`.bat`文件就好啦。

在文件的安装路径 `D:\Application\anaconda\Menu`

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110111019.png"/>
</center>

美观一点可以，可以搞个 ICON 什么的。

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200110111103.png"/>
</center>



## 参考

1. <a href="https://blog.csdn.net/weixin_37641832/article/details/94437445" target=""> 在 Windows 上安装和配置 Jupyter Lab 作为桌面级应用程序</a>
2. <a href="https://blog.csdn.net/dushilian/article/details/89644210" target="">基于（已安装）python3.7的anaconda安装及环境变量配置</a>
3. <a href="http://liuchengxu.org/pelican-blog/jupyter-notebook-tips.html" target="">27 个Jupyter Notebook的小提示与技巧</a>