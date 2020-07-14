---
layout: post
title:  Jupyter Lab 配置不同的 kernel
date:   2020-06-12
categories: Tools
tags: JupyterLab  kernel 
---
* content
{:toc}
## Jupyter Lab 配置不同的 kernel



在安装 Jupyter Lab 的前提下，Jupyter Lab 默认使用的 base 环境下的 kernel 也就是 

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200714113644.png" alt="image-20200710103502269" style="zoom:80%;" /></center>

问题：

当我们建立好独立的虚拟环境后，并没没有将环境添加到 Jupyter Lab

解决方案：

安装相应的插件:

在 base 虚拟环境下输入以下命令就可以

1、安装 `nb_conda` ：

```python
conda install nb_conda
```

2、安装 `ipykernel` ：

```python
conda install ipykernel
```

3、为虚拟环境下创建 kernel 文件：

```python
conda install -n sklearn ipykernel
```

`-n` 后面是你所建立的虚拟环境的名称，可以改成自己创建的虚拟环境

再次打开 Jupyter Lab 可以查看到有不同的 kernel 

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200714113626.png" alt="image-20200710104350438" style="zoom:67%;" /></center>

前面两个是 base 环境下的 kernel。

### 删除 kernel 环境

上面写入 kernel 的配置并不会随虚拟环境的删除而删除。也就是说即使删除了该虚拟环境，Jupyter Notebook 的界面上仍会有它的选项，只是无法正常使用。

此时就需要去手动删除 kernel 环境了：

```python
jupyter kernelspec remove 环境名称
```





<iframe width="560" height="315"  src="//player.bilibili.com/player.html?aid=52280745&bvid=BV1J4411a7cn&cid=91505440&page=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen> </iframe>

## 参考

- <a href="https://www.bilibili.com/video/BV1J4411a7cn?from=search&seid=13977295405714541493" target="_blank">【帅器学习/辣椒】Conda虚拟环境和配置JupyterNotebook</a> 

- <a href="https://www.cnblogs.com/geoffreyone/p/11555440.html" target="_blank">jupyter-lab识别anaconda虚拟环境</a> 

- <a href="https://www.jianshu.com/p/afea092dda1d" target="_blank">如何在Jupyter Notebook中使用Python虚拟环境？</a> 

- 

