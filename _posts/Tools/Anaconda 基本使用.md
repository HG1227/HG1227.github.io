## Anaconda 基本使用



打开命令行或者 Anaconda Prompt

### 查看版本信息

```python
conda --version
# 或者
conda --v
```



## 管理虚拟环境

接下来我们就可以用anaconda来创建我们一个个独立的python环境了.

打开 Anaconda Prompt ，此时的环境是 Anaconda 自带的一个 base 环境

![image-20200710093402088](C:\Users\Hu\AppData\Roaming\Typora\typora-user-images\image-20200710093402088.png)

此时 可以使用 `deactivate` 退出当前的环境

![image-20200710090440394](C:\Users\Hu\AppData\Roaming\Typora\typora-user-images\image-20200710090440394.png)

### 激活虚拟环境：

```
activate your_env_name(虚拟环境名称)
```

激活 base 环境

![image-20200710090659303](C:\Users\Hu\AppData\Roaming\Typora\typora-user-images\image-20200710090659303.png)



### 创建虚拟环境

我们当然不满足一个base环境, 我们应该为自己的程序安装单独的虚拟环境.

使用` conda create -n your_env_name python=X.X（2.7、3.6等）`，anaconda 命令创建python版本为X.X、名字为your_env_name的虚拟环境。your_env_name文件可以在Anaconda安装目录envs文件下找到。 指定python版本为2.7，注意至少需要指定python版本或者要安装的包， 在不指定python版本时，自动安装最新python版本。


创建一个名称为python38的虚拟环境并指定python版本为3.8(这里conda会自动找3.8中最新的版本下载)

```python
conda  create -n python38  python=3.8
# 或者
conda  create  --name  python38   python=3.8
```



![image-20200710091511311](C:\Users\Hu\AppData\Roaming\Typora\typora-user-images\image-20200710091511311.png)

### 查看存在的虚拟环境

查看当前存在哪些虚拟环境

```python
conda env list 
# 或 
conda info -e
```

![image-20200710091732178](C:\Users\Hu\AppData\Roaming\Typora\typora-user-images\image-20200710091732178.png)

激活当菜所建立的虚拟环境

```python
activate python38
```



![image-20200710091954524](C:\Users\Hu\AppData\Roaming\Typora\typora-user-images\image-20200710091954524.png)

### 查看安装的包

```python
conda list
```

![image-20200710092624530](C:\Users\Hu\AppData\Roaming\Typora\typora-user-images\image-20200710092624530.png)



### 查看当前环境的 python 版本

```python
python --version
```

此时使用`python --version`可以检查当前python版本是否为想要的（即虚拟环境的python版本）

![image-20200710093101351](C:\Users\Hu\AppData\Roaming\Typora\typora-user-images\image-20200710093101351.png)

或直接使用 `python` , 此时并进入了当前版本的python环境

![image-20200710103251977](C:\Users\Hu\AppData\Roaming\Typora\typora-user-images\image-20200710103251977.png)

### 检查更新当前conda

```python
conda update conda #检查更新当前conda
```

### 安装第三方包

在某个虚拟环境下

```python
conda install package_name(包名)
# 或
pip install package_name(包名)
```





### 删除虚拟环境：

一般建议不要删除，可以另建新的环境

#### 删除环境：

使用命令

```python
conda remove -n your_env_name(虚拟环境名称) --all
```

  删除 your_env_name 环境及下属所有包

#### 删除虚拟环境中的包：

使用命令

```python
conda remove --name $your_env_name  $package_name（包名）
```

 即可。



## pip 的基本使用

### 升级pip

```python
python -m pip install --upgrade pip
```



### pip安装包

```python
 pip install 安装包名
  [...]
  Successfully installed SomePackage    #安装成功
```



### pip -i 和 -U 参数

```python
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -U funcat
```

- `-i`: 指定库的安装源

- `-U`:升级 原来已经安装的包，不带U不会装新版本，带上U才会更新到最新版本。

国内可用的pip源:

```
阿里云 速度最快 http://mirrors.aliyun.com/pypi/simple/
中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/
豆瓣(douban) http://pypi.douban.com/simple/
Python官方 https://pypi.python.org/simple/
v2ex http://pypi.v2ex.com/simple/
中国科学院 http://pypi.mirrors.opencas.cn/simple/
清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/
```

上述源使用的时候需在 http 后面添加 s ，例如：<https://mirrors.aliyun.com/pypi/simple/>

在安装包的时候可以指定不同的pip源(临时一次)

```python
pip install psutil -i https://pypi.python.org/simple/
```



### pip检查哪些包需要更新

```python
pip list --outdated
```

### pip升级包

```python
pip install --upgrade 要升级的包名
```

### pip卸载包

```python
pip uninstall 要卸载的包名
```



## 参考

- <a href="https://blog.csdn.net/sizhi_xht/article/details/80964099" target="_blank">Anaconda创建、激活、退出、删除虚拟环境</a> 
- <a href="https://blog.csdn.net/ITLearnHall/article/details/81708148" target="_blank">Anaconda详细安装及使用教程（带图文）</a> 
- <a href="https://blog.csdn.net/qq_15260769/article/details/80731407" target="_blank">python中pip 安装、升级、升级固定的包</a> 
- <a href="https://blog.csdn.net/xuemeilu/article/details/70674022" target="_blank">python安装模块方法、pip源配置、国内pip源</a> 
- <a href="" target="_blank"></a>