**函数是指一段可以直接被另一段程序调用的程序或代码**

**1、常用的字符串函数**
```
concat(S1,S2,...,Sn)字符串拼接，将S1,S2,...,Sn拼接成一个字符串
lower(str) 将字符串str全部转换成小写
upper(str) 将字符串str全部转换成大写
lpad(str,n,pad) 左填充，用字符串pad对str的左边进行填充，达到n个字符串长度
rpad(str,n,pad) 右填充，用字符串pad对str的右边进行填充，达到n个字符串长度
trim(str) 去掉字符串头部和尾部的空格
substring(str,start,len) 返回字符串str从start位置起的len个长度的字符串
索引值是从1开始的
演示可用 select 函数(参数);
```

**2、常见的数值函数**
```
ceil(x) 向上取整
floor(x) 向下取整
mod(x,y) 返回x/y的模
rand() 返回0~1内的随机数
round(x,y) 求参数x的四舍五入值，保留y为小数
```

**3、常见的日期函数**
```
curdate() 返回当前日期
curtime() 返回当前时间
now() 返回当前日期和时间
year(date) 获取指定date的年份
month(date) 获取指定date月份
day(date) 获取只当date日期
date_add（date,interval expr type） 返回一个日期/时间值加上一个时间间隔expr后的时间值
expr 是数字
type是类型，可以是year，month，day
datediff(date1,date2) 返回起始时间date1和结束时间date2之间的天数
```

**4、流程函数**
```
流程函数也是很常用的一类函数，可以在SQL语句中实现条件筛选，从而提高语句的效率
if(value,t,f) 如果value为true，返回t，否则f
ifnull(value1,vaule2) 如果value1不为空，返回value1，否则返回value2
case when value1 then res1 ... else default end 如果value1为true，返回res1，... ，否则返回默认值default
case expr when val1 then res1 else default end 如果expr的值等于val1，返回res1，否则返回default默认值
-- 需求：查询emp表的员工姓名和工作地址（北京/上海------>一线城市，其他城市----->二线城市）
SELECT
    name,
    workaddress,
    (CASE workaddress WHEN '北京' THEN '一线城市' WHEN '上海' THEN '一线城市' ELSE '二线城市' END) '工作地址'
    FROM emp;
-- 案例：统计班级各个学员的成绩，展示的规则如下：
-- >= 85 ，展示优秀
-- >= 60 ,展示及格
-- 其他，展示不及格

SELECT
    id,
    name,
    math,
    (CASE
         WHEN math >= 85 THEN '优秀'
         WHEN (math >= 60 AND math < 85) THEN '及格'
         ELSE '不及格' END) '数学评定',
    english,
    (CASE
         WHEN english >= 85 THEN '优秀'
         WHEN english >= 60 AND english < 85 THEN '及格'
         ELSE '不及格' END) '英语评定',
    chinese,
    (CASE
         WHEN chinese >= 85 THEN '优秀'
         WHEN chinese >= 60 AND chinese < 85 THEN '及格'
         ELSE '不及格' END) '语文评定'
    FROM
        score;
case expr 要求的是等于，而case when要求的是true或false，注意区别
```