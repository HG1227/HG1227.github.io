---
layout: post
title:  python 不同excel文件数据合并
date:   2020-08-06
categories: 小程序
tags:  openpyxl 
---
* content
{:toc}


利用 pandas 的 `merge` 和 `insert` 函数，将不同表格的文件进行匹配合并















数据表 source.csv：

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200806164131.jpg" alt="微信图片_20200806163337" style="zoom:80%;" /></center>

我们要做的是从上表中提取数据，来生成一份符合以下要求的表格：

1. 按照以下分组名单 group.xls 来整理数据表中的数据：

   <center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200806164201.png" alt="image-20200806163511894" style="zoom:80%;" /></center>

2. 最终要展现的数据项：

   <center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200806164217.png" alt="image-20200806163658802" style="zoom:80%;" /></center>

3. 其中“K数据/60”为数据表中的“数据K”/60后保留的2位小数



先看手工 Excel 如何处理以上需求：要在 source.csv 数据表中读取读取每条数据，放入 group.xls 匹配的分组成员中，最后筛选需要的数据项，再对特定的 “数据K”进行运算处理。

那么 Python 又将如何操作呢？这里我们要用到功能强大的 pandas 库。

首先导入 pandas 库，通过相关的函数读取 csv 和 xls 表格内容：

```python
import pandas as pd
import numpy as np

# 读取 group.xls 分组信息
group = pd.read_excel('group.xls',header=None)
group.columns = ['分组','角色']


# 读取 source.csv 获取所有成员数据
source = pd.read_csv('source.csv')

```

首先对 source.csv 中的数据项进行筛选，需要的数据项有“角色”、“编号”、“数据B”、“数据C”、“数据D”和“数据K”：

```python
# 通过 iloc[:,[列坐标]] 来定位需要的各列数据
filter_merge = source.iloc[:,[0,2,4,5,6,13]]
```

接下来是根据分组角色来匹配角色数据，注意到 group.xls 和 source.csv 共有“角色”一项，我们可以通过此项将两个表格融合从而形成匹配填充的效果。

```python
combine = pd.merge(group,filter_merge,on="角色")
```

在第二列插入运算后的“数据K/60”：

```python
combine.insert(1, '数据K/60', round(filter_merge['数据K']/60,2))
```

最终，将生成的数据格式写入新的 xlsx 表格中：

```python
combine.to_excel(excel_writer="result.xlsx",index=False)

```

最终自动生成的表格如下：

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200806164237.jpg" alt="微信图片_20200806164027" style="zoom:80%;" /></center>