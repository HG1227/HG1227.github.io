---
layout: post
title:  Markdown中内嵌HTML表格
date:   2019-12-6
categories: HTML
tags: HTML Markdown
---
* content
{:toc}

自己在 `Markdown` 中使用内置的表格时候，不太好控制。在网上搜索了一下，`Markdown` 也可以使用 `HTML` 格式的表格，两者相比之下，选择使用 `HTML` 格式的表格 ！下面是表格的基本内容，并不完全 ！



## 表格
表格由 `<table>`  标签来定义。每个表格均有若干行（由  `<tr>`  标签定义），每行被分割为若干单元格（由 `<td>`   标签定义）。字母  td  指表格数据（table data），即数据单元格的内容。数据单元格可以包含文本、图片、列表、段落、表单、水平线、表格等等。

### 1. `table` 属性

- `border` ：设置边框，取值以 px 为单位的数值（ px 可以省略）
- `width `：设置宽度
- `height`：设置高度
- `align `：设置表格在其父元素中的水平对齐方式
- `cellpadding` : 设置单元格的内边距（内容与边框之间的距离），取值为px单位的数值
- `cellspacing` : 设置单元格的外边距（单元格与单元格之间的距离，或者单元格与表格边框之间的距离），取值像素为单位的数值
- `bgcolor` : 设置表格的背景颜色，取值可以是英文的颜色名称

### 2. `tr `标签属性

- `bgcolor` : 设置当前行的背景颜色
- `align` ：设置当前行中内容的水平对齐方式 取值 ： left / center / right
- `valign`: 设置当前行内容的垂直对齐方式 取值 ：top / middle / bottom,默认垂直居中

### 3. `td` 标签属性

- `width` 设置单元格的宽度
- `height` 设置单元格的高度
- `align` 单元格内容的水平对齐方式
- `valign`单元格内容的垂直对齐方式
- `bgcolo`r 单元格的背景颜色

示例 ： 基本的表格

源码：

```html
<table >
        <tr>
            <th rowspan="2">值班人员</th>
            <th>星期一</th>
            <th>星期二</th>
            <th>星期三</th>
        </tr>
        <tr>
            <td>李强</td>
            <td>张明</td>
            <td>王平</td>
        </tr>
 </table>
```

显示 ：

<table   >
        <tr>
            <th rowspan="2">值班人员</th>
            <th>星期一</th>
            <th>星期二</th>
            <th>星期三</th>
        </tr>
        <tr>
            <td>李强</td>
            <td>张明</td>
            <td>王平</td>
        </tr>
</table>






## 表格和边框属性

如果不定义边框属性，表格将不显示边框。有时这很有用，但是大多数时候，我们希望显示边框。

使用边框属性来显示一个带有边框的表格：

代码：

```html
<table   border="2">
        <tr>
            <th rowspan="2">值班人员</th>
            <th>星期一</th>
            <th>星期二</th>
            <th>星期三</th>
        </tr>
        <tr>
            <td>李强</td>
            <td>张明</td>
            <td>王平</td>
        </tr>
 </table>
```

<table   border="2">
        <tr>
            <th rowspan="2">值班人员</th>
            <th>星期一</th>
            <th>星期二</th>
            <th>星期三</th>
        </tr>
        <tr>
            <td>李强</td>
            <td>张明</td>
            <td>王平</td>
        </tr>

 </table>



## 表格的表头

表格的表头使用  `<th> `标签进行定义。

大多数浏览器会把表头显示为粗体居中的文本：

```html
<table border="1">
    <tr>
        <th>Heading</th>
        <th>Another Heading</th>
    </tr>
    <tr>
        <td>row 1, cell 1</td>
        <td>row 1, cell 2</td>
    </tr>
    <tr>
        <td>row 2, cell 1</td>
        <td>row 2, cell 2</td>
    </tr>
</table>
```

<table border="1">
<tr>
<th>Heading</th>
<th>Another Heading</th>
</tr>
<tr>
<td>row 1, cell 1</td>
<td>row 1, cell 2</td>
</tr>
<tr>
<td>row 2, cell 1</td>
<td>row 2, cell 2</td>
</tr>
</table>



## 表格中的空单元格

在一些浏览器中，没有内容的表格单元显示得不太好。如果某个单元格是空的（没有内容），浏览器可能无法显示出这个单元格的边框。为了避免这种情况，在空单元格中添加一个空格占位符。

使用 `&nbsp;` 处理没有内容的单元格

```
<table border="1">
    <tr>
        <td>row 1, cell 1</td>
        <td>row 1, cell 2</td>
    </tr>
    <tr>
        <td>&nbsp;</td>
        <td>row 2, cell 2</td>
    </tr>
</table>
```
<table border="1">
    <tr>
        <td>row 1, cell 1</td>
        <td>row 1, cell 2</td>
    </tr>
    <tr>
        <td>&nbsp;</td>
        <td>row 2, cell 2</td>
    </tr>
</table>



## 单元格合并

**定义和用法**

`<td>` 标签定义 HTML 表格中的标准单元格。

HTML 表格有两类单元格：
- 表头单元 - 包含头部信息（由 th 元素创建）
- 标准单元 - 包含数据（由 td 元素创建）

`colspan`  和 ` rowspan`  属性来实现内容横跨多个行或列。

**单元格的跨列合并**

- 从当前单元格的位置开始，横向向右合并几个单元格
- `colspan='3'`->跨3列进行合并（包含自身）

**单元格的跨行合并**

- 从当前的单元格开始，纵向向下合并单元格
- `rowspan='3'`-> 向下跨3行合并单元格

*注意：一旦发生单元格合并*

- 跨列合并，要删除当前行中多于的单元格
- 跨行合并，要删除其后行中多于的单元格
- 始终保持表格结构完整
  





## 关于特殊字符

`&nbsp；`表示一个空格

`&it；`表示小于号 <

`&gt；`表示大于号

`&copy；`表示版权符号 ©

`&yen；`表示人民币符号 ￥



参考：

[w3school 在线教程](https://www.w3school.com.cn/tags/tag_table.asp)

[HTML 表格](https://www.w3school.com.cn/html/html_tables.asp)





