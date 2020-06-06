---
layout: post
title:  MySQL GROUP_CONCAT 函数详解
date:   2020-03-21
categories: MySQL
tags:  MySQL
---
* content
{:toc}
## `GROUP_CONCAT` 函数

`GROUP_CONCAT(expr) `函数会从 expr 中连接所有非 NULL 的字符串。如果没有非 NULL 的字符串，那么它就会返回 NULL。

MySQL 的 GROUP_CONCAT 函数详解



```sql
group_concat([DISTINCT] 要连接的字段(可以是多个) 
             [Order BY ASC/DESC 排序字段] 
             [Separator '分隔符'])
```

Separator 是一个字符串值，它被用于插入到结果值中。缺省为一个逗号 (",")，可以通过指定 SEPARATOR "" 完全地移除这个分隔符。





### 1 使用示例

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200603220119.png"/></center>
```sql
select GROUP_CONCAT(c_id) id
from score
where s_id = '01';
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200603220202.png"/></center>


【2】可以使用 `DISTINCT` 过滤重复的值，也可以加入 `ORDER BY` 对值进行排序，还可以使用 `SEPARATOR` 指定分隔符：

```sql
select GROUP_CONCAT(c_id separator ' ') id
from score
where s_id = '01';
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200603220631.png"/></center>
如果将多个字段进行连接，会首先将这几个字段连接，然后再用指定的分隔符连接前面拼接好的字符串

```sql
select GROUP_CONCAT(c_id,s_id separator '-') id
from score
where s_id = '01';
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200603221810.png"/></center>


### 2 最大值限制

`GROUP_CONCAT() `是有最大长度限制的，默认值是 1024。

可以通过 `group_concat_max_len` 参数进行动态设置。参数范围可以是 Global 或 Session。

设置语法如下：

```sql
SET [GLOBAL |SESSION] group_concat_max_len= val
```

示例

```sql
SET SESSION group_concat_max_len=18446744073709551615;
SELECT GROUP_CONCAT(a.REGION_ID) FROM t_region a;
```





## `CONCAT()`函数

CONCAT（）函数用于将多个字符串连接成一个字符串。
使用数据表Info作为示例，其中SELECT id,name FROM info LIMIT 1;的返回结果为

```sql
+----+--------+
| id | name   |
+----+--------+
|  1 | BioCyc |
+----+--------+
```

1、语法及使用特点：

```sql
CONCAT(str1,str2,…)
```



返回结果为连接参数产生的字符串。**如有任何一个参数为NULL ，则返回值为 NULL**。可以有一个或多个参数。

2、使用示例：
`SELECT CONCAT(id, ‘，’, name) AS con FROM info LIMIT 1;`返回结果为

```sql
+----------+
| con      |
+----------+
| 1,BioCyc |
+----------+
```

`SELECT CONCAT(‘My’, NULL, ‘QL’);` 返回结果为

```sql
+--------------------------+
| CONCAT('My', NULL, 'QL') |
+--------------------------+
| NULL                     |
+--------------------------+
```



3、如何指定参数之间的分隔符

## `CONCAT_WS() `函数

使用函数`CONCAT_WS()`。使用语法为：

```sql
CONCAT_WS(separator,str1,str2,…)
```



`CONCAT_WS() `代表 CONCAT With Separator ，是CONCAT()的特殊形式。

第一个参数是其它参数的分隔符。分隔符的位置放在要连接的两个字符串之间。分隔符可以是一个字符串，也可以是其它参数。**如果分隔符为 NULL，则结果为 NULL**。函数会忽略任何分隔符参数后的 NULL 值。**但是`CONCAT_WS()`不会忽略任何空字符串。** (然而会忽略所有的 NULL）。

```sql
select concat_ws('-',c_id,s_id)
from score
where s_id='01';
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200603222312.png"/></center>


## 参考

- <a href="https://segmentfault.com/a/1190000004844113" target="_blank">mysql中函数CONCAT及GROUP_CONCAT的使用</a>
- <a href="https://www.jianshu.com/p/447eb01eebb2" target="_blank">MySQL 的 GROUP_CONCAT 函数详解</a>