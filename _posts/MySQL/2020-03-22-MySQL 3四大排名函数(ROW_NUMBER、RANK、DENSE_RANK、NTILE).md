---
layout: post
title:  MySQL 四大排名函数ROW_NUMBER、RANK、DENSE_RANK、NTILE
date:   2020-03-22
categories: MySQL
tags:  MySQL
---
* content
{:toc}
Sql四大排名函数(ROW_NUMBER、RANK、DENSE_RANK、NTILE)







创建数据表：

```sql
CREATE TABLE rk
(
    ID         int  NOT NULL,
    UserId     int      NOT NULL,
    TotalPrice int      NOT NULL,
    SubTime    datetime NOT NULL
);

insert into rk values (1, 1, 100, '2015-01-07 17:18:22.450'),
                        (2, 2, 500, '2015-01-07 17:18:34.433'),
                        (3, 3, 300, '2015-01-07 17:18:39.150'),
                        (4, 2, 1000, '2015-01-07 17:18:43.580'),
                        (5, 1, 520, '2015-01-07 17:18:48.277'),
                        (6, 2, 2000, '2015-01-07 17:22:26.590');
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200602212356.png"/></center>
## 一、RANK

`rank`函数用于返回结果集的分区内每行的排名， 行的排名是相关行之前的排名数加一。

简单来说 `rank` 函数就是对查询出来的记录进行排名，与 `row_number` 函数不同的是，`rank` 函数考虑到了`over` 子句中排序字段值相同的情况，如果使用rank函数来生成序号，over子句中排序字段值相同的序号是一样的，后面字段值不相同的序号将跳过相同的排名号排下一个，也就是相关行之前的排名数加一，可以理解为根据当前的记录数生成序号，后面的记录依此类推。

```sql
select  *, rank() over (order by UserId) rankk
from rk;
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200602214007.png"/></center>

由上图可以看出，`rank`函数在进行排名时，同一组的序号是一样的，而后面的则是根据当前的记录数依次类推，图中第一、二条记录的用户Id相同，所以他们的序号是一样的，第三条记录的序号则是3。　

## 二、DENSE_RANK

`dense_rank`函数的功能与 `rank` 函数类似，`dense_rank` 函数在生成序号时是连续的，而`rank` 函数生成的序号有可能不连续。`dense_rank` 函数出现相同排名时，将不跳过相同排名号，`rank`值紧接上一次的rank值。在各个分组内，rank()是跳跃排序，有两个第一名时接下来就是第四名，`dense_rank()`是连续排序，有两个第一名时仍然跟着第二名。

```sql
select *, dense_rank() over (order by UserId) dk
from rk;
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200602214329.png"/></center>

图中第一、二条记录的用户Id相同，所以他们的序号是一样的，第三条记录的序号紧接上一个的序号，所以为2不为3，后面的依此类推

## 三、ROW_NUMBER

`row_number` 的用途的非常广泛，排序最好用他，一般可以用来实现web程序的分页，他会为查询出来的每一行记录生成一个序号，依次排序且不会重复，注意使用`row_number` 函数时必须要用`over` 子句选择对某一列进行排序才能生成序号。row_number用法实例:

```sql
select * ,row_number() over (order by SubTime desc ) row_num 
from rk;
```

查询结果如下图所示：

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200602212937.png"/></center>
图中的 row_num 列就是 `row_number` 函数生成的序号列，其基本原理是先使用`over`子句中的排序语句对记录进行排序，然后按照这个顺序生成序号。over子句中的`order by`子句与SQL语句中的`order by`子句没有任何关系，这两处的`order by `可以完全不同，如以下sql，over子句中根据SubTime降序排列，Sql语句中则按TotalPrice降序排列。

```sql
select * ,row_number() over (order by SubTime desc ) row_num
from rk
order by TotalPrice desc ;
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200602213404.png"/></center>
两次执行得到的结果不同主要是语句的执行顺序问题，row_number 所对应的行的数据是一样的。



## 四、NTILE

`ntile` 函数可以对序号进行分组处理，将有序分区中的行分发到指定数目的组中。 各个组有编号，编号从一开始。 对于每一个行，`ntile` 将返回此行所属的组的编号。这就相当于将查询出来的记录集放到指定长度的数组中，每一个数组元素存放一定数量的记录。`ntile` 函数为每条记录生成的序号就是这条记录所有的数组元素的索引（从1开始）。也可以将每一个分配记录的数组元素称为“桶”。`ntile`函数有一个参数，用来指定桶数。

```sql
select *, ntile(4) over (order by SubTime desc ) nt
from rk;
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200602215051.png"/></center>
表的总记录数是6条，而上面的Sql语句ntile函数指定的组数是4，那么Sql Server2005是怎么来决定每一组应该分多少条记录呢？这里我们就需要了解ntile函数的分组依据（约定）。

### `ntile`函数的分组依据（约定）

　　**1、每组的记录数不能大于它上一组的记录数，即编号小的桶放的记录数不能小于编号大的桶。 ** **也就是说，第1组中的记录数只能大于等于第2组及以后各组中的记录数。**

　　**2、所有组中的记录数要么都相同，要么从某一个记录较少的组（命名为X）开始后面所有组的记录数都与该组（X组）的记录数相同。也就是说，如果有个组，前三组的记录数都是9，而第四组的记录数是8，那么第五组和第六组的记录数也必须是8。**

　　这里对约定2进行详细说明一下，以便于更好的理解。

　　首先系统会去检查能不能对所有满足条件的记录进行平均分组，若能则直接平均分配就完成分组了；若不能，则会先分出一个组，这个组分多少条记录呢？就是 （总记录数/总组数）+1 条，之所以分配 （总记录数/总组数）+1 条是因为当不能进行平均分组时，总记录数%总组数肯定是有余的，又因为分组约定1，所以先分出去的组需要+1条。

　　分完之后系统会继续去比较余下的记录数和未分配的组数能不能进行平均分配，若能，则平均分配余下的记录；若不能，则再分出去一组，这个组的记录数也是（总记录数/总组数）+1条。

　　然后系统继续去比较余下的记录数和未分配的组数能不能进行平均分配，若能，则平均分配余下的记录；若还是不能，则再分配出去一组，继续比较余下的......这样一直进行下去，直至分组完成。

　　举个例子，将51条记录分配成5组，51%5==1不能平均分配，则先分出去一组（51/5）+1=11条记录，然后比较余下的 51-11=40 条记录能否平均分配给未分配的4组，能平均分配，则剩下的4组，每组各40/4=10 条记录，分配完成，分配结果为：11，10，10，10，10，

验证

```sql
select nt,count(ID) recordCount
from (
     select *, ntile(4) over (order by SubTime desc) nt
    from rk
         ) as t
group by t.nt;
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200602215758.png"/></center>


## 五、rank, dense_rank, row_number有什么区别呢？

原始表：

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200817142335.png" alt="df106cff81cd06569e1e616cde5f69a693d646b2e2fb4ed06fcd3bfe8faa903d-1" width="60%" height="60%" /></center>



```mysql
select *,
   rank() over (order by 成绩 desc) as ranking,
   dense_rank() over (order by 成绩 desc) as dese_rank,
   row_number() over (order by 成绩 desc) as row_num
from 班级;
```

得到结果：

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200817142503.png" alt="07f68cabafcde24758904c92ed7ce5f614562d9ffa4885348463dac99c04cd26-1" width="60%" height="60%"/></center>

从上面的结果可以看出：
1)rank函数：这个例子中是5位，5位，5位，8位，也就是如果有并列名次的行，会占用下一名次的位置。比如正常排名是1，2，3，4，但是现在前3名是并列的名次，结果是：1，1，1，4。

2)dense_rank函数：这个例子中是5位，5位，5位，6位，也就是如果有并列名次的行，不占用下一名次的位置。比如正常排名是1，2，3，4，但是现在前3名是并列的名次，结果是：1，1，1，2。

3)row_number函数：这个例子中是5位，6位，7位，8位，也就是不考虑并列名次的情况。比如前3名是并列的名次，排名是正常的1，2，3，4。

这三个函数的区别如下：

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200817142550.png" alt="d6f89b608476612c0e70ebc9c2ce521f29342be6d466270bd4e13827c37dc2bd-1" width="60%" height="60%" /></center>

## 六、总结

在使用排名函数的时候需要注意以下三点：

　　1、排名函数必须有 OVER 子句。

　　2、排名函数必须有包含 ORDER BY 的 OVER 子句。

　　3、分组内从1开始排序。



参考

- <a href="https://www.cnblogs.com/52xf/p/4209211.html" target="_blank">Sql 四大排名函数（ROW_NUMBER、RANK、DENSE_RANK、NTILE）简介</a> 