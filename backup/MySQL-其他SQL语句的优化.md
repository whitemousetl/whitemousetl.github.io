**1、插入数据优化**
```
insert优化
批量插入
1 insert into 表名(字段列表) values(1,'Tom'),(2,'Cat'),(3,'Jerry')...;
2 不建议批量插入超过1000条，可以开启手动提交事务
start transaction
insert into 表名(字段列表) values(1,'Tom'),(2,'Cat'),(3,'Jerry')...;
insert into 表名(字段列表) values(4,'Tom'),(5,'Cat'),(6,'Jerry')...;
insert into 表名(字段列表) values(7,'Tom'),(8,'Cat'),(9,'Jerry')...;
...
commit;主键顺序插入
3 顺序插入的性能高于乱序插入
```
```
大批量插入数据
不建议insert
使用load指令
如果一次性要插入大批量数据，使用insert语句插入性能较低，此时可以使用MySQL数据库提供的load指令进行插入。操作如下：
1、客户端连接服务端时，加上参数 --local-infile
mysql --local-infile -u root -p

2、设置全局参数local-infile为1，开启从本地加载文件导入数据的开关
set global local-infile=1;
可以使用:select @@local_infile来查看local_infile是否开启

3、执行load指令将准备好的数据，加载到表结构中
load data local infile '/root/sql1.log' into table tb_user fields terminated by ',' lines terminated by '\n';
注意：
1、.sql格式的文件可以通过记事本创建，把后缀改成.sql。
2、load 指令尽量输入所有字段，包括id，减少warnings
3、需要添加序号可以在notepad++的 编辑->列块编辑 中插入数字来解决（初始值1，增量1，十进制）
4、字符串不需要引号 '' 包围，去掉 ''
5、巧用替换，使得.sql文件满足格式需求
```
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/754fe0d8-4b15-4148-ae9c-8699bd749c2c)

**2、主键优化**
数据组织方式
在InnoDB中存储引擎中，表数据都是根据主键顺序组织存放的，这种存储方式的表称为索引组织表（index organized table IOT）
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/00214fad-c222-4e8e-95b7-f88855ae55fe)
InnoDB表数据都是根据主键顺序组织存放的
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/6eec6af2-adaf-4089-ab64-2ff152c56cd3)
一页是16k

页分裂
页可以为空，也可以填充一半，也可以填充100%。每个页包含了2-N行数据（如果一行数据太大，会行溢出），根据主键排列。
当乱序插入时，会可能发生页分裂现象
页合并
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/80fc8622-def4-4bcd-b251-2067a6376224)
当删除一行记录时，实际上记录并没有被物理删除，只是记录被标记（flaged）为删除并它的空间允许被其他记录声明使用。

当页中删除的记录达到merge_threshold(默认为页的50%)，InnoDB会开始寻找最靠近的页（前或后）看看是否可以将两个页合并以优化空间使用。

```
主键设计原则
满足业务需求的情况下，尽量降低主键的长度
插入数据时，尽量选择顺序插入，选择使用auto_increment自增主键
尽量不要使用uuid做主键或者是其他自然主键，如身份证号
业务操作时，尽量避免对主键的修改
```

**3、order by优化**
```
1、using filesort
通过表的索引或全表扫描，读取满足条件的数据行，然后在排序缓冲区sort buffer中完成排序操作，所有不是通过索引直接返回排序结果的排序都叫filesort排序
2、using index 通过有序索引顺序扫描直接返回有序数据，这种情况即为using index ，不需要额外排序，操作效率高
3、当创建索引的时候可以指定字段的排列顺序
如：create index idx_user_age_phone_ad on user(age asc,phone desc)
那样select id,age,phone from user order by age asc,phone desc;的查询效率是最高的。
优化原则
根据排序字段建立合适的索引，多字段排序时，页遵循最左前缀法则
尽量使用覆盖索引
多字段排序，一个升序一个降序，此时需要注意联合索引在创建时的规则（asc/desc)
如果不可避免地出现filesort，大数据量排序时，可以适当增大排序缓冲区大小，sort_buffer_size(默认256k）
```

**4、group by优化**
```
主要是联合索引和满足最左前缀法则
在分组操作时，也可以通过索引来提高效率
分组操作时，索引的使用也需要满足最左前缀法则
```

**5、limit优化**
```
一个常见又头疼的问题就是limit 2000000，10 ，此时需要MySQL排序前2000010记录，仅仅返回2000000 - 2000010 的记录，其他记录丢弃，查询的代价非常大，效率也低
一般分页查询时，通过创建覆盖索引能够比较好地提高性能，可以通过覆盖索引加子查询形式进行优化
通过覆盖索引加子查询的方式对limit进行优化，这个例子是通过表的内连接来优化
select * from student111 limit 9000000,10;
耗时 4.40秒

select id from student111 order by id limit 9000000,10;
耗时2.79秒

select * from student111 where id in (select id from student111 order by id limit 9000000,10);
ERROR 1235 (42000): This version of MySQL doesn't yet support 'LIMIT & IN/ALL/ANY/SOME subquery'

select * from student111 s ,(select id from student111 order by id limit 9000000,10) a where s.id = a.id ;
耗时2.77秒

通过覆盖索引和子查询可以提高limit的查询效率
```

**6、count优化**
```
MyISAM引擎把一个表的总行数存在了磁盘上，因此执行count(*)的时候会直接返回这个数，效率很高
InnoDB引擎比较麻烦，它执行count(*)时，需要把数据一行一行地从引擎里面读出来，然后累计技术
count()是一个聚合函数，对于返回的结果集，一行行地判断，如果count函数的参数不是null，累计值就加1，否则不加，最后返回累加值
count(*)、count(主键)、count(字段)、count(1)

性能
count(*) 越等于count(1) >count(主键) > count(字段)
推荐使用count(*)
```

**7、update优化**
```
InnoDB的行锁是针对索引加的锁，不是针对记录加的锁，并且该索引不能失效，否则会从行级锁升级为表锁。
表锁会影响性能。
尽量根据主键/索引字段进行数据更新
```
