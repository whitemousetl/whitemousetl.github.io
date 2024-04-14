**1、约束概述**
约束是作用于表中字段上的规则，用于限制存储在表中的数据
约束的目的是保证数据库中数据的正确性、有效性和完整性
```
约束的分类：
非空约束    限制该字段的数据不能为null   not null
唯一约束    保证该字段的所有数据都是唯一的、不重复的     unique
主键约束    主键是一行数据的唯一约束，要求非空且唯一     primary key
默认约束    保存数据时，如果未指定该字段的值，则采用默认约束    default
检查约束    保证约束满足某一个条件（8.0.16版本之后） check
外键约束    用来让两张表的数据之间建立连接，保证数据的一致性和完整性   foreign key
```
约束是作用于表中字段上的，可以在创建表/修改表的时候添加约束
自动增长 auto_increment外键约束

**2、约束演示**
根据需求，完成表结构的创建：
```
id            int                   主键，且自动增长
name      varchar(10)    不为空且唯一
age         int                   大于0且小于等于120
status     char(1)            如果没有指定，默认为1
gender    char(1)           无
```

**3、外键约束**
外键约束用来让两张表的数据之间建立连接，从而保证数据的一致性和完整性
添加外键语法：
```
创建表时
create table 表名(
    字段1 字段1类型，
    ... ,
    [constraint] [外键名称] foreign key(外键字段名) references 主表(主表列名)
);

修改表时
alter table 表名 add constraint 外键名称 foreign (外键字段名) references 主表(主表列名)；
```
删除外键语法：
`alter table 表名 drop foreign key 外键名称；`

**4、外键的删除/更新行为**
```
no action
当在父表删除/更新对应记录时，首先检查是否有对应外键，如果有则不允许删除/更新 （与RESTRICT一致）外键约束的默认行为
restrict
与NO ACTION一致
cascade
当在父表删除/更新对应记录时，首先检查是否有对应外键，如果有，则也删除/更新外键在子表中的记录
set null
当在父表删除对应记录时，首先检查是否有对应外键，如果有则设置子表中该外键值为null（这要求该外键允许取null）
set default（Innodb不支持）
当在父表删除/更新对应记录时，首先检查是否有对应外键，如果有，子表将外键列设置成一个默认值（Innodb不支持）
```
```
语法：
alter table 表名 add constraint 外键名称 foreign key（外键字段） references 主表名（主表字段名） on update cascade on delete cascade;
```