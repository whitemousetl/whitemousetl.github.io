**1、SQL执行频率**
```
MySQL客户端连接成功后，通过 show [session | global] status 命令可以提供服务器状态信息。
通过下面指令，可以查看当前数据库的insert、update、delete、select的访问频次：
show global status like 'Com____'; 一个下划线代表一个字符，一般七个下划线 
```
**2、慢查询日志**
```
慢查询日志记录了所有执行时间超过指定参数(long_query_time,单位：秒，默认10秒)的所有SQL语句的日志。
MySQL的慢查询日志默认没有开启，需要在MySQL的配置文件(/etc/my.cnf)中配置以下信息：
#开启慢查询日志
slow_query_log=1
#设置慢查询日志的时间为2秒，SQL语句执行超过2秒，就会被视为慢查询，记录到慢查询日志
long_query_time=2
配置完成后，重启MySQL服务器进行测试，查看慢日志文件中记录的信息 /var/lib/mysql/localhost-slow.log

Linux指令 tail -f /var/lib/mysql/localhost-slow.log持续查看最后一行
```
**3、profile详情**
```
show profiles 能够在做SQL优化时帮助我们了解时间都耗费到哪里去了。
通过have_profiling参数，能够看到当前MySQL是否支持profile操作
select @@have_profiling;
查看profiling是否开启
select @@profiling;
默认profiling是关闭的，可以通过set语句在session/global级别开profiling：
set profiling=1;
查看每一条SQL的耗时基本情况
show profiles;

查看指定query_id的SQL语句各个阶段的耗时情况
show profile for query query_id;

查看指定query_id的SQL语句CPU的使用情况
show profile cpu for query query_id;
```
**4、explain执行计划**
```
explain或者desc命令获取MySQL如何执行select语句的信息。包括在select语句执行过程中表如何连接和连接的顺序。
语法：直接在select语句之前加上关键字explain/desc
explain select 字段列表 from 表名 where 条件;
```
explain执行计划查出来的字段含义
```
id：
select查询的序列号，表示查询中执行select子句或者是操作表的顺序（id相同，操作顺序从上到下；id不同，值越大，越先执行）。
```
```
select_type：
表示select的类型，常见的取值有simple（简单表，即不使用表连接或者子查询）、
primary（主查询，即外层的查询）、
union（union中的第二个或者后面的查询语句）、
subquery（select/where之后包含的子查询）等
```
```
type（重要）：
表示连接类型，性能由好到差的连接类型为null、system、const、eq_ref、ref、range、index、all
null性能最好，all性能最差，优化时尽量按顺序往null方向优化。
null基本不可能，当查询时不涉及任何表可做到
如 select 'A';
system是访问系统表，一般优化到const就算是最好的了
const是根据主键和唯一索引进行访问
ref是使用非唯一索引进行访问的type
index代表用了索引但是也会遍历整个索引树
all代表的是全表扫描，性能很低
```
```
possible_key（次重要）
显示可能应用在这张表上的索引，一个或多个
```
```
key（次重要）
实际使用的索引，如果为null，则没有使用索引
```
```
key_len（次重要）
表示索引使用的字节数，该值为索引字段最大可能长度，在不损失精确度的前提下，长度越短越好
```
```
rows
MySQL认为必须要执行查询的行数，在innodb中是一个估算值，可能并不总是准确的。
```
```
filtered
表示返回结果的行数占需要读取行数的百分比，filtered的值越大越好
```