---
layout: post
title:  python“制作工资条”的自动化程序！
date:   2020-08-05
categories: 小程序
tags:  openpyxl 
---
* content
{:toc}








## python“制作工资条”的自动化程序！

始数据是什么样子的。

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200805152543.png" alt="image-20200805151903995" style="zoom:80%;" /></center>

那么最后做成的效果是什么样子的呢？

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200805152602.png" alt="image-20200805151918899" style="zoom:80%;" /></center>

## 代码逻辑剖析

**那么这样一个程序，是怎么写的呢？**

其实只要是`逻辑想清楚`了，剩下的就是写代码的事儿了。下面我就带着大家梳理一下，这段代码的逻辑。

首先，我们应该是`读取Excel表格`。然后需要拷贝其中一个sheet表到另外一张sheet表，并给sheet命名。`这样做的目的：`为了存放制作好工资条的那张sheet表。

```python
import re
import openpyxl
from copy import copy

wb = openpyxl.load_workbook('工资条.xlsx')
# copy_worksheet()：拷贝sheet表 
wb.copy_worksheet(wb['工资条'])
# worksheets：以列表的形式返回所有的Worksheet(表格)
ws = wb.worksheets[-1]
ws.title = 'final_工资条'
```

下面截一张图给大家，其实就可以很好的说明上述函数的含义了。

<img src=".\img\image-20200805152022414.png" alt="image-20200805152022414" style="zoom:80%;" />

接着，就需要`给每一行数据前面添加一个表头`。由于后面每一行表头的样式，都与第一行完全一模一样的，因此我们需要复制第一行表头中的样式。

```python
def cell_style(cell):
    alignment = copy(cell.alignment)    # 对齐样式
    border = copy(cell.border)          # 边框样式
    fill = copy(cell.fill)              # 填充样式
    font = copy(cell.font)              # 字体样式
    return alignment, border, fill, font
    
# 获取标题行中，每个单元格中的各种样式
alignment, border, fill, font = cell_style(cell=cells_rows[0][0])
```

`从上面的代码中可以看到：`我定义了一个函数，使用copy库中的`copy()`方法，**直接拷贝单元格的4大样式**。因为原表第一行中每个单元格的4大样式，都是完全一致的，因此我们`直接获取第一个单元格的样式即可`。

最后这一part是整个代码中`最精彩的部分`，不太好叙述，大家仔细研究一下下方的注释。

```python
for i, _ in enumerate(cells_rows[1:]):
    if i > 0:
        index = i*3
        # 每循环一次，就在对应位置下方插入2行。1行是空行，1行是表头行。
        ws.insert_rows(idx=index, amount=2)
        # 因为每次插入2行，所以需要在表头行那里，将表头及其样式写入。
        for j, v in enumerate(header):
            r, c = index+1, j+1
            cell = ws.cell(row=r, column=c)
            cell.value = v
            cell.alignment = alignment
            cell.font = font
            cell.border = border
            cell.fill = fill
            # 更新后面的公式
            if cell.coordinate[:1] in ('H', 'J'):
                cell = ws.cell(row=r+1, column=c)
                cell.value = re.sub('\d+', str(r+1), cell.value)
```

这里需要特别说明一点的就是`更新公式`。就拿第一次循环来说，我们在第3行的位置，插入了2个空白行。那么原本第3行的数据，此时就被挤到了第5行。

**注意：****它是被迫挤到第5行的**，因此这一整行是原封不动搬到第5行的，**包括它原来的公式**。原来在第3行的时候，如果公式是`SUM(E3:G3)`，被挤到到了第5行后，应该是`SUM(E5:G5)`，但是它仍然是`SUM(E3:G3)`，**因为它是被迫的**，所以需要我们修改公式，上述代码中正是使用`正则`将这个数字3改为了5。

## 完整代码

```python
import re
import openpyxl
from copy import copy

def cell_style(cell):
    alignment = copy(cell.alignment)    # 对齐样式
    border = copy(cell.border)          # 边框样式
    fill = copy(cell.fill)              # 填充样式
    font = copy(cell.font)              # 字体样式
    return alignment, border, fill, font

wb = openpyxl.load_workbook('工资条.xlsx') 
wb.copy_worksheet(wb['工资条'])
ws = wb.worksheets[-1]
ws.title = 'final_工资条'

# 获取每一列的值，拼接在一个列表中
cells_rows = [[cell for cell in row] for row in ws.rows]

# 获取标题
header = [cell.value for cell in cells_rows[0]]

# 获取标题行中，每个单元格中的各种样式
alignment, border, fill, font = cell_style(cell=cells_rows[0][0])

for i, _ in enumerate(cells_rows[1:]):
    if i > 0:
        index = i*3
        # 每读取一行，就在下方插入两行
        ws.insert_rows(idx=index, amount=2)
        # 写表头
        for j, v in enumerate(header):
            r, c = index+1, j+1
            cell = ws.cell(row=r, column=c)
            cell.value = v
            cell.alignment = alignment
            cell.font = font
            cell.border = border
            cell.fill = fill
            # 更新后面的公式
            if cell.coordinate[:1] in ('H', 'J'):
                cell = ws.cell(row=r+1, column=c)
                cell.value = re.sub('\d+', str(r+1), cell.value)
# 整个代码写完后，一定要记得保存               
wb.save('工资条.xlsx')    
```



## 参考

- 转：<a href="https://mp.weixin.qq.com/s/T1Z0yBerUIbQQ4mYHi5-4g" target="_blank">数据分析与统计学之美</a> 

