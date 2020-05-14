---
layout: post
title:  Python数据可视化 词云图
date:   2020-4-23
categories: Python
tags:  词云 
---
* content
{:toc}
wordcloud`库，可以说是 python 非常优秀的词云展示第三方库。词云以词语为基本单位更加直观和艺术的展示文本 词云图，也叫文字云，是对文本中出现频率较高的“关键词”予以视觉化的展现，词云图过滤掉大量的低频低质的文本信息，使得浏览者只要一眼扫过文本就可领略文本的主旨











## Python数据可视化 -- Wordclod

## 安装

```python
# 启动命令行，输入：
pip install wordcloud  
```

## 快速生成词云

```python
from wordcloud import WordCloud
import matplotlib.pyplot as plt
import re

with open('constitution.txt') as c:
    # 抽取文本中的英文部分并小写化，并将空格作为分隔拼接为长字符串
    text = ' '.join([word.group().lower() for word in re.finditer('[a-zA-Z]+',c.read())])

# 从文本中生成词云
wordcloud = WordCloud(background_color='white',  # 背景色为白色
                      height=400,  # 高度设置为400
                      width=800,  # 宽度设置为800
                      scale=20,   # 长宽拉伸程度设置为20
                      prefer_horizontal=0.9999).generate(text)
plt.figure(figsize=(8, 4))
plt.imshow(wordcloud)
plt.axis('off')
plt.savefig('图6.jpg', dpi=600, bbox_inches='tight', quality=95)
plt.show()
```

<center>
<img   src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514152303.jpg"  height="80%" width="80%">
</center>

`wordcloud`库为每一个词云生成一个`WordCloud`对象（注意，此处的W和C是大写）

也就是说，`wordcloud.WordCloud()`代表一个词云对象

`WordCloud()`括号里填入各种参数，控制词云的字体、字号、字的颜色、背景颜色等等。

`wordcloud` 库会非常智能地按空格进行分词及词频统计，出现次数多的词就大

## 常用参数

`wordcloud.WordCloud()` 词云参数

- `width`  词云图片宽度，默认400像素

- `height`  词云图片高度 默认200像素

- `background_color`  词云图片的背景颜色，默认为黑色

  `background_color='white'`

- `font_step` 字号增大的步进间隔 默认1号

- font_path 指定字体路径 默认None，对于中文可`font_path='msyh.ttc'`

- `mini_font_size` 最小字号 默认4号

- `max_font_size`  最大字号 根据高度自动调节

- `max_words` 最大词数 默认200

- `stop_words` 不显示的单词 `stop_words={"python","java"}`

- `Scale`  默认值1。值越大，图像密度越大越清晰

- `prefer_horizontal`：默认值0.90，浮点数类型。表示在水平如果不合适，就旋转为垂直方向，水平放置的词数占0.9？

- `relative_scaling`：默认值0.5，浮点型。设定按词频倒序排列，上一个词相对下一位词的大小倍数。有如下取值：“0”表示大小标准只参考频率排名，“1”如果词频是2倍，大小也是2倍

- `contour_width` 和 `contour_color` 设置轮廓宽度和颜色
  
- `mask ` 指定词云形状图片，默认为矩形

  通过以下代码读入外部词云形状图片（需要先`pip install imageio`安装imageio）

## 绘制指定形状的词云

方式一 ： 借助 `PIL`  `numpy` 模块导入图片蒙版

```python
from PIL import Image
import numpy as np
usa_mask = np.array(Image.open('美国本土地图蒙版.png'))

# 从文本中生成词云
wordcloud = WordCloud(background_color='white',
                      height=4000,
                      width=8000,
                      scale=20,
                      prefer_horizontal=0.9999,
                      mask=usa_mask).generate(text)
plt.figure(figsize=(8, 4))
plt.imshow(wordcloud)
plt.axis('off')
# 保存到本地
plt.savefig('图8.jpg', dpi=600, bbox_inches='tight', quality=95)
plt.show()
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514153822.jpg" height="80%" width="80%"></center>
方式二 ： 借助 `imageio` 模块 导入图片蒙版

```python
import imageio


usa_mask = imageio.imread('美国本土地图蒙版.png')
```

### 勾勒轮廓线及颜色

```python
with open('constitution.txt') as c:
    '''抽取文本中的英文部分并小写化，并将空格作为分隔拼接为长字符串'''
    tt = ' '.join([word.group().lower() for word in re.finditer('[a-zA-Z]+', c.read())])


mk = imageio.imread('美国本土地图蒙版.png')

wordcloud = WordCloud(background_color='white', # 背景色为白色
                      height=4000, # 高度设置为400
                      width=8000, # 宽度设置为800
                      scale=20, # 长宽拉伸程度程度设置为20
                      prefer_horizontal=0.9999,
                      contour_width=5, # 轮廓线的宽度
                      contour_color='steelblue',  #轮廓线的颜色
                      mask=mk # 添加蒙版
                     ).generate(tt)
plt.figure(figsize=[8, 4])
plt.imshow(wordcloud)
plt.axis('off')
plt.show()
```



<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514155751.jpg" height="80%" width="80%"></center> 
效果不太明显

### 按模板填色

```python
from PIL import Image
import numpy as np
from wordcloud import ImageColorGenerator

usa_mask = np.array(Image.open('美国地图蒙版_星条旗色.png'))
image_colors = ImageColorGenerator(usa_mask)

'''从文本中生成词云图'''
wordcloud = WordCloud(background_color='white', # 背景色为白色
                      height=400, # 高度设置为400
                      width=800, # 宽度设置为800
                      scale=20, # 长宽拉伸程度程度设置为20
                      prefer_horizontal=0.2, # 调整水平显示倾向程度为0.2
                      mask=usa_mask, # 添加蒙版
                      max_words=1000, # 设置最大显示字数为1000
                      relative_scaling=0.3, # 设置字体大小与词频的关联程度为0.3
                      max_font_size=80 # 缩小最大字体为80
                     ).generate(text)

plt.figure(figsize=[8, 4])
plt.imshow(wordcloud.recolor(color_func=image_colors), alpha=1)
plt.axis('off')
plt.show()
```



<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514162051.jpg" height="80%" width="80%"></center> 


## 中文分词 `jieba` 

中文分词第三方模块 `jieba` 

安装 `pip install jieba` 

```python
>>> import jieba
>>> textlist = jieba.lcut('动力学和电磁学')
>>> textlist
# ['动力学', '和', '电磁学']
>>> string = " ".join(textlist)
>>> string
# '动力学 和 电磁学'
```

以上代码将一句`完整的中文字符串`转换成了`以空格分隔的词组成的字符串`，而后者是绘制词云时`generate()`方法要求传入的参数。



### 中文分词库`jieba`的常用方法

- **确模式（最常用，只会这个就行）**：每个字只用一遍，不存在冗余词汇。 `jieba.cut('动力学和电磁学')`
- **全模式**：把每个字可能形成的词汇都提取出来，存在冗余。 `jieba.cut('动力学和电磁学',cut_all=True)` 
- **搜索引擎模式**：将全模式分词的结果从短到长排列好 `jieba.cut_for_search('动力学和电磁学')` 


以下命令演示了三种分词模式及结果，精确模式是最常用的。

```python
import jieba

seg_list = jieba.cut("我来到北京清华大学", cut_all=True, HMM=False)
print("Full Mode: " + "/ ".join(seg_list))  # 全模式
# Full Mode: 我/ 来到/ 北京/ 清华/ 清华大学/ 华大/ 大学


seg_list = jieba.cut("我来到北京清华大学", cut_all=False, HMM=True)
print("Default Mode: " + "/ ".join(seg_list))  # 默认模式
# Default Mode: 我/ 来到/ 北京/ 清华大学

seg_list = jieba.cut("他来到了网易杭研大厦", HMM=False)
print(", ".join(seg_list))
# 他, 来到, 了, 网易, 杭, 研, 大厦

seg_list = jieba.cut_for_search("小明硕士毕业于中国科学院计算所，后在日本京都大学深造", HMM=False)  # 搜索引擎模式
print(", ".join(seg_list))
# 小, 明, 硕士, 毕业, 于, 中国, 科学, 学院, 科学院, 中国科学院, 计算, 计算所, ，, 后, 在, 日本, 京都, 大学, 日本京都大学, 深造

# jieba.cut的默认参数只有三个,jieba源码如下
# cut(self, sentence, cut_all=False, HMM=True)
# 分别为:输入文本 是否为全模式分词 与是否开启HMM进行中文分词
```



```
import jieba
import wordcloud
# 构建并配置词云对象w
w = wordcloud.WordCloud(width=1000,
                        height=700,
                        background_color='white',
                        font_path='msyh.ttc')

# 调用jieba的lcut()方法对原始文本进行中文分词，得到string
txt = '南京师范大学（Nanjing Normal University），简称南京师大，坐落于六朝古都南京市，由江苏省人民政府和中华人民共和国教育部共建，是首批国家“211工程”重点建设高校、世界一流学科建设高校'
txtlist = jieba.lcut(txt)
string = " ".join(txtlist)

# 将string变量传入w的generate()方法，给词云输入文字
w.generate(string)

# 将词云图片导出到当前文件夹
w.to_file('output4-tongji.png')
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514163920.png" height="80%" width="80%"></center> 
### 停用词的使用

```python
import pandas as pd
import jieba 
import re
from PIL import Image
import numpy as np
from wordcloud import ImageColorGenerator

# 读入数据
raw_comments = pd.read_csv('waimai_10k.csv')

# 导入停词用表
with open('stopwords.txt') as s:
    stopwords = set([line.replace('\n', ' ') for line in s])

# 传入apply的预处理函数，完成中文提取、分词以及多余空格剔除
def preprocessing(c):
    c = [word for word in jieba.cut(' '.join(re.findall('[\u4e00-\u9fa5]+', c))) \
         if word != ' ' and word not in stopwords]
    return ' '.join(c)

# 将所有语料按空格拼接为一整段文字
comments = ' '.join(raw_comments['review'].apply(preprocessing))


waimai_mask = np.array(Image.open('美团外卖logo蒙版.png'))
image_colors = ImageColorGenerator(waimai_mask)

'''从文本中生成词云图'''
wordcloud = WordCloud(font_path='SimHei.ttf', # 定义SimHei字体文件,防止中文乱码
                      background_color='white', # 背景色为白色
                      height=400, # 高度设置为400
                      width=800, # 宽度设置为800
                      scale=20, # 长宽拉伸程度程度设置为20
                      prefer_horizontal=0.2, # 调整水平显示倾向程度为0.2
                      mask=waimai_mask, # 添加蒙版
                      max_words=1000, # 设置最大显示字数为1000
                      relative_scaling=0.3, # 设置字体大小与词频的关联程度为0.3
                      max_font_size=80 # 缩小最大字体为80
                     ).generate(comments)

plt.figure(figsize=[8, 4])
plt.imshow(wordcloud.recolor(color_func=image_colors), alpha=1)
plt.axis('off')
plt.show()
```
<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514165209.jpg" height="80%" width="80%"></center>

## Python数据可视化 -- stylecloud

制作词云图

```python
stylecloud.gen_stylecloud(file_path='constitution.txt',
                          icon_name='fas fa-dog',
                          palette='colorbrewer.diverging.Spectral_11',
                          background_color='black',
                          gradient='horizontal')
```

参数：

- `text`：输入文本。最好在直接调用函数时使用。
- `file_path`：输入文本/CSV 的文件路径。最好在 CLI 上使用。
- `gradient`：梯度方向。（其默认值是 None，如果它的值不是 None，则 stylecloud 使用了方向性梯度。）[default: None]
- `size`：stylecloud 的大小（长度和宽度）。[default: 512]
- `icon_name`：stylecloud 形状的图标名称（如 fas fa-grin）。[default: fas fa-flag] <a href="https://fontawesome.com/icons?d=gallery&m=free" blank="">Font Awesome</a> 
- `palette`：调色板（通过 palettable 实现）。[default: cartocolors.qualitative.Bold_6]  <a href="https://jiffyclub.github.io/palettable/" blank="">Palettable</a>  
  示例 `palette='cartocolors.diverging.ArmyRose_2'` 
- `background_color`：背景颜色。[default: white]
- `max_font_size`：stylecloud 中的最大字号。[default: 200]
- `max_words`：stylecloud 可包含的最大单词数。[default: 2000]
- `stopwords`：布尔值，用于筛除常见禁用词。[default: True]
- `output_name`：stylecloud 的输出文本名。[default: stylecloud.png]
- `font_path`：stylecloud 所用字体 .ttf 文件的路径。[default: uses included Staatliches font]
- `random_state`：控制单词和颜色的随机状态。
- `colors` : 颜色列表，可以自己指定使用的颜色
  `colors=['#ecf0f1', '#3498db', '#e74c3c']`

> `max_font_size` 的默认值 200 与 size 的默认值 512 呈正相关，如要增加 `size`，你还需要考虑增加 `max_font_size` 的值。

生成优秀 stylecloud 需要的完美字体是：加粗/高字重，以提高可读性；紧凑/低间距，以容纳更多文本。

### 绘制英文词云图

```python
import stylecloud
from IPython.display import Image # 用于在jupyter lab中显示本地图片

'''生成词云图'''
stylecloud.gen_stylecloud(text=text, 
                          size=512,
                          output_name='图17.png')

'''显示本地图片'''
Image(filename='图17.png') 
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514165600.png" height="80%" width="80%"></center



```python
'''生成词云图'''
stylecloud.gen_stylecloud(text=text, 
                          size=1024,
                          output_name='图18.png',
                          palette='scientific.diverging.Broc_3', # 设置配色方案
                          icon_name='fas fa-bomb' # 设置图标样式
                         )

'''显示本地图片'''
Image(filename='图18.png') 
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514165639.png" height="80%" width="80%"></center


### 绘制中文词云图

```python
weibo = pd.read_csv('weibo_senti_100k.csv')
weibo_text = [word for word in jieba.cut(' '.join(re.findall('[\u4e00-\u9fa5]+', ' '.join(weibo['review'].tolist())))) if word != ' ' and word not in stopwords]
'''生成词云图'''
stylecloud.gen_stylecloud(text=' '.join(weibo_text), 
                          size=1024,
                          output_name='图20.png',
                          palette='colorbrewer.sequential.Reds_3', # 设置配色方案为https://jiffyclub.github.io/palettable/colorbrewer/sequential/#reds_3
                          icon_name='fab fa-weibo', # 设置图标样式
                          gradient='horizontal', # 设置颜色渐变方向为水平
                          font_path='SimHei.ttf',
                          collocations=False
                         )

'''显示本地图片'''
Image(filename='图20.png') 
```
<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514165818.png" height="80%" width="80%"></center


## 参考

1. <a href="https://www.cnblogs.com/wkfvawl/p/11585986.html" blank="">Python 词云可视化</a> 
2. <a href="https://blog.csdn.net/FontThrone/article/details/72782499" blank="">Python中文分词 jieba 十五分钟入门与进阶</a>  
3. <a href="https://www.jiqizhixin.com/articles/2019-12-23-6" blank="">更改形状和背景色、自定义风格、颜色流动…这款词云工具都能做到</a>    
4. <a href="https://www.ctolib.com/minimaxir-stylecloud.html" blank="">生成多种风格词云的Python软件包+ CLI，包括渐变和图标形状！</a>     