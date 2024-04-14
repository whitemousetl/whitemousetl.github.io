**1、索引概述**
介绍：
索引（index）是帮助MySQL高效获取数据的数据结构（有序）。

在数据之外，数据库系统还维护着满足特定查找算法的数据结构，这些数据结构以某种方式引用（指向）数据，这样就可以在这些数据结构上实现高级查找算法，这种数据结构就是索引。

![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/3284748b-8094-4ae9-91d1-918230b66554)

```
优势：
提高数据检索的效率，减低数据库的IO成本。
通过索引列对数据进行排序，降低数据排序的成本，降低CPU的消耗。

劣势：
索引列也是要占用空间的。
索引大大地提高了查询效率，同时却也降低了更新表的速度，如对表进行insert、update、delete时，效率降低。
```

**2、索引结构**
```
MySQL的索引是在存储引擎层实现的，不同的存储引擎有不同的结构，主要包含以下几种：

B+Tree索引 最常见的索引类型，大部分引擎都支持B+树索引

Hash索引（性能高）  底层数据结构是用哈希表实现，只有精确匹配索引列的查询才有效，不支持范围查询

R-Tree（空间索引）空间索引是MyISAM引擎的一个特殊的索引类型，主要用于地理空间数据类型，通常使用较少

Full-Text（全文索引）一种通过建立倒排索引，快速匹配文档的方式。类似于Lucene，Solr，ES
```

![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/0d3c1c03-49cd-45ad-95e7-9993c41fc112)

```
二叉树：一个节点下面最多包含两个子节点，左边的比根节点小，右边的比根节点大。
二叉树缺点：顺序插入时，会形成一个链表，查询性能大大降低。大数据量情况下，层级较深，检索速度慢。
红黑树：红黑树是一个自平衡的二叉树，解决了顺序插入时，查询性能大大降低的问题，但是大数据量的情况下，层级较深，检索速度依然慢。
```

```
B-Tree（多路平衡查找树）
树的度数指的是一个节点的子节点个数
```
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/a8707bb4-92b0-4579-9802-b2896a4b487f)

```
B+Tree
所有的元素都会出现在叶子节点，非叶子节点左索引，叶子节点存放元素
叶子节点形成一个单向链表，每一个叶子节点都会通过指针指向下一个叶子节点
```
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/9a9ba698-36ad-48ba-8dae-377a0b05d6d8)

`MySQL索引数据结构对经典的B+树进行了优化。在原B+树的基础上，增加了一个指向相邻叶子节点的链表指针，就形成了带有顺序的指针的B+树，提高区间访问性能。`
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/5a9805fd-26de-4f66-a8a6-87a90665a21b)

Hash
哈希索引就是采用一定的hash算法，将键值换算成新的hash值，映射到对应的槽位上，然后存储在hash表中。
如果两个或多个键值，映射到一个相同的槽位上，他们就产生了hash冲突（也称为hash碰撞），可以通过链表来解决。

```
Hash索引特点：
1、Hash索引只能用于对等比较（=、in），不支持范围查询（between、>、< ...）。
2、无法利用索引完成排序操作。
3、查询效率高，通常只需要一次检索就可以了，效率通常要高于B+树索引。
```
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/c572276e-f38b-4201-9d8d-e3d5b714764d)

```
为什么InnoDB存储引擎选择使用B+树索引结构？
1、相对于二叉树，层级更少，搜索效率更高；
2、对于B树，无论是叶子节点还是非叶子节点，都会保存数据，这样导致一页中存储的键值减少，指针跟着减少，要同样保存大量数据，只能增加树的高度，导致性能降低。
3、相对于Hash索引，B+树索引支持范围匹配及排序操作。
```

**3、索引分类**
```
主键索引
针对于表中主键创建的索引
默认自动创建，只能有一个
primary key
```
```
唯一索引
避免同一个表中某数据列中的值重复
可以有多个
unique
```
```
常规索引
快速定位特定数据
可以有多个
```
```
全文索引
全文索引查找的是文本中的文件词，而不是比较索引中的值
可以有多个
fulltext
```

**在InnoDB存储引擎中，根据索引的存储形式，又可以分为两种。**
```
聚焦索引（行数据）
将数据与索引放到了一块，索引结构的叶子节点保存了行数据
必须有，且只有一个
```
```
二级索引（主键）
将数据与索引分开存储，索引结构的叶子节点关联的是对应的主键
可以存在多个
```
```
聚集索引选取规则：
如果存在主键，主键索引就是聚集索引。
如果不存在主键，将使用第一个唯一索引作为聚集索引。
如果没有主键，也没有唯一索引，InnoDB会自动生成一个rowid作为隐藏的聚集索引。
```

**回表查询**
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/e0e5d119-05cd-4a27-bd80-1e145a98597b)
先从二级索引查到Arm的id值，然后回到聚集索引通过id值查到该id值叶子节点上的row记录。

**思考题**
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/c5ce3b1d-648f-4974-8417-b5fb8e632470)
select * from user where id = 10;执行效率高，因为不需要回表查询。

![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/bf39b4fd-b5cf-4ac4-9582-ff47f42d712e)
如果数据超过了2200万行数据，那么高度会超过3，这时候可以考虑分库分页。

**4、索引语法**
```
创建索引
create [unique] [fulltext] index idx_表名_字段名 on table_name (index_col_name, ... );
如果没有unique或fulltext，那么这就是一个普通索引，如果一个索引只有一个字段，这种索引称为单列索引，如果一个索引有多个字段，这种索引称为联合索引或组合索引。
```

```
查看索引
show index from table_name;
```

`删除索引drop index index_name on table_name;`
