**1、事务简介**
```
事务是一组操作的集合，它是一个不可分割的工作单位，事务会把所有操作作为一个整体一起向系统提交或撤销操作请求，即这些操作要么同时成功，要么同时失败。
例子：银行转账
1、查询张三的余额
2、张三账户 -1000
3、李四账户 +1000
如果在第2第3步抛出异常，那么会出现张三账户减少了1000而李四账户没有增加1000的问题，这时候就需要事务把他们绑定在一起，保证同时成功或同时失败。
```
默认MySQL的事务是自动提交的，也就是说，当执行一条DML语句，MySQL会立即隐式地提交事务。

**2、事务操作** 
```
查看/设置事务的提交方式
select @@autocommit;
set @@autocommit = 0;
提交事务
commit;
回滚事务
rollback;
开启事务
start transaction 或 begin;
提交事务
commit;
回滚事务
rollback;
```
**3、事务的四大特性**
```
原子性：事务是不可分割的最小操作单元，要么全部成功，要么全部失败。

一致性：事务完成时，必须使所有数据都保持一致状态。

隔离性：数据库系统提供的隔离机制，保证事务在不受外部并发操作影响的独立环境下运行。

持久性：事务一旦提交或回滚，它对数据库中的数据的改变就是永久的。
```
**4、并发事务问题**
脏读：一个事务读到另外一个事务还没有提交的数据。
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/04cf274d-7ec4-4dd1-8175-1eacc0d3fb14)
不可重复读：一个事务先后读取同一条记录，但两次读取的数据不同，称之为不可重复读。
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/6498e2a2-b8c6-4cac-acaf-b913f69a94a3)
幻读：一个事务按照条件查询时，没有对应的数据行，但是在插入数据时，又发现了这行数据已经存在，好像出现了“幻影”
![image](https://github.com/whitemousetl/whitemousetl.github.io/assets/67313669/4d08868a-ac33-4b11-8344-b8775c091994)
**5、事务隔离级别**
```
read uncommitted  
脏读不可重复读幻读均会出现
read committed（Oracle默认）
脏读不会出现，但不可重复读幻读会出现
repeatable read（MySQL默认）
脏读不可重复读不会出现，但是幻读会出现
Serializable
脏读不可重复读幻读均不会出现
四种隔离级别从上到下隔离级别越来越高（数据越安全），性能越来越差
查看事务隔离级别
select @@transaction_isolation
设置事务隔离级别
set [session | global] transaction isolation level {read uncommitted | read committed | repeatable read | serializable}
```