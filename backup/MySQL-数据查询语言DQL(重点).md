**DQL （Data Query Language）
数据查询语言：用来对数据库表进行查询**

1、DQL-语法

```
select 
           字段列表
from 
            表名列表
where
            条件列表
group by
            分组字段列表
having
            分组后条件列表
order by
            排序字段列表
limit
            分页参数
```

2、DQL-基本查询
- 查询多个字段
`select 字段1，字段2，字段3，... from 表名；`
- 查询全部字段
`select * from 表名；`
- 设置别名
`select 字段1 [as 别名1] ，字段2 [as 别名2] ... from 表名；`
- 去掉重复记录
`select distinct 字段列表 from 表名`

3、DQL-条件查询
```
比较运算符
> 大于
>= 大于等于
< 小于
<= 小于等于
= 等于
<> 或 != 不等于
between ... and ... 在某个范围之内（含最小最大值）
in (...) 在in之后的列表中的值多选一
like 占位符 模糊匹配( _ 匹配单个字符，%匹配任意个字符)
is null 是null
```
```
逻辑运算符
and 或 &&         并且（多个条件同时成立）
or 或 ||                或者（多个条件任意一个成立）
not 或 !               非，不是
```

4、DQL-集合函数
聚合函数是将一列数据作为一个整体，进行纵向计算
注意：所有的null都不参与聚合函数运算
```
常见的聚合函数
count          统计数量
max             最大值
min              最小值
avg              平均值
sum             总和
```
`语法：select 聚合函数（字段列表） from 表名；`

5、DQL-分组查询
分组函数一般配合聚合函数使用

`select 字段列表 from 表名 [where 条件] group by 分组字段名 [having 分组后过滤条件]`

where 和 having 的区别
- 执行时机不同，where是分组之前进行过滤，不满足where条件，不参与分组；而having是分组之后对结果进行过滤
- 判断条件不同，where不能对聚合函数进行判断，而having可以

注意：
- 执行顺序：where > 聚合函数 > having
- 分组之后，查询的字段一般为聚合函数和分组字段，查询其他字段无任何意义

6、DQL-排序查询
`语法：select 字段列表 from 表名 order by 字段1 排序方式1，字段2 排序方式2；`
排序方式：
ASC ：升序（默认值）
DESC： 降序
如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序

DQL-分页查询
`语法：select 字段列表 from 表名 limit 起始索引，查询记录数；`
注意：
1、起始索引从0开始，起始索引=（查询页码-1）*每页显示记录数
2、分页查询是数据库的方言，不同数据库有不同实现，MySQL中是limit
3、如果查询的是第一页的数据，起始索引可以省略，如：limit 10 是第一页的10条记录

DQL-执行顺序
语法顺序：
```
select 
           字段列表
from 
            表名列表
where
            条件列表
group by
            分组字段列表
having
            分组后条件列表
order by
            排序字段列表
limit
            分页参数
```
`执行顺序：from > where > group by > select > order by > limit `
