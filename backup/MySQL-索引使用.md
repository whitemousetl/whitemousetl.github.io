**1、验证索引效率**
```
为建立索引之前，执行如下SQL语句，查看SQL耗时
select distinct major from student111 where name = 'John Doe';
针对字段创建索引
create index idx_student111_name on student111(name);
然后执行相同的SQL语句，再次查看SQL的耗时
select distinct major from student111 where name = 'John Doe';
```

**2、索引的使用原则**
```
最左前缀法则
如果索引了多列（联合索引），要遵守最左前缀法则。
最左前缀法则指的是查询从索引的最左列开始，并且不跳过索引中的列。
如果跳跃过某一列，索引将部分失效（后面的字段索引失效）。
```
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/1ffcaa88-ab29-4010-8d18-9ea286ea7b88)
```
联合索引是idx_user_pro_age_sta
索引长度为83、88、93，分别对应使用到了一个两个三个索引字段。

explain select * from tb_user where profession = '软件工程' and age =31 and status = '0';
符合最左前缀法则，ref，const，const，const，索引长度93

explain select * from tb_user where  age =31 and status = '0' and profession = '软件工程';
符合最左前缀法则，ref，const，const，const，索引长度93

explain select * from tb_user where status = '0' and profession = '软件工程';
符合最左前缀法则，ref，const，索引长度83，这也会导致索引部分失效

explain select * from tb_user where profession = '软件工程' and age =31;
符合最左前缀法则，ref，const，const，索引长度88

explain select * from tb_user where age =31 and status = '0';
不符合最左前缀法则（索引失效），all，null，null，null

explain select * from tb_user where status = '0';
不符合最左前缀法则（索引失效），all，null，null，null

explain select * from tb_user where profession = '软件工程' and status = '0';
符合最左前缀法则，但是只有profession生效，ref，const，索引长度83

```

`联合索引中，出现范围查询（>,<），范围查询右侧的列索引失效`
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/082607b0-60bf-4f9f-a834-ba20b1e7d518)
```
索引长度为83、88、93，分别对应使用到了一个两个三个索引字段。
explain select * from tb_user where profession = '软件工程' and age > 30 and status = '0';
range，null，88，用到了索引，但是范围查询右侧的字段失效了

explain select * from tb_user where profession = '软件工程' and age >= 30 and status = '0';
range，null，93，用到了索引，并且没有失效的字段
```

```
索引列运算
不要在索引列上进行运算操作，会导致索引失效
explain select * from tb_user where phone = '17799990010';
使用了索引

explain select * from tb_user where substring(phone,10,2) = '10';
没有使用索引
```

```
字符串不加引号
字符串类型字段使用时，不加引号，会导致索引失效
explain select * from tb_user where phone = 17799990010;
没有使用索引

explain select * from tb_user where phone = '17799990010';
使用索引
```

```
模糊查询
如果仅仅是尾部模糊匹配，索引不会失效
如果是头部模糊匹配，索引失效
尾部匹配是%在尾部
头部匹配是%在头部
中间匹配也不会导致索引失效，只有头部索引会导致失效
explain select * from tb_user where profession like '%工程';
索引失效

explain select * from tb_user where profession like '软%工程';
索引不失效

explain select * from tb_user where profession like '软件%';
索引不失效
```

```
or连接的条件
用or分割开的条件，如果or前的条件中的列有索引，而后面的列中没有索引，那么涉及的索引都不会被用到
```
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/fe6d1a26-e74f-4b23-b7ad-1792b72b3664)
```
age没有索引
explain select * from tb_user where id = 10 or age =23;
索引失效

explain select * from tb_user where phone = '17799990008' or age =23;
索引失效

由于age没有索引，所以即使id、phone有索引，索引也会失效。需要针对age也要建立索引。
```

```
数据分布影响
如果MySQL评估使用索引比全表更慢，则不会使用索引。
```
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/2554b122-02b7-449f-9e1e-4a45d63764cb)
```
当满足大部分数据时，MySQL会进行全表扫描，满足小部分数据时，MySQL会走索引

-- 走全表扫描，大部分满足条件
explain select * from tb_user where phone >= '17799990005';

-- 走索引，小部分满足条件
explain select * from tb_user where phone >= '17799990015';

-- 走索引，小部分满足条件
explain select * from tb_user where profession is null;

-- 走全表扫描，大部分满足条件
explain select * from tb_user where profession is not null;
```

```
SQL提示
SQL提示，是优化数据库的一个重要手段，简单来说，就是在SQL语句中加入一些人为的提示来达到优化操作的目的。
如果单字段a索引和联合索引（有这个字段a的联合索引），MySQL默认会优先使用联合索引，需要指定使用单字段a索引的时候需要使用SQL提示。
use index(建议MySQL，可能会不采纳)
-- SQL提示
create index idx_user_pro on  tb_user(profession);

-- 指定使用idx_user_pro
explain select * from tb_user use index(idx_user_pro) where profession = '软件工程';

-- 默认使用idx_user_pro_age_sta
explain select * from tb_user  where profession = '软件工程';
ignore index（忽略某索引）
explain select * from tb_user ignore index (idx_user_pro) where profession = '软件工程';
force index（强制使用某索引）
explain select * from tb_user force index (idx_user_pro) where profession = '软件工程';
```

```
覆盖索引
尽量使用覆盖索引（查询使用了索引，并且需要返回的列，在该索引中已经全部能够找到），减少select * 。
```
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/ee1cd416-e92c-4c8a-979e-e3cd3c85a2a3)
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/0c7703e5-9294-4917-bf0e-a52f10240773)
```
回表查询影响效率
二级索引上挂的id，并且本来就有联合索引中的profession、age和status，所以如果查询id，profession、age和status的话不需要回表查询
如果查询联合索引和id以外的值，那么就会需要回表查询，这样就会影响效率
```
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/f0195ee6-26ba-400b-9c36-a313625a1836)
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/7e7b0792-fbcb-4a9b-b107-079ceb735a26)
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/70d011cd-a2b9-4d52-9788-b16c6c9bf3ee)
**对username，password建立联合索引**

```
前缀索引
当字段类型为字符串(varchar,text等)时，有时候需要对长字符串建立索引，这回让索引变得很大，查询时，浪费大量的磁盘IO，影响查询效率。
此时可以只将字符串的一部分前缀，建立索引，这样可以大大节约索引空间，从而提高索引效率。
语法：
create index idx_xxx_ xxx on table_name (colunm(n));
与以前建立索引的语法有差不多，就是在字段后加上(n)
前缀长度
可以根据索引的选择性来决定，而选择性是指不重复的索引值（基数）和数据表的记录总数的比值，索引选择性越高则查询效率越高，唯一索引的选择性是1，这是最好的索引选择性，性能也是最好的。
求取选择性：
select count(distinct email)/count(*) from tb_user;

select count(distinct substring(email,1,5)) / count(*) from tb_user;
```
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/fe62669d-0743-4b16-a01f-1869d08b4b92)
**前缀索引必须要回表查询**

```
单列索引和联合索引
单列索引即一个索引只包含单个列
联合索引即一个索引包含了多个列
在业务场景中，如果存在多个查询条件，考虑针对于查询字段建立索引时，建议使用联合索引， 而非单列索引，避免回表查询
在业务场景中，如果存在多个查询条件，考虑针对于查询字段建立索引时，建议使用联合索引， 而非单列索引，避免回表查询
```

**3、索引设计原则** 
```
1、针对数据量较大，且查询比较频繁的表建立索引
2、针对于常作为查询条件（where）、排序（order by）、分组（group by）操作的字段建立索引
3、尽量选择区分度高的列作为索引，尽量建立唯一索引，区分度越高，使用的索引效率越高
4、如果是字符串类型的字段，字段的长度较长，可以针对字段的特点，建立前缀索引
5、尽量使用联合索引，减少单列索引，查询时，联合索引很多时候可以覆盖索引，节省存储空间，避免回表查询，提高查询效率
6、要控制索引的数量，索引并不是多多益善，索引越多，维护索引结构的代价也就越大，会影响增删改的效率
7、如果索引列不能存储null值，请在创建表时使用not null约束它。当优化器知道每列是否包含null值时，它可以更好地确定哪个索引最有效地用于查询
```