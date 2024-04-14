**DML （Data Manipulation Language）
数据操作语言：用来对数据库表记录进行增删改**

添加数据：insert

- 给指定字段添加数据：
  insert into 表名(字段1,字段2,字段3,...) values(值1,值2,值3,...);

- 给全部字段增加：
 insert into 表名 values(值1,值2,值3,...);

- 批量添加数据：
insert into 表名(字段1,字段2,字段3,...),(值1,值2,值3,...);
insert into 表名 values(值1,值2,值3,...),(值1,值2,值3,...);

修改数据：update
update 表名 set 字段名1=值1,字段名2=值2, ... [where 条件]
条件如果没有的话就是修改整张表的该字段的数据

删除数据：delete
delete form 表名 [where 条件]
注意：
1、delete语句条件可以有，也可以没有，没有会删除该表所有数据
2、delete语句不能删除某一个字段的值，可以使用update把该字段赋值为null