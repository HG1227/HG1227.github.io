---
layout: post
title:  pandas_profiling 教你一行代码生成数据分析报告
date:   2020-06-29
categories: 可视化
tags: 
---
* content
{:toc}


pandas_profiling ：教你一行代码生成数据分析报告









## 分析报告全貌

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200822210050.gif" alt="v2-4c958cca326e23cdd51e2d87529cb5fd_b" style="zoom:80%;" />

## **什么是探索性数据分析**

熟悉pandas的童鞋估计都知道pandas的 `describe()` 和 `info()`函数，用来查看数据的整体情况，比如平均值、标准差之类，就是所谓的探索性数据分析-EDA。

## pandas_profiling简介

如果你想更方便快捷地了解数据的全貌，泣血推荐一个python库：`pandas_profiling`，这个库只需要一行代码就可以生成数据EDA报告。

`pandas_profiling` 基于 pandas 的 DataFrame 数据类型，可以简单快速地进行探索性数据分析。

对于数据集的每一列，`pandas_profiling`会提供以下统计信息：

1、**概要：**数据类型，唯一值，缺失值，内存大小
2、**分位数统计：**最小值、最大值、中位数、Q1、Q3、最大值，值域，四分位

3、**描述性统计：**均值、众数、标准差、绝对中位差、变异系数、峰值、偏度系数

4、**最频繁出现的值，直方图/柱状图**

5、**相关性分析可视化：**突出强相关的变量，Spearman, Pearson矩阵相关性色阶图

并且这个报告可以导出为HTML，非常方便查看。

## **pandas_profiling安装**

安装 `pandas_profiling` 可以使用pip、conda或者下载文件安装，非常方便。

我这里使用pip方式，在命令行输入：

```python
pip install pandas-profiling
```

## 使用

- 导入pandas-profiling

```python
import pandas_profiling
```

- 生成的数据报告

```python
# data是需要生成报告的数据，DataFrame类型
pandas_profiling.ProfileReport(data)
```

- 导出报告

```python
pfr = pandas_profiling.ProfileReport(data)
pfr.to_file('report.html')
```

目前**pandas-profiling**目前只支持导出html格式的文件。









参考

- <a href="https://zhuanlan.zhihu.com/p/85967505" target="_blank">pandas_profiling ：教你一行代码生成数据分析报告</a>
- <a href="https://zhuanlan.zhihu.com/p/47548106" target="_blank">使用pandas-profiling生成数据的详细报告</a>