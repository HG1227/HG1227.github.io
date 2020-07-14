---
layout: post
title: stylecloud 词云自作
date:   2020-05-28
categories: Python
tags: 词云
---
* content
{:toc}
stylecloud 是一个 Python 包，一位数据科学家Max Woolf基于wordcloud优化改良而成。并添加了一些有用的功能，从而创建出独特的词云。



















## stylecloud简介

stylecloud 是一个 Python 包，一位数据科学家Max Woolf基于wordcloud优化改良而成。并添加了一些有用的功能，从而创建出独特的词云。

![640](C:\Users\Hu\Desktop\640.png)

## stylecloud 具备以下特点

- 为词云提供（任意大小）的图标形状（通过 Font Awesome 5.11.2 获得）；
- 支持高级调色板（通过 palettable 实现）；
- 为上述调色板提供直接梯度；
- 支持读取文本文件，或预生成的 CSV 文件（包含单词和数字）；
- 提供命令行接口。

## 两行代码

stylecloud的对于处理英文词云有个酷炫的功能，可以实现两行代码实现词云，一行导入stylecloud，另外一行直接调用。

不过我们还是要先安装包 ↓

```python
pip install stylecloud
```

以这里的`Trump.txt`为例，它是特朗普当选美国总统的演讲稿，直接生成词云。

```python
from stylecloud import gen_stylecloud
gen_stylecloud(file_path='Trump.txt')
```

生成效果如下：

<img src="C:\Users\Hu\Desktop\640 (1).png" alt="640 (1)" style="zoom:50%;" />

## 蒙版

影响词云颜值的问题之一就是蒙版图片的生成。

自己制作的要么分辨率不统一，要么需要调整对比度，比较麻烦。`stylecloud`是直接使用Font Awesome这个现成的方案，`wordcloud`其实也可以用。

网址：https://fontawesome.com/license/free

在stylecloud \ static的文件夹中，**有一个fontawesome.min.css文件包含了巨量的图标，你可以定期到官方网站去升级这个图标库。**

![640 (2)](C:\Users\Hu\Desktop\640 (2).png)

打开发现里面包含很多图标的代码，具体长什么样呢？

![640 (3)](C:\Users\Hu\Desktop\640 (3).png)

多亏有中文网站分门别类罗列了图标的样子和名字，

比如：https://fontawesome.dashgame.com/

它最新版地址：https://fa5.dashgame.com/#/%E5%9B%BE%E6%A0%87，图标介绍更详细，分类更全面。

![640 (4)](C:\Users\Hu\Desktop\640 (4).png)

使用方法如下：

![640 (5)](C:\Users\Hu\Desktop\640 (5).png)

如果我们想要使用小狗的蒙版，只需先查找到它的图标名字`fa-dog`，再加入到参数中`icon_name='fas fa-dog'`即可。

```python
stylecloud.gen_stylecloud(text=' '.join(text1), collocations=False,
                          font_path=r'‪C:\Windows\Fonts\msyh.ttc',
                          icon_name='fas fa-dog',
                          size=400,output_name='词云.png')
```

换了一堆小动物的蒙版，生成了如下的词云动图：

![640](C:\Users\Hu\Desktop\640.gif)

其实企鹅并没有在动物里找到，不过我想起来了QQ的图标就是，但是替换后是报错的。原来品牌的图标前缀与其他不同，需要改为`icon_name='fab fa-qq'`，这样就可以啦。

![640 (6)](C:\Users\Hu\Desktop\640 (6).png)

![640 (7)](C:\Users\Hu\Desktop\640 (7).png)

## 配色

配色是影响词云颜值的又一大问题。`stylecloud`同样找到了比较好的方案，配色方案是使用的高级调色板palettable来实现了。

palettable 网站：https://jiffyclub.github.io/palettable/

这是一款专业的配色网站，非常适合我们这种对词云的美观有一点小追求的人。

![640 (8)](C:\Users\Hu\Desktop\640 (8).png)

里面的配色方案超级多，随便点击几个给大家预览一下：

![640 (1)](C:\Users\Hu\Desktop\640 (1).gif)

我们可以通过修改参数`palette='配色方案'`来达到更改自己词云配色的目的。

```python
stylecloud.gen_stylecloud(text=' '.join(text1), collocations=False,
                          palette='tableau.BlueRed_6',
                          font_path=r'‪C:\Windows\Fonts\msyh.ttc',
                          icon_name='fab fa-qq',size=400,
                          output_name='腾讯-词云.png')
```

![640 (2)](C:\Users\Hu\Desktop\640 (2).gif)

## 其他参数

**以下参数对 stylecloud Python 函数和 CLI 均有效，你可以通过 stylecloud -h 获取这些参数的信息。**

- `text`：输入文本。最好在直接调用函数时使用。
- `file_path`：输入文本/CSV 的文件路径。最好在 CLI 上使用。
- `gradient`：梯度方向。（其默认值是 None，如果它的值不是 None，则 stylecloud 使用了方向性梯度。）[default: None]
- `size`：stylecloud 的大小（长度和宽度）。[default: 512]
- `icon_name`：stylecloud 形状的图标名称（如 fas fa-grin）。[default: fas fa-flag]
- `palette`：调色板（通过 palettable 实现）。[default: cartocolors.qualitative.Bold_6]
- `background_color`：背景颜色。[default: white]
- `max_font_size`：stylecloud 中的最大字号。[default: 200]
- `max_words`：stylecloud 可包含的最大单词数。[default: 2000]
- `stopwords`：布尔值，用于筛除常见禁用词。[default: True]
- `output_name`：stylecloud 的输出文本名。[default: stylecloud.png]
- `font_path`：stylecloud 所用字体 .ttf 文件的路径。[default: uses included Staatliches font]
- `random_state`：控制单词和颜色的随机状态。

## 参考

- <a href="https://mp.weixin.qq.com/s?__biz=MzU5MjI3NzIxMw==&mid=2247488724&idx=1&sn=1ade29812952979b86f1f8a6b45adc7e&chksm=fe236f66c954e6701e2493e0ea1838e84167e578899d0264e9912370b8d90efa9a2714f6d15e&mpshare=1&scene=1&srcid=0703bTqzCfrLvTS4USLrXgb1&sharer_sharetime=1593743893212&sharer_shareid=a49666cf2c8d2905df9b2c542be3e8aa&key=8c1e0ba910e0936a68de0d2c67347e1bf18e835da3c0cc68a19152e498eadf9abb55956ef4f43cebb32c7750e186403b9bc0450cb47bb0c23dfbcabeef3fc73aa04e12bee584a536534e61a9235736fb&ascene=1&uin=MzgxMzU5NzQ4&devicetype=Windows+10+x64&version=62090070&lang=zh_CN&exportkey=Ay2RGXIcNbtYhCckIYzKybo%3D&pass_ticket=hu5wcsiznu1YuyOkvKZnI3WgKOe%2FI26Xq1OoyixGgFGlw0apHbEmsr3WOLHCl3Ar" target="_blank">如何用一款高颜值的词云包尽情围观腾讯和老干妈的爱恨情仇？</a>  
- <a href="https://www.ershicimi.com/p/25e58abcf77e707a830fce69ccb92e51" target="_blank">stylecloud:简洁易用的词云库</a> 